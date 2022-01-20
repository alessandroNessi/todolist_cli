<template>
  <div
    :style="{
      backgroundImage:
        'url(' + require(`./common/images/${this.bgrImage}.jpg`) + ')',
    }"
    class="container-fluid app py-4 position-relative"
    id="app"
  >
  <div v-if="this.editing!=false" class="d-flex justify-content-center align-items-center overlay position-absolute">
    <div class="input-group edit__input">
      <input @keyup.enter="confirmEdit" name="edittask__input" type="text" class="edit__input--task form-control" :value="0" :placeholder="'edit task'">
      <button @click="confirmEdit" class="btn btn-outline-secondary" type="button"><i class="fas fa-check-double"></i></button>
    </div>
  </div>
    <div class="container d-flex" id="main__container">
      <Header
        @changeDayNight="changeDayNight"
        title="TodoList"
        :day="day"
      ></Header>
      <Main
        @deleteCompleted="deleteCompleted"
        @saveTas="saveTask"
        @deleteTask="deleteTask"
        @insertNewElement="insertNewElement"
        @launchEdit="launchEdit"
        :tasks="tasks"
        :nextId="nextId"
      ></Main>
      <Footer></Footer>
    </div>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  data() {
    return {
      nextId: 7, //unique id
      day: true,
      editing:false,
      bgrImage: "day",
      tasks: [
        {
          id: 1,
          status: "todo",
          editing: false,
          content:
            "primo Lorem ipsum dolor, sit amet consectetur adipisicing elit. Assumenda quasi sunt quis minima consectetur hic totam officia exercitationem rerum harum animi optio, ex eveniet cupiditate quos, nulla dolor dolorum sapiente!",
        },
        {
          id: 2,
          status: "todo",
          editing: false,
          content: "secondo task",
        },
        {
          id: 3,
          status: "todo",
          editing: false,
          content: "terzo task",
        },
        {
          id: 4,
          status: "todo",
          editing: false,
          content: "quarto task",
        },
        {
          id: 5,
          status: "todo",
          editing: false,
          content: "quinto task",
        },
        {
          id: 6,
          status: "todo",
          editing: false,
          content: "sesto task",
        },
      ],
    };
  },
  components: {
    // HelloWorld,
    Header,
    Main,
    Footer,
  },
  methods: {
    launchEdit(id){
      this.editing=id;
    },
    //delete all completed tasks
    deleteCompleted() {
      this.tasks = this.tasks.filter((task) => {
        if (task.status != "completed") {
          return task;
        }
      });
    },
    //save a modified task
    saveTask(task) {
      let found = false;
      for (let i = 0; i < this.tasks.length && found == false; i++) {
        if (this.tasks[i].id == task.id) {
          found = true;
          this.tasks[i] = task;
          this.editing = false;
        }
      }
      if (found == false) {
        console.log("error on saving edit: task not found");
      }
    },
    //delete the task with the given id
    deleteTask(id) {
      let found = false;
      for (let i = 0; i < this.tasks.length && found == false; i++) {
        if (this.tasks[i].id == id) {
          found = true;
          this.tasks.splice(i, 1);
          if (this.editing == id) {
            this.editing = false;
          }
        }
      }
      if (found == false) {
        console.log("error on delete: task not found");
      }
    }, //insert a new element in the tasks array given a content and sum the unique id
    insertNewElement(content) {
      this.tasks.push({
        id: this.nextId,
        status: "todo",
        editing: false,
        content: content,
      });
      this.nextId++;
    },
    changeDayNight() {
      const r = document.querySelector(":root");
      if (this.day == true) {
        this.day = false;
        this.bgrImage = "night";
        r.style.setProperty("--task-hover", "rgb(35,35,35)");
        r.style.setProperty("--task-odd", "rgb(20,20,45)");
        r.style.setProperty("--task-even", "rgb(35,45,55)");
        r.style.setProperty("--yellow-400", "#bb6633");
        r.style.setProperty("--red-400", "#bb5555");
        r.style.setProperty("--blue-400", "#5555bb");
        r.style.setProperty("--green-400", "#55bb55");
        r.style.setProperty("--grey-200", "#ddd");
        r.style.setProperty("--grey-400", "#aaa");
        r.style.setProperty("--grey-600", "#777");
        r.style.setProperty("--grey-700", "#333");
        r.style.setProperty("--white-700", "#222");
        r.style.setProperty("--main-container-bg-color", "rgba(0,0,0,0.5)");
        r.style.setProperty("--black-700", "#fff");
        r.style.setProperty("--scrollbar-color", "#555");
        r.style.setProperty("--scrollbar-hover-color", "#aaa");
      } else {
        this.day = true;
        this.bgrImage = "day";
        r.style.setProperty("--task-hover", "rgb(220,220,220)");
        r.style.setProperty("--task-odd", "rgb(255,255,230)");
        r.style.setProperty("--task-even", "rgb(235,255,235)");
        r.style.setProperty("--yellow-400", "#ffcc00");
        r.style.setProperty("--red-400", "#ff3333");
        r.style.setProperty("--blue-400", "#3333ff");
        r.style.setProperty("--green-400", "#009900");
        r.style.setProperty("--grey-200", "#333");
        r.style.setProperty("--grey-400", "#777");
        r.style.setProperty("--grey-600", "#aaa");
        r.style.setProperty("--grey-700", "#ddd");
        r.style.setProperty("--white-700", "#fff");
        r.style.setProperty(
          "--main-container-bg-color",
          "rgba(255,255,255,0.7)"
        );
        r.style.setProperty("--black-700", "#000");
        r.style.setProperty("--scrollbar-color", "#888");
        r.style.setProperty("--scrollbar-hover-color", "#555");
      }
    },
  },
};
</script>

<style lang="scss">
@import "~bootstrap/dist/css/bootstrap.css";
@import "./common/css/variabiles.css";
@import "./common/css/common.css";
.app {
  font-family: "Roboto", sans-serif;
  // background-image: url("./common/images/bgr.jpg");
  // background-image:var(--main-bg-img);
  background-size: cover;
  background-position: center;
  height: 100vh;
  * {
    background-color: var(--main-bg-color);
  }
  .overlay{
    background-color: rgba(0,0,0,0.5);
    z-index: 1;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
  }
  #main__container {
    background-color: var(--main-container-bg-color);
    box-shadow: 0 0 3px 3px var(--main-container-bg-color);
    backdrop-filter: blur(6px);
    border-radius: 0.5rem;
    flex-direction: column;
    justify-content: center;
    max-width: var(--max-width);
  }
}
</style>
