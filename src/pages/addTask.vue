<template>
    
    <div class="container">
      <div class="row">
        <div class="col-4 offset-4 mt-4 " >
          <h3>Add Task</h3> 
          <form @submit.prevent="addData"> 
            <div class="form-group">
              <label for="exampleInputTitle">Title</label>
              <input type="text" class="form-control" v-model="title" aria-describedby="emailHelp">
            </div>
            <div class="form-group ">
              <label for="exampleInputDescription">Description</label>
              <input type="text" class="form-control" v-model="description">
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
          </form> 
        </div>
      </div>
    </div>
</template>

<script>

export default {
    name:"addTask",
    data(){
      return{
        title:'',
        description:''
      }
    },
    methods:{
      addData(){
        let input = {title:this.title, description:this.description}
        console.log(input);
        this.$emit("addData", input )
      }
    }
}
</script>

<style>

</style>