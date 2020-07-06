<template>
  <div class="header">
    <h1>Todo App</h1>
  </div>
</template>

<script>
export default {
  name: "Header"
};
</script>

<style>
.header {
  color: #3b90ff;
  display: flex;
  min-height: 8vh;
  align-items: center;
  justify-content: center;
  font-size: 1rem;
  background: #232323;
  box-shadow: rgba(0, 0, 0, 0.05) 0px 5px 10px;
  z-index: 2;
}
</style>