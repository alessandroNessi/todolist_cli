<template>
  <!-- <div @mouseenter="msg" class="task list__element d-flex align-items-center px-1"> -->
  <div class="task list__element d-flex justify-content-between align-items-center px-1">
      <div class="content__container">
        <p :class="this.task.editing?'d-none':''">{{task.content}}</p>
        <div :class="this.task.editing?'d-flex':'d-none'" class="edit__input" id="input__form">
            <input name="newtask__input" type="text" class="form-control" :value="this.task.content" @keyup.enter="insertTask" :placeholder="'edit '+this.task.id+' task'">
            <button class="btn btn-outline-secondary" type="button">Submit</button>
        </div>
      </div>
      <div class="options__container">
          <button @mouseup="copyOption" class="options option__copy"><i class="far fa-copy"></i></button>
          <button @mouseup="editOption" class="options option__edit"><i class="far fa-edit"></i></button>
          <button @mouseup="deleteOption" class="options option__delete"><i class="far fa-trash-alt"></i></button>
      </div>
  </div>
</template>

<script>
export default {
    name:"Task",
    data() {
        return {
            onedit:false
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
            width: 100%;
            margin-right: 1rem;
            .edit__input{
                display: flex;
                width: 100%;
                .form-control{
                    min-width: 100px;
                }
                .btn{
                    // padding-left:2px;
                    // padding-right:2px;
                }
            }
        }
        .options__container{
            // min-width: 5.25rem;
        }
    }
</style>