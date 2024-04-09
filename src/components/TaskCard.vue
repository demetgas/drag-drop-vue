<template>
  <div class="cardContainer">
    <div class="card">
      <div class="title"><div class="titleName">To Do</div></div>
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
.title {
  background-color: #a54b4a;
  width: 250px;
}
.titleName {
  color: white;
}
</style>
