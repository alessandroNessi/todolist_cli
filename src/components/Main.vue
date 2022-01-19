<template>
  <main>
      <div class="main__container">
        <div class="input-group mb-3" id="input__form">
            <input name="newtask__input" type="text" class="form-control" @keyup.enter="insertTask" placeholder="Insert a new task">
            <button class="btn btn-outline-secondary" @click="insertTask" type="button" id="newtask__button">Submit</button>
        </div>
        <div class="task__container">
            <Task @confirmEdit="saveTask" @askEdit="checkEditing" @emitDelete="deleteTask" @emitCopy="insertNewElement" v-for="(task, index) in this.tasks" :key="index" :task="task"></Task>
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
            editing:false,
            tasks:[{
                id:1,
                status:"todo",
                editing:false,
                content:"primo Lorem ipsum dolor, sit amet consectetur adipisicing elit. Assumenda quasi sunt quis minima consectetur hic totam officia exercitationem rerum harum animi optio, ex eveniet cupiditate quos, nulla dolor dolorum sapiente!"
            },
            {
                id:2,
                status:"todo",
                editing:false,
                content:"secondo task"
            },
            {
                id:3,
                status:"todo",
                editing:false,
                content:"terzo task"
            },
            {
                id:4,
                status:"todo",
                editing:false,
                content:"quarto task"
            },
            {
                id:5,
                status:"todo",
                editing:false,
                content:"quinto task"
            },
            {
                id:6,
                status:"todo",
                editing:false,
                content:"sesto task"
            },
            ],
        };
    },
    methods:{
        insertTask(){
            const target=document.getElementsByName("newtask__input")[0];
            const content = target.value;
            if(content!=""){
                target.value="";
                this.insertNewElement(content);
            }
        },
        insertNewElement(content){
            this.tasks.push({
                id:this.nextId,
                status:"todo",
                editing:false,
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
                    if(this.editing==id){
                        this.editing=false;
                    }
                }
            }
            if(found==false){
                console.log("error on delete: task not found");
            }
        },
        checkEditing(id){
            // alert(task.id);
            if(this.editing==false){
                this.editing=id;
                this.toggleEdit(id,true);
            }else if(this.editing==id){
                this.editing=false;
                this.toggleEdit(id,false);
            }
        },
        toggleEdit(id,value){
            let found=false;
            for(let i=0;i<this.tasks.length&&found==false;i++){
                if(this.tasks[i].id==id){
                    found=true;
                    this.tasks[i].editing=value;
                }
            }
            if(found==false){
                console.log("error on enabling edit: task not found");
            }
        },
        saveTask(task){
            console.log(task);
            let found=false;
            for(let i=0;i<this.tasks.length&&found==false;i++){
                if(this.tasks[i].id==task.id){
                    found=true;
                    this.tasks[i]=task;
                    this.editing=false;
                }
            }
            if(found==false){
                console.log("error on saving edit: task not found");
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
        background-color: var(--white-700);
        margin-bottom: 0!important;
        height: var(--todo-element-height);
        input{
            border:0;
        }
        #newtask__button{
            border-width:0px 0px 0px 1px;
            color: var(--gray-200);
        }
        border-bottom: 1px solid gray;
    }
</style>