<template>
  <!--Edit Task-->
       <div class="container">
      <div class="row">
        <div class="col-4 offset-4 mt-4 " >
          <h3>Edit Task</h3> 
          <form @submit.prevent="editTask"> 
            <div class="form-group">
              <label for="exampleInputTitle">Title</label>
              <input type="text" class="form-control"  aria-describedby="emailHelp" v-model="loadData.title">
            </div>
            <div class="form-group ">
              <label for="exampleInputDescription">Description</label>
              <input type="text" class="form-control"  v-model="loadData.description">
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
          </form> 
        </div>
      </div>
    </div>
</template>

<script>
export default {
    name:"edit",
    props:['loadData'],
    methods:{
      editTask(){
        this.$emit("emitEdit", this.loadData)
      }
    }
}
</script>

<style>

</style>