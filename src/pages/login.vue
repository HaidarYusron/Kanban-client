<template>
    <div>
            <!-- LOGIN --> 
        <div class="bg-image" 
            style="background-image: url('https://mdbootstrap.com/img/Photos/Others/images/76.jpg');
            height: 100vh">
            <div class="container">
                <div class="row">
                    <div class="col-4 offset-4 mt-4" >
                        <h3 >Login</h3>
                        <form @submit.prevent="login">
                        <div class="form-group" >
                            <label for="exampleInputEmail1">Email address</label>
                            <input type="email" class="form-control" v-model="email" aria-describedby="emailHelp">
                            <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
                        </div>
                        <div class="form-group">
                            <label for="exampleInputPassword1">Password</label>
                            <input type="password" class="form-control" v-model="password">
                        </div>
                        <button type="submit" class="btn btn-primary">Submit</button>
                        </form> 
                        <button v-google-signin-button="`320537985281-58gn2doblr30r45oektfbufbl2ie07vj.apps.googleusercontent.com`" class="google-signin-button mt-2"> Continue with Google</button>
                    </div>

                    
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: "login",
    data(){
        return {
            email: "",
            password: ""
        }
    },

    methods: {
        login(){
            let input = {email:this.email,password:this.password}
            // console.log(input,'dari login');
            this.$emit("loginData", input )
        },
        OnGoogleAuthSuccess (idToken) {
        //console.log(idToken,'>>>>ID TOKEN<<<<')
        this.$emit("tokenGoogle", idToken )
      // Receive the idToken and make your magic with the backend
        },
        OnGoogleAuthFail (error) {
          console.log(error,'>>>>ERROR<<<<')
        }
        
    }
}
</script>

<style>
.google-signin-button {
  color: white;
  background-color: rgb(7, 131, 248);
  height: 50px;
  font-size: 16px;
  border-radius: 5px;
  padding: 10px 20px 25px 20px;
  
}
</style>