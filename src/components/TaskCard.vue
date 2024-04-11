<template>
  <div class="cardContainer">
    <div v-for="dataItem in data" :key="dataItem.id" class="card">
      <div class="title" :style="{ backgroundColor: dataItem.backgroundColor }">
        <div class="titleName">{{ dataItem.id }}</div>
      </div>
      <div class="list">
        <div
          class="listItem"
          :draggable="true"
          v-for="(task, taskIndex) in displayTasks(dataItem)"
          :key="taskIndex"
        >
          {{ task.name }}
        </div>
        <button
          v-if="dataItem.tasks.length > 5"
          class="btn"
          @click="toggleShowMoreTasks(dataItem.id)"
        >
          {{ showMoreTasks[dataItem.id] ? "Show Less" : "Load More" }}
        </button>
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
      showMoreTasks: {},
    };
  },

  methods: {
    toggleShowMoreTasks(id) {
      this.showMoreTasks = {
        ...this.showMoreTasks,
        [id]: !this.showMoreTasks[id],
      };
    },
    displayTasks(dataItem) {
      return this.showMoreTasks[dataItem.id]
        ? dataItem.tasks
        : dataItem.tasks.slice(0, 5);
    },
  },
};
</script>

<style scoped>
.cardContainer {
  display: flex;
}
.card {
  border-radius: 5px;
  margin-right: 20px;
  text-align: center;
  font-family: "Times New Roman", Times, serif;
}
.title {
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
.btn {
  border-radius: 5px;
  padding: 10px;
  margin: auto;
  margin-top: auto;
  margin-bottom: 20px;
  border: none;
  color: white;
  font-weight: bold;
  background-color: rgb(74, 83, 112);
}

.btn:hover {
  background-color: rgb(54, 62, 86);
}
</style>
