<template>
  <main>
      <div class="main__container my-3">
        <div class="input-group mb-3" id="input__form">
            <input name="newtask__input" type="text" class="form-control" @keyup.enter="insertTask" placeholder="Insert a new task">
            <button class="btn btn-outline-secondary" @mouseup="insertTask" type="button" id="newtask__button">Submit</button>
        </div>
        <div class="task__container">
            <Task @emitDelete="deleteTask" @emitCopy="insertNewElement" v-for="(task, index) in this.tasks" :key="index" :task="task"></Task>
        </div>
      </div>
  </main>
</template>

<script>
import Task from "./Task.vue";

export default {
    name:"Main",
    components:{
        Task
    },
    data() {
        return {
            nextId:7,
            tasks:[{
                id:1,
                status:"todo",
                content:"primo task"
            },
            {
                id:2,
                status:"todo",
                content:"secondo task"
            },
            {
                id:3,
                status:"todo",
                content:"terzo task"
            },
            {
                id:4,
                status:"todo",
                content:"quarto task"
            },
            {
                id:5,
                status:"todo",
                content:"quinto task"
            },
            {
                id:6,
                status:"todo",
                content:"sesto task"
            },
            ],
        };
    },
    methods:{
        insertTask(){
            const target=document.getElementsByName("newtask__input")[0];
            const content = target.value;
            target.value="";
            this.insertNewElement(content);
        },
        insertNewElement(content){
            this.tasks.push({
                id:this.nextId,
                status:"todo",
                content:content
            });
            this.nextId++;
        },
        deleteTask(id){
            let found=false;
            for(let i=0;i<this.tasks.length&&found==false;i++){
                if(this.tasks[i].id==id){
                    found=true;
                    this.tasks.splice(i,1);
                }
            }
            if(found==false){
                console.log("error on delete: task not found");
            }
        }
    }
}
</script>

<style scoped lang="scss">
    .main__container{
        height: 70vh;
        border-radius: 5px;
        border:1px solid grey;
        overflow: hidden;
    }
    .task__container{
        height: calc(100% - var(--todo-element-height));
//scrollbar personalization
        overflow-y: overlay;
        overflow-x: hidden;
        &::-webkit-scrollbar {
            width: var(--scrollbar-width);
        }
        &::-webkit-scrollbar-thumb {
            background: var(--scrollbar-color);
            border-radius:5px
        }
        &::-webkit-scrollbar-thumb:hover {
            background:var(--scrollbar-hover-color);
        }
    }
    #input__form{
        margin-bottom: 0!important;
        height: var(--todo-element-height);
        #newtask__button{
            border-width:0px 0px 0px 1px;
        }
        border-bottom: 1px solid gray;
    }
</style>