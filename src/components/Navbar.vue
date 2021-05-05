<template>
  <div  >
      <!-- NAVBAR -->
    <nav class="navbar navbar-expand-lg navbar-light bg-warning shadow">
        <div class="container-fluid">
          <a  class="navbar-brand "  >Kanban KITA</a>
          <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarText" aria-controls="navbarText" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarText">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li v-if="isLogin === true" class="nav-item">
                <a class="nav-link active" aria-current="page" @click.prevent="changePage('homePage')" >Home</a>
              </li>  
              <li v-if="isLogin === false" class="nav-item">
                <a class="nav-link active" aria-current="page" @click.prevent="changePage('registerPage')">Register</a>
              </li> 
              <li>
                <button 
                  type="button" 
                  class="btn btn-primary" 
                  @click.prevent="changePage('addPage')"
                  v-if="isLogin === true"
                >
                  ADD TASk
                </button>
              </li>
            </ul>
            
            <span class="navbar-text ">
                <a class="nav-link" 
                v-if="isLogin === true"
                @click.prevent="isLogOut"
                
                >LOGOUT</a>
            </span>
          </div>
        </div>
      </nav>
      
  </div>
</template>

<script>

export default {
  name: "Navbar",
  props: ["isLogin",'task'],
  methods: {
    changePage(val){
      this.$emit('changePage', val)
    },
    isLogOut(){
      let status = ({status:false, page:'loginPage'})
      this.$emit('isLogOut', status)
    }
   
  },
  components: {
    
  }
}
</script>

<style>

</style>