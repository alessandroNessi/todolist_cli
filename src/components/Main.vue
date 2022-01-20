<template>
  <main>
    <div class="main__container">

      <div class="input-group mb-3" id="input__form">

        <input
          name="newtask__input"
          type="text"
          class="form-control"
          @keyup.enter="insertTask"
          placeholder="Insert a new task"
        />

        <button
          class="btn btn-outline-secondary"
          @click="insertTask"
          type="button"
          id="newtask__button"
        >
          Submit
        </button>

      </div>

      <div class="task__container">
        <!-- @confirmEdit="saveTask" **NO LONGER USED** -->
        <Task
          v-for="(task, index) in this.tasks"
          :key="index"
          
          @askEdit="launchEdit"
          @emitDelete="deleteTask"
          @emitCopy="insertNewElement"
          :filter="filter"
          :task="task"
        ></Task>

      </div>
    </div>

    <div class="filters">

      <div class="d-flex filters__container align-items-center">

        <p
          v-if="this.filter == 'all'"
          @mouseup="showIncompleted"
          class="filter filter__left pointer"
        >
          hide completed
        </p>

        <p v-else @mouseup="showAll" class="filter filter__left pointer">
          show all
        </p>

        <p @mouseup="deleteCompleted" class="filter pointer">
          delete completed
        </p>

      </div>
    </div>
  </main>
</template>

//++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

<script>
import Task from "./Task.vue";

export default {
  name: "Main",

  components: {
    Task,
  },

  props: {
    tasks: Array,
  },

  data() {
    return {
      filter: "all", //data used to toggle the show of tasks completed
    };
  },

  methods: {

    //takes the value from the form and add to the tasks
    insertTask() {
      const target = document.getElementsByName("newtask__input")[0];
      const content = target.value;
      if (content != "") {
        target.value = "";
        this.insertNewElement(content);
      }
    },

    //insert a new element in the tasks array given a content and sum the unique id
    insertNewElement(content) {
      this.$emit("insertNewElement", content);
    },

    //delete the task with the given id
    deleteTask(id) {
      this.$emit("deleteTask", id);
    },

    //launch the edit overlay event
    launchEdit(id) {
      this.$emit("launchEdit", id);
      // if(this.editing==false){
      //     this.editing=id;
      //     this.toggleEdit(id,true);
      // }else if(this.editing==id){
      //     this.editing=false;
      //     this.toggleEdit(id,false);
      // }
    },
    //toggle the propriety editing of the current task
    // toggleEdit(id,value){
    //     let found=false;
    //     for(let i=0;i<this.tasks.length&&found==false;i++){
    //         if(this.tasks[i].id==id){
    //             found=true;
    //             this.tasks[i].editing=value;
    //         }
    //     }
    //     if(found==false){
    //         console.log("error on enabling edit: task not found");
    //     }
    // },

    //save a modified task
    saveTask(task) {
      this.$emit("saveTask", task);
    },

    //show just the tasks that are still to do
    showIncompleted() {
      if (this.filter == "all") {
        this.filter = "todo";
      }
    },

    //show all tasks
    showAll() {
      if (this.filter == "todo") {
        this.filter = "all";
      }
    },

    //delete all completed tasks
    deleteCompleted() {
      this.$emit("deleteCompleted");
    },
    
  },
};
</script>

//++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

<style scoped lang="scss">

.main__container {
  height: 70vh;
  border-radius: 5px;
  border: 1px solid var(--grey-400);
  overflow: hidden;
}

.task__container {
  height: calc(100% - var(--todo-element-height));
  //scrollbar personalization
  overflow-y: overlay;
  overflow-x: hidden;
  &::-webkit-scrollbar {
    width: var(--scrollbar-width);
  }
  &::-webkit-scrollbar-thumb {
    background: var(--scrollbar-color);
    border-radius: 5px;
  }
  &::-webkit-scrollbar-thumb:hover {
    background: var(--scrollbar-hover-color);
  }
}

#input__form {
  background-color: var(--white-700);
  margin-bottom: 0 !important;
  height: var(--todo-element-height);
  input {
    border: 0;
  }
  #newtask__button {
    border-width: 0px 0px 0px 1px;
    color: var(--gray-200);
  }
  border-bottom: 1px solid gray;
}

.filters {
  .filters__container {
    height: 1.5625rem;
    margin: 0.4rem 0;
  }
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  .filter {
    &:last-child {
      border-right: 0;
    }
    &__left {
      width: 133px;
      text-align: end;
    }
    padding: 0 5px;
    border-right: 2px solid var(--grey-400);
  }
}
/*******************RESPONSIVE********************/
@media screen and (max-width: 320px) {
  .filters .separator {
    display: none;
  }
  .filters .filters__container {
    width: 100%;
    justify-content: space-between;
  }
}
</style>