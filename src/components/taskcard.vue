<template>
    <div>
        <div class="card mt-3" >
            <div class="card-body">
                <h5 class="card-title">{{task.title}}</h5>
                <label for="floatingInputInvalid">Description:</label>
                <p class="card-text">{{task.description}}</p>
                <div>
                     <button 
                        type="button" 
                        class="btn btn-primary" 
                        @click.prevent="editTask"
                        >
                        Edit
                    </button>
                    <button @click.prevent="deleteTask" class="btn btn-danger" type="button">Delete</button> <br>
                    <button v-if="task.category !== 'done'" @click.prevent="changeStatus('next')" class="btn btn-primary mt-2" type="button">Next</button>
                    <button v-if="task.category !== 'backlog'" @click="changeStatus('back')" class="btn btn-primary mt-2" type="button">Back</button>
                </div>
                <h6 class="card-subtitle mb-2 text-muted jarak-atas" >{{task.User.username}}</h6>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: "TaskCard",
    props: ["task"],
    methods:{
      deleteTask(){
         // console.log(this.task.id,'card');
          this.$emit('emitDeletedTask', {id: this.task.id})
      },
      editTask(){
          let input = {page: 'editPage', id: this.task.id }
          this.$emit('emitEditTask', input)
      },
      changeStatus(status){
          //console.log(this.task.id, 'task');
          let input = {status,id: this.task.id }
          console.log(input, "task");
          this.$emit('changeStatus', input )
      }
    }
}
</script>

<style>

</style>