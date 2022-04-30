<template>
    <div class="container">
    <div class="row">
      <div class="col-md-6 offset-md-3">
     
        <div class="card my-5">

          <form @submit.prevent="login" class="card-body cardbody-color p-lg-5">

            <div class="text-center">
              <img src="https://cdn.pixabay.com/photo/2016/03/31/19/56/avatar-1295397__340.png" class="img-fluid profile-image-pic img-thumbnail rounded-circle my-3"
                width="200px" alt="profile">
            </div>

            <div class="mb-3">
              <input v-model="email" type="text" class="form-control" id="Email" aria-describedby="emailHelp"
                placeholder="e-mail">
            </div>
            <div class="mb-3">
              <input v-model="password" type="password" class="form-control" id="password" placeholder="password">
            </div>
            <div class="text-center"><button type="submit" class="btn btn-color px-5 mb-5 w-100">Login</button></div>
            <div id="emailHelp" class="form-text text-center mb-5 text-dark">Not
              Registered? <router-link :to="'/register'" class="text-dark fw-bold"> Create an
                Account</router-link>
            </div>
          </form>
        </div>
          
      </div>
    </div>
  </div>
</template>


<script>
import axios from 'axios';

export default {
    name : 'LoginView',
    data(){
      return {
        email:null,
        password:null
      }
    },
    methods:{
      login:function(){

        console.log('login')
        let payload = {
          email: this.email,
          password: this.password
        }
        axios
          .post('http://localhost:3000/api/auth/login',payload)
          .then(response => console.log(response.data))
          .catch(error => console.log(error))
        // this.$router.push('/')
      } 
    }
}
</script>


<style>
    .btn-color{
  background-color: #0e1c36;
  color: #fff;
  
}

.profile-image-pic{
  height: 200px;
  width: 200px;
  object-fit: cover;
}



.cardbody-color{
  background-color: #ebf2fa;
}

a{
  text-decoration: none;
}
</style>