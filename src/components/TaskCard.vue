<template>
  <div class="cardContainer">
    <div class="card">
      <div class="title"><div class="titleName">To Do</div></div>
      <div class="list">
        <div class="listItems">Task 1</div>
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
.card {
  border-radius: 5px;
  margin-right: 20px;
  text-align: center;
}
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
.list {
  display: flex;
  flex-direction: column;
  border-radius: 5px;
  background-color: rgb(192, 196, 209);
  height: 680px;
  overflow-y: auto;
  overflow-x: hidden;
}
</style>
