<template>
  <div class="cardContainer">
    <div
      v-for="dataItem in data"
      :key="dataItem.id"
      class="card"
      :style="dragging ? styleCard(dataItem.id) : null"
    >
      <div class="title" :style="{ backgroundColor: dataItem.backgroundColor }">
        <div class="titleName">{{ dataItem.id }}</div>
        <div class="titleName">
          -
          {{
            dataItem.tasks.length === 0
              ? "No tasks available"
              : dataItem.tasks.length === 1
              ? "1 task"
              : dataItem.tasks.length + " tasks"
          }}
          -
        </div>
      </div>
      <div
        class="list"
        @dragover.prevent
        @drop="handleDrop($event, dataItem.id)"
      >
        <div
          class="listItem"
          :class="{ dragging }"
          :draggable="true"
          v-for="(task, taskIndex) in displayTasks(dataItem)"
          :key="taskIndex"
          @dragstart="handleDragStart($event, task.name, dataItem.id)"
          @dragenter="handleDragEnter({ id: dataItem.id, task }, taskIndex)"
          :style="dragging ? styleTask(task.name) : null"
        >
          <font-awesome-icon class="icon" :icon="faGripVertical" />
          <div class="taskName">
            {{ task.name }}
          </div>
        </div>
        <button
          v-if="dataItem.tasks.length > 6"
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
import { ref } from "vue";
import { data } from "../data.js";
import { faGripVertical } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
export default {
  data() {
    return {
      data: JSON.parse(localStorage.getItem("tasks")) || data,
      showMoreTasks: {},
      dragging: false,
      dragItem: ref(null),
      dragNode: ref(null),
      dragOverCard: null,
    };
  },
  components: {
    FontAwesomeIcon,
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
        : dataItem.tasks.slice(0, 6);
    },
    handleDragStart(e, taskName, tasks) {
      console.log("hello");
      e.dataTransfer.setData("id", taskName);
      this.dragItem = { tasks, task: { name: taskName } };
      this.dragNode = e.target;
      // if (this.dragNode) {
      this.dragNode.addEventListener("dragend", this.handleDragEnd);
      //  }
      this.dragging = true;
    },
    handleDragEnd() {
      console.log("bye");
      this.dragging = false;
      if (this.dragNode) {
        this.dragNode.removeEventListener("dragend", this.handleDragEnd);
      }
      this.dragItem = null;
      this.dragNode = null;
    },
    checkEven(cardId, taskName) {
      if (
        cardId === "Even" &&
        parseInt(taskName.replace("task", "")) % 2 !== 0
      ) {
        return false;
      }
      return true;
    },
    handleDrop(e, cardId) {
      const taskName = e.dataTransfer.getData("id");
      if (!this.checkEven(cardId, taskName)) {
        return;
      }
      const updatedData = this.data.map((card) => {
        if (card.id === cardId) {
          if (card.tasks.find((task) => task.name === taskName)) {
            return card;
          }
          return {
            ...card,
            tasks: [...card.tasks, { name: taskName }],
          };
        } else {
          return {
            ...card,
            tasks: card.tasks.filter((task) => task.name !== taskName),
          };
        }
      });
      this.data = updatedData;
      localStorage.setItem("tasks", JSON.stringify(updatedData));
    },
    handleDragEnter(params, taskIndex) {
      const currentItem = this.dragItem;
      this.dragOverCard = params.id;
      if (!this.checkEven(params.id, currentItem.task.name)) {
        return;
      }
      const updatedData = this.data.map((card) => {
        if (card.id === params.id) {
          const newTasks = [...card.tasks];
          const draggedItem = newTasks.findIndex(
            (task) => task.name === currentItem.task.name
          );

          if (draggedItem !== -1) {
            newTasks.splice(draggedItem, 1);
          }
          newTasks.splice(taskIndex, 0, currentItem.task);
          return { ...card, tasks: newTasks };
        } else {
          return {
            ...card,
            tasks: card.tasks.filter(
              (task) => task.name !== currentItem.task.name
            ),
          };
        }
      });
      this.data = updatedData;
      localStorage.setItem("tasks", JSON.stringify(updatedData));
    },
    styleTask(taskName) {
      const currentItem = this.dragItem;
      if (currentItem.task.name === taskName) {
        return {
          backgroundColor: "rgb(27, 28, 31, 0.1)",
          border: "none",
          color: "rgb(0, 0, 0, 0.2)",
          textDecoration: "underline",
        };
      }
      return null;
    },
    styleCard(id) {
      if (this.dragOverCard === id) {
        if (this.checkEven(id, this.dragItem.task.name)) {
          return {
            border: "2px solid white",
          };
        }
      }
      return null;
    },
  },
  computed: {
    faGripVertical() {
      return faGripVertical;
    },
  },
};
</script>

<style scoped>
.cardContainer {
  display: flex;
  font-family: "Times New Roman", Times, serif;
  gap: 20px;
}
.card {
  border-radius: 10px;
}
.title {
  padding: 43px;
  align-items: center;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  border: 1px solid #ccc;
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.titleName {
  font-weight: bold;
  color: white;
  width: 250px;
}
.list {
  display: flex;
  flex-direction: column;
  background-color: rgb(192, 196, 209);
  height: 680px;
  overflow-y: auto;
  overflow-x: hidden;
  align-items: center;
}
.listItem {
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 5px;
  margin: 5px 7px;
  background-color: rgb(224, 225, 228);
  color: black;
  padding: 35px 40px;
  width: 250px;
  border: 1px solid #fcfcfc;
  font-weight: bold;
  overflow: visible;
  cursor: grab;
  text-align: center;
  justify-content: space-between;
  transition: transform 0.3s, background-color 0.3s, color 0.3s;
}
.listItem:active {
  cursor: grabbing;
  box-shadow: 2px 2px 5px #73767a;
}
.listItem:hover {
  transform: scale(1.03);
  background-color: #858997;
  color: white;
  .icon {
    color: white;
  }
}
.listItem.dragging:hover {
  box-shadow: none;
  transform: none;
  background-color: rgb(224, 225, 228);
  color: black;
  .icon {
    color: rgb(125, 120, 120);
  }
}

.icon {
  margin-right: 10px;
  color: rgb(125, 120, 120);
  font-size: 15px;
}
.taskName {
  padding: 0;
  margin: 0;
  margin-right: 4.5rem;
  width: 100px;
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
