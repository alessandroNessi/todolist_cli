<template>

  <div
    :style="{
      backgroundImage:
        'url(' + require(`./common/images/${this.bgrImage}.jpg`) + ')',
    }"
    class="container-fluid app py-4 position-relative"
    id="app"
  >

    <div
      :class="this.editing != false?'d-flex':'d-none'"
      class="
        d-flex
        justify-content-center
        align-items-center
        overlay
        position-absolute
      "
    >

      <div class="edit__input">

        <div class="edit__input--container">

          <button @mouseup="closeEdit" class="edit__input--container--closebutton rounded-circle"><i class="far fa-times-circle"></i></button>

          <h6 for="edittask__input">Edit the text in the input below</h6>

          <div class="input-group">

            <input
              @keyup.enter="confirmEdit"
              name="edittask__input"
              id="edittask__input"
              type="text"
              class="edit__input--task form-control"
              :placeholder="'edit task'"
            />

            <button
              @click="confirmEdit"
              class="btn btn-outline-secondary"
              type="button"
            >
              <i class="fas fa-check-double"></i>
            </button>

          </div>

        </div>

      </div>

    </div>

    <div class="container d-flex" id="main__container">

      <Header
        @changeDayNight="changeDayNight"
        title="TodoList"
        :day="day"
      ></Header>
<!-- @saveTask="saveTask" **NO LONGER USED** -->
      <Main
        @deleteCompleted="deleteCompleted"
        @deleteTask="deleteTask"
        @insertNewElement="insertNewElement"
        @launchEdit="launchEdit"
        :tasks="tasks"
      ></Main>

      <Footer></Footer>

    </div>
    
  </div>

</template>

//++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";
import Footer from "./components/Footer.vue";

export default {

  name: "App",

  data() {
    return {
      nextId: 7, //unique id
      day: false, //setted to false to swap on day on create
      editing: false, //status of current editing controlling the show ov the overlay input
      currentTask: null, //just the index of the task to pass to the overlay, to avoid another for
      bgrImage: "day", //initial bgr image
      tasks: [  //list of tasks
        {
          id: 1,
          status: "todo",
          editing: false,
          content:
            "puntare la sveglia per domani mattina",
        },
        {
          id: 2,
          status: "todo",
          editing: false,
          content: "comprare il pane",
        },
        {
          id: 3,
          status: "todo",
          editing: false,
          content: "Medico di base venerdì 24 alle 09.30",
        },
        {
          id: 4,
          status: "todo",
          editing: false,
          content: "messaggio molto lungo messaggio molto lungo messaggio molto lungo messaggio molto lungo messaggio molto lungo messaggio molto lungo messaggio molto lungo messaggio molto lungo messaggio molto lungo messaggio molto lungo messaggio molto lungo messaggio molto lungo messaggio molto lungo messaggio molto lungo messaggio molto lungo messaggio molto lungo ",
        },
        {
          id: 5,
          status: "todo",
          editing: false,
          content: "andare in palestra",
        },
        {
          id: 6,
          status: "todo",
          editing: false,
          content: "preparare la cena e il pranzo per domani",
        },
      ],
    };
  },

  components: {
    Header,
    Main,
    Footer,
  },

  //oncreated i create the color vars for day mode
  created(){
    this.changeDayNight();
  },

  methods: {

    //display the hidden input for edit
    launchEdit(id) {
      this.editing = id;
      let found = false;
      for (let i = 0; i < this.tasks.length && !found; i++) {
        if (this.tasks[i].id == id) {
          found = true;
          this.currentTask=i;
          document.getElementById('edittask__input').value=this.tasks[i].content;
        }
      }
      if (!found) {
        console.log("error on delete: task not found");
        this.editing=false;
      }
    },

    //on close edit empty the input value end hide the overlay
    closeEdit() {
      this.editing = false;
      document.getElementById('edittask__input').value="";
    },

    //on confirm update the task
    confirmEdit(){
      this.tasks[this.currentTask].content=document.getElementById('edittask__input').value;
      this.closeEdit();
    },

    //delete all completed tasks
    deleteCompleted() {
      this.tasks = this.tasks.filter((task) => {
        if (task.status != "completed") {
          return task;
        }
      });
    },

    //save a modified task **NO LONGER USED**
    // saveTask(task) {
    //   let found = false;
    //   for (let i = 0; i < this.tasks.length && found == false; i++) {
    //     if (this.tasks[i].id == task.id) {
    //       found = true;
    //       this.tasks[i] = task;
    //       this.editing = false;
    //     }
    //   }
    //   if (found == false) {
    //     console.log("error on saving edit: task not found");
    //   }
    // },

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
    }, 
    
    //insert a new element in the tasks array given a content and sum the unique id
    insertNewElement(content) {
      this.tasks.push({
        id: this.nextId,
        status: "todo",
        editing: false,
        content: content,
      });
      this.nextId++;
    },

    //change the color vars for the night/day modes
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

//++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

<style lang="scss">
@import "~bootstrap/dist/css/bootstrap.css";
@import "./common/css/variabiles.css";
@import "./common/css/common.css";
.app {
  font-family: "Roboto", sans-serif;
  background-size: cover;
  background-position: center;
  height: 100vh;
  * {
    background-color: var(--main-bg-color);
  }

  .overlay {
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 1;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    backdrop-filter: blur(3px);

    .edit__input {
      display: flex;
      width: var(--max-width);
      .form-control {
        min-width: 100px;
      }
      .btn {
        height: calc(var(--todo-element-height) - 0.6rem);
        align-self: center;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: var(--white-700);
        color: var(--green-400);
      }
      &--container{
        position: relative;
        background-color: var(--white-700);
        border-radius: .4375rem;
        padding: .9375rem;
        width: 100%;
        &--closebutton{
          width: 1.5625rem;
          height: 1.5625rem;
          font-size: 1.5rem;
          color: var(--red-400);
          border: none;
          // border:2px solid var(--black-700);
          position: absolute;
          top: 0;
          right: .3125rem;
        }
      }
      &--task {
        background-color: white;
      }
    }
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
