<template>
  <div>
  <div class="container">
    <div class="row"> <br>
      
      <Category 
        v-for="(cat,i) in categories" 
        :key="i"
        :category="cat"
        :tasks= "loadTask"
        @emitDeletedTask="deleteTask"
        @emitEditTask="editTask"
        @changeStatus="changeStatus"
      ></Category>
    </div>
  </div>
        
  </div>
</template>

<script>
import Category from '../components/category';

export default {
    name:"home",
    data(){
      return {
        categories: ['Backlog','Doing','Todo','Done']
      }
    },
    components: {Category},
    props:['loadTask'],
   
    created(){
      this.$emit('emitLoadTasks')
    },
    methods: {
      deleteTask(id){
          //console.log(id,'home');
          this.$emit('emitDeletedTask', id)
      },
      editTask(input){
        this.$emit('emitEditTask', input)
      },
       changeStatus(id){
        console.log(id,'home');
        this.$emit('changeStatus', id)
      }
    }


}
</script>

<style>

</style>