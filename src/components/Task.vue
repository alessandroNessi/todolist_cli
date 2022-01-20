<template>
  <!-- <div @mouseenter="msg" class="task list__element d-flex align-items-center px-1"> -->
  <div v-if="this.filter=='all'||(this.filter==this.task.status)" class="task list__element d-flex justify-content-between align-items-center px-1">
      <div class="content__container" @mouseup="checkAsDone">
        <div :class="this.task.editing?'d-none':''">
            <p :class="this.task.status=='completed'?'completed pointer':'pointer'">{{task.content}}</p>
        </div>
        <!-- <div v-if="this.task.editing" class="input-group edit__input">
            <input @keyup.enter="confirmEdit" name="edittask__input" type="text" class="edit__input--task form-control" :value="this.task.content" :placeholder="'edit '+this.task.id+' task'">
            <button @click="confirmEdit" class="btn btn-outline-secondary" type="button"><i class="fas fa-check-double"></i></button>
        </div> -->
      </div>
      <div class="options__container">
          <button @click="copyOption" class="options option__copy"><i class="far fa-copy"></i></button>
          <button @click="editOption" class="options option__edit">
            <i class="far fa-edit yellow"></i>
            <!-- <i v-else class="fas fa-undo-alt yellow"></i> -->
          </button>
          <button @click="deleteOption" class="options option__delete"><i class="far fa-trash-alt"></i></button>
      </div>
  </div>
</template>

<script>
// import { component } from 'vue/types/umd';?????????non l'ho scritto io, copia incolla da node?
export default {
    name:"Task",
    data() {
        return {
            // inputValue
        };
    },
    props: {
        filter: String,
        task: Object,
    },
    methods:{
        copyOption(){
            this.$emit('emitCopy',this.task.content);
        },
        editOption(){
            this.$emit('askEdit',this.task.id);
        },
        confirmEdit(){
            this.task.content=document.getElementsByName("edittask__input")[0].value;
            this.task.editing=false;
            this.$emit('confirmEdit',this.task);
        },
        deleteOption(){
            this.$emit('emitDelete',this.task.id);
        },
        checkAsDone(){
            if(this.task.editing==false){
                if(this.task.status=="todo"){
                    this.task.status="completed";
                }else{
                    this.task.status="todo";
                }
                this.$emit('confirmEdit',this.task);
            }
        },
    }
}
</script>

<style scoped lang="scss">
    .task{
        overflow-y: auto;
        &:nth-child(2n){
            background: linear-gradient(0deg, rgba(0,0,0,0) 0%, var(--task-even) 5%, var(--task-even) 95%, rgba(0,0,0,0) 100%);
        }
        &:nth-child(2n-1){
            background: linear-gradient(0deg, rgba(0,0,0,0) 0%, var(--task-odd) 5%, var(--task-odd) 95%, rgba(0,0,0,0) 100%);
        }
        &:hover{
            background: var(--task-hover);
            .options{
                background: var(--white-700);
            }
        }
        height: var(--todo-element-height);
        border-bottom: 1px solid gray;
        .options__container{
            display: flex;
            // flex-direction: column;
            .options{
                width: 1.75rem;
                height: 1.75rem;
                border: 1px solid lightgray;
                border-radius: 1rem;
                margin-left: 0.5rem;
                &:first-child{
                    margin-left: 0px;
                }
                &:hover{
                    transform: scale(1.1);
                    background-color: var(--white-700);
                    transition: transform 100ms linear;
                }
            }
        }
        .content__container{
            width: calc(100% - 6.75rem);
            max-height: calc(100% - 0.2rem);
            overflow:overlay ;
            &::-webkit-scrollbar {
                height: var(--scrollbar-width);
                width: var(--scrollbar-width);
            }
            &::-webkit-scrollbar-thumb {
                background: var(--scrollbar-color);
                border-radius:5px
            }
            &::-webkit-scrollbar-thumb:hover {
                background:var(--scrollbar-hover-color);
            }
            margin-right: 1rem;
            // .edit__input{
            //     display: flex;
            //     width: 100%;
            //     .form-control{
            //         min-width: 100px;
            //     }
            //     &--task{
            //         background-color: white;
            //     }
            //     .btn{
            //         height: calc(var(--todo-element-height) - 0.60rem);
            //         align-self: center;
            //         display: flex;
            //         justify-content: center;
            //         align-items: center;
            //         background-color: var(--white-700);
            //         color: var(--green-400);
            //     }
            // }
        }
        .options__container{
            .fa-copy{
                color: var(--blue-400);
            }
            .yellow{
                color: var(--yellow-400);
            }
            .fa-trash-alt{
                color: var(--red-400);
            }
        }
    }
    @media screen and (max-width: 375px) {
        .task .options__container .options{
            margin-left: 0rem;
            width: 1.65rem;
            height: 1.65rem;
        }
        .task .content__container{
            width: calc(100% - 4.25rem);
            margin-right: 0.5rem;
        }
    }
    @media screen and (max-width: 320px) {
        .task .options__container .options{
            margin-left: 0rem;
            width: 1.45rem;
            height: 1.45rem;
            font-size: 0.9rem;
        }
        .task .content__container{
            width: calc(100% - 3.25rem);
            margin-right: 0.3rem;
        }
    }
</style>