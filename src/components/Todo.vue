<template>
  <div class="todo-wrapper">
    <form @submit.prevent="addTodo">
      <input
        type="text"
        v-model="todo"
        v-validate="'required'"
        name="task"
        placeholder="Enter a task..."
      />
      <transition
        enter-active-class="animate__animated animate__bounceIn"
        leave-active-class="animate__animated animate__bounceOut"
      >
        <p class="alert" v-if="errors.has('task')">
          {{ errors.first("task") }}
        </p>
      </transition>
    </form>

    <ul>
      <p class="no-todo" v-if="todos.length < 1">
        You haven't created any tasks yet
      </p>
      <transition-group
        enter-active-class="animate__animated animate__bounceInUp"
        leave-active-class="animate__animated animate__bounceOutDown"
      >
        <li v-for="todo in todos" :key="todo.id">
          <div class="todo">
            <div class="check-input">
              <input
                type="checkbox"
                class="checkbox"
                @change="markComplete(todo.id)"
              />
              <p :class="{ completed: todo.completed }">{{ todo.title }}</p>
            </div>
            <i class="fa fa-minus-circle" @click="deleteTodo(todo.id)"></i>
          </div>
        </li>
      </transition-group>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      todos: [],
      todo: ""
    };
  },
  methods: {
    addTodo() {
      const newTodo = {
        id:
          this.todos.length > 0 ? this.todos[this.todos.length - 1].id + 1 : 1,
        title: this.todo,
        completed: false
      };
      this.todos = [...this.todos, newTodo];
      this.todo = "";
    },

    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },

    markComplete(id) {
      const todo = this.todos.find(todo => todo.id === id);
      todo.completed = !todo.completed;
    }
  }
};
</script>

<style>
@import url("https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css");
@import url("https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.0.0/animate.min.css");

.todo-wrapper {
  background: #232323;
  display: flex;
  flex-direction: column;
  margin: 100px auto;
  border-radius: 8px;
  box-shadow: rgba(0, 0, 0, 0.05) 0px 5px 10px;
  width: 560px;
}

input[type="text"] {
  padding: 13px 15px;
  font-family: "Poppins", sans-serif;
  background: #f8f8f8;
  border: none;
  outline: none;
  line-height: 1.6;
  border-radius: 8px 8px 0 0;
  font-size: 1.1rem;
  width: 100%;
}

ul {
  list-style: none;
}

ul li {
  padding: 20px;
  background: #1f1e1e;
  color: rgb(209, 209, 209);
}

.alert {
  background: #3b90ff;
  padding: 10px 20px;
  text-align: center;
  font-size: 0.9rem;
}

.todo {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.check-input {
  display: flex;
  align-items: center;
}

input[type="checkbox"] {
  margin-right: 10px;
  cursor: pointer;
}

li:last-of-type {
  border-radius: 0 0 8px 8px;
}

i {
  cursor: pointer;
}

.no-todo {
  padding: 28px 20px;
  text-align: center;
  font-size: 1.1rem;
}

.completed {
  text-decoration: line-through;
}
</style>