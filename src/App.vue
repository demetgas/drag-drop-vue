<template>
  <div class="App">
    <TaskCard />
  </div>
</template>

<script>
import TaskCard from "./components/TaskCard.vue";

export default {
  components: {
    TaskCard,
  },
};
</script>

<style>
#root {
  background-color: #292727;
}
.App {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #292727;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
