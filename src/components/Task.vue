<template>
  <!-- <div @mouseenter="msg" class="task list__element d-flex align-items-center px-1"> -->
  <div class="task list__element d-flex justify-content-between align-items-center px-1">
      <div class="content__container">
        <p>{{task.content}}</p>
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
        return {};
    },
    props: {
        task: Object,
    },
    methods:{
        copyOption(){
            this.$emit('emitCopy',this.task.content);
        },
        editOption(){
            alert("edit "+this.task.id);
        },
        deleteOption(){
            // alert("delete "+this.task.id);
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
    }
</style>