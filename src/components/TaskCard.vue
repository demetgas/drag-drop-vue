<template>
  <div class="cardContainer">
    <div class="card">
      <div class="title"><h1 class="titleName">To Do</h1></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TaskCard",
  props: {
    msg: String,
  },
};
</script>

<style scoped>
.titleName {
  color: white;
}
</style>
