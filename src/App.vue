<template>
<div>
  
  <navbar 
    :isLogin="isLogin"
    @changePage="changePage" 
    @isLogOut="logOut"
    :task = "tasks"
  ></navbar>
  <login 
    v-if="activePage === 'loginPage'"
    @switchPage="changePage" 
    @loginData="login" 
    @tokenGoogle="loginGoogle"
  ></login>
  <register 
    v-else-if="activePage === 'registerPage'"
    @dataRegister='register'
  ></register>
  <home 
    v-else-if="activePage === 'homePage'" 
    :loadTask = "tasks"
    @emitLoadTasks="fetchTask"
    @emitDeletedTask="deleteTask"
    @emitEditTask="findIdTask"
    @changeStatus="findIdTaskStatus"
    
  ></home>
  <taskAdd 
    v-else-if="activePage === 'addPage'"
    @addData="addData"
  ></taskAdd>
  <editTask
    v-else-if="activePage === 'editPage'"
    :loadData = "dataTask"
    @emitEdit = "editData"
  ></editTask>
   

</div>
  
  
</template>

<script>
import login from './pages/login'
import editTask from './pages/edit'
import home from './pages/home'
import navbar from './components/Navbar';
import register from './pages/register'
import axios from './api/axios'
import taskAdd from './pages/addTask'
export default {
  name: "app",
  data() {
    return {
      activePage: "loginPage",
      isLogin: false,
      tasks: [],
      dataTask: {},
      username: [],
      clientId: 'cliend-id'
    };
  },
  components:{navbar, login, home, register, editTask, taskAdd},
  methods:{
    changePage(namePage) {
      this.activePage = namePage
    },
    //Login method >>>>>>>
      login(input){
            let {email,password} = input
            // console.log(email,password,'form app');
            axios({
                method:'POST',
                url: "/login",
                data : {
                    email 
                    ,password
                }
            })
            .then((response)=>{
                //console.log(response.data);
                localStorage.setItem("access_token", response.data.access_token)
                this.activePage = 'homePage'
                this.isLogin = true
            })
            .catch((err)=>{
                console.log(err);
            })
    
        },
      //fetch task method >>>>>>
      fetchTask(){
        axios({
          method: "GET",
          url: "/tasks/",
          headers: {
            access_token: localStorage.access_token
          }
        })
        .then((response)=>{
          this.tasks = response.data
          
          //console.log(response.data,'app');
          
        })
        .catch((err)=>{
          console.log(err);
        })
      },
      //register
      register(input){
        let {username,email,password} = input
        //console.log(username,email,password);
        axios({
          method: "POST",
          url: "/register",
          data: {
            username,email,password
          }
        })
        .then((response)=>{
          // console.log(response);
          this.activePage = 'loginPage'
        })
        .catch((err)=>{

        })
   
      },
      deleteTask(task){
          axios({
            method: "delete",
            url: `/tasks/${task.id}`,
            headers: {
            access_token: localStorage.access_token
            }
          })
          .then((response)=>{
            console.log(response.data);
            this.fetchTask()
            
          })
          .catch((err)=>{
            console.log(err);
          })
          
      }, addData(input){
        let {title,description} =  input
        
           axios({
            method: "post",
            url: `/tasks/`,
            headers: {
            access_token: localStorage.access_token
            },
            data: {
            title,description
          }
          })
          .then(({data})=>{
            this.fetchTask
            this.activePage='homePage'
          })
          .catch((err)=>{
            console.log(err);
          })  
      }, findIdTask(input){
          this.activePage = input.page
          axios({
            method: "get",
            url:`/tasks/${input.id}`,
            headers: {
            access_token: localStorage.access_token
            }
          })
          .then(({data}) =>{ 
            this.dataTask = data
          })
          .catch(err=>{
            console.log(err);
          })
      }, editData(input){
          let {title, description, id} = input
          // console.log(title, description, id);
          axios({
            method: "put",
            url: `/tasks/${id}`,
            headers: {
            access_token: localStorage.access_token
            },
            data: {
              title,description
            }
          })
          .then(()=>{
            this.fetchTask()
            this.activePage='homePage'
            })
            .catch((err)=>{
              console.log(err);
          })
      },logOut(input){
        let {page, status} = input
        this.activePage = page,
        this.isLogin = status
        localStorage.removeItem("access_token")

        var auth2 = gapi.auth2.getAuthInstance();
        auth2.signOut().then(function () {
        console.log('User signed out.');
    })
      },findIdTaskStatus(input){
          let {id, status} = input
          axios({
            method: "get",
            url:`/tasks/${id}`,
            headers: {
            access_token: localStorage.access_token
            }
          })
          .then(({data}) =>{ 
            let input = {status,data}
            this.changeStatus(input)
          })
          .catch(err=>{
            console.log(err);
          })


      },loginGoogle(token){
         const id_token = token

            axios({
                method:'POST',
                url: "/loginGoogle",
                data : {
                   token
                }
            }).then((response)=>{
              //console.log(response.data.access_token);
              localStorage.setItem("access_token", response.data.access_token)
                this.activePage = 'homePage'
                this.isLogin = true
            })


          
      },changeStatus(input){
        let {category, id} = input.data
        if(input.status === 'next'){
          if(category === 'backlog'){
            category = 'doing'
          } else if(category === 'doing'){
            category = 'todo'
          } else if(category === 'todo'){
            category = 'done'
          }
        } else {
          if(category === 'done'){
            category = 'todo'
          } else if(category === 'todo'){
            category = 'doing'
          } else if(category === 'doing'){
            category = 'backlog'
          }
        }
        
        axios({
            method: "patch",
            url:`/tasks/${id}`,
            headers: {
            access_token: localStorage.access_token
            },
            data: {
              category
            }
          })
          .then(() =>{ 
            this.fetchTask()
            
          })
          .catch(err=>{
            console.log(err);
          })
      }, 
       
  },
 
  created(){
      this.fetchTask()
  } 
};
</script>

<style scoped>

</style>