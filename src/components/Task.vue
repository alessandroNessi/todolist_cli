<template>
  <!-- <div @mouseenter="msg" class="task list__element d-flex align-items-center px-1"> -->
  <div class="task list__element d-flex justify-content-between align-items-center px-1">
      <div class="content__container">
        <p :class="this.task.editing?'d-none':''">{{task.content}}</p>
        <div v-if="this.task.editing" class="edit__input">
            <input @keyup.enter="confirmEdit" name="edittask__input" type="text" class="form-control" :value="this.task.content" :placeholder="'edit '+this.task.id+' task'">
            <button @click="confirmEdit" class="btn btn-outline-secondary rounded-circle" type="button"><i class="fas fa-check"></i></button>
        </div>
      </div>
      <div class="options__container">
          <button @click="copyOption" class="options option__copy"><i class="far fa-copy"></i></button>
          <button @click="editOption" class="options option__edit"><i class="far fa-edit"></i></button>
          <button @click="deleteOption" class="options option__delete"><i class="far fa-trash-alt"></i></button>
      </div>
  </div>
</template>

<script>
export default {
    name:"Task",
    data() {
        return {
            // inputValue
        };
    },
    props: {
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
        //example targetting function on event
        // msg: function(event){
        //     event.target.getElementsByTagName("p")[0].style.display = "none";
        // }
    }
}
</script>

<style scoped lang="scss">
    .task{
        overflow-y: auto;
        background-color: lightblue!important;
        height: var(--todo-element-height);
        border-bottom: 1px solid gray;
        &:last-child{
            border-bottom: 0px;
        }
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
            }
        }
        .content__container{
            width: calc(100% - 7.75rem);
            overflow-x:overlay ;
            &::-webkit-scrollbar {
                height: var(--scrollbar-width);
            }
            &::-webkit-scrollbar-thumb {
                background: var(--scrollbar-color);
                border-radius:5px
            }
            &::-webkit-scrollbar-thumb:hover {
                background:var(--scrollbar-hover-color);
            }
            margin-right: 1rem;
            .edit__input{
                display: flex;
                width: 100%;
                .form-control{
                    min-width: 100px;
                }
                .btn{
                    width: calc(var(--todo-element-height) - 0.6rem);
                    background-color: var(--gray-300);
                    color: var(--green-400);
                }
            }
        }
        .options__container{
            // min-width: 5.25rem;
        }
    }
    @media screen and (max-width: 375px) {
        .options{
            margin-left: 0rem!important;
        }
        .content__container{
            width: calc(100% - 5.25rem)!important;
        }
    }
</style>