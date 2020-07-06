<template>
  <div id="app">
    <Header />
    <Todo />
  </div>
</template>

<script>
import Header from "./components/Header";
import Todo from "./components/Todo";

export default {
  name: "App",
  components: {
    Header,
    Todo
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap");

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  overflow: hidden;
  color: #f8f8f8;
  background: #191919;
  font-family: "Poppins", sans-serif;
}
</style>
