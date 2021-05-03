<template>
  <!-- CARD KANBAN -->
   
               <div class="col-4 mt-5 " style="max-height: 80vh; overflow-y: auto;"> 
                    <h3 class="text-center">{{category}}</h3>
                        <TaskCard
                            v-for="task in groupedTask"
                            :key="task.id"
                            :task="task"
                            @emitDeletedTask="deleteTask"
                            @emitEditTask="editTask"
                            @changeStatus="changeStatus"
                        ></TaskCard>
               </div>
      
</template>

<script>
import TaskCard from './taskcard';
export default {
    name: "category",
    components: {
        TaskCard
    },
    props: ["category","tasks"],
    computed: {
        groupedTask(){
            return this.tasks.filter(task => task.category == this.category.toLowerCase())
        }
    },
     methods:{
      deleteTask(id){
        //   console.log(id,'category');
          this.$emit('emitDeletedTask', id)
      },
      editTask(input){
          this.$emit('emitEditTask', input)
      },
      changeStatus(id){
        //console.log(id,'category');
        this.$emit('changeStatus', id)
      }
    }
}
</script>

<style>

</style>