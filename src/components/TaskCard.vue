<template>
  <div class="cardContainer">
    <div class="card">
      <div class="title"><div class="titleName">To Do</div></div>
      <div class="list">
        <div class="listItem">Task 1</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: [
        {
          id: "To Do",
          tasks: [
            { name: "task 1" },
            { name: "task 2" },
            { name: "task 3" },
            { name: "task 4" },
            { name: "task 5" },
            { name: "task 6" },
            { name: "task 7" },
            { name: "task 8" },
          ],
          backgroundColor: "#A54B4A",
        },
        {
          id: "In Progress",
          tasks: [{ name: "task 9" }, { name: "task 10" }],
          backgroundColor: "#4A71A5",
        },
        {
          id: "Done",
          tasks: [
            { name: "task 11" },
            { name: "task 12" },
            { name: "task 13" },
          ],
          backgroundColor: "#4AA561",
        },
        {
          id: "Even",
          tasks: [
            { name: "task 14" },
            { name: "task 16" },
            { name: "task 18" },
          ],
          backgroundColor: "#A5A14A",
        },
      ],
    };
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
.listItem {
  border-radius: 5px;
  margin: 5px 7px;
  background-color: rgb(224, 225, 228);
  color: black;
  padding: 40px;
  width: 250px;
  border: 1px solid #fcfcfc;
  font-weight: bold;
  cursor: pointer;
  overflow: visible;
}
</style>
