<template>
  <div class="cardContainer">
    <div class="card">
      <div class="title"><div class="titleName">To Do</div></div>
      <div class="list">
        <div class="items"><div class="listItems">Task 1</div></div>
      </div>
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
  border-radius: 5px;
  padding: 48px;
  border: 1px solid #ccc;
}
.titleName {
  font-weight: bold;
  color: white;
  width: 250px;
}
</style>
