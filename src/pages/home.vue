<template>
   <div class="bg-image" 
            style="background-image: url('https://trumpwallpapers.com/wp-content/uploads/Pixel-Art-Wallpaper-12-1920-x-1080.jpg');
             height: 100vh;
            background-size: 1500px
            ">
    
    <div class="jumbotron text-center ">
      <h1>Welcome to Kanban-KITA</h1>
      <p>Being Productive isn't criminal!!!</p>
    </div>
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