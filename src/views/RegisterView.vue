<template>
    <div class="container">
    <div class="row">
      <div class="col-md-6 offset-md-3">
     
        <div class="card my-5">

          <form @submit.prevent="register" class="card-body cardbody-color p-lg-5">

            <div class="text-center">
              <img src="https://cdn.pixabay.com/photo/2016/03/31/19/56/avatar-1295397__340.png" class="img-fluid profile-image-pic img-thumbnail rounded-circle my-3"
                width="200px" alt="profile">
            </div>

            <div class="mb-3">
              <input v-model="email" @change="cleanMailError" v-bind:class="{ inputError: emailError}" type="text" class="form-control" id="Email" aria-describedby="emailHelp"
                placeholder="E-mail">
            </div>
            <div class="mb-3">
              <input v-model="password" @change="cleanPasswordError" v-bind:class="{ inputError: passwordError || matchingError}" type="password" class="form-control" id="password" placeholder="Password">
            </div>
            <div class="mb-3">
              <input v-model="passwordConfirm" @change="cleanPasswordConfirmError" v-bind:class="{ inputError: passwordConfirmError || matchingError }" type="password" class="form-control" id="passwordConfirm" placeholder="Password confirmation">
            </div>
            <span v-if="errMsg" class="mb-3 fw-bold text-danger">{{errMsg}}</span>
            <div class="text-center"><button type="submit" class="btn btn-color px-5 mb-5 w-100">Register</button></div>
            <div id="emailHelp" class="form-text text-center mb-5 text-dark">Not
              Already have an account ? <router-link :to="'/login'" class="text-dark fw-bold"> Login</router-link>
            </div>
          </form>
        </div>

      </div>
    </div>
  </div>
</template>


<script>
import axios from 'axios'
export default {
    name : 'RegisterView',
    data(){
        return {
            email:null,
            password:null,
            passwordConfirm:null,
            emailError:false,
            passwordError:false,
            passwordConfirmError:false,
            matchingError:false,
            errMsg:null,
            successMsg:null,
        }
    },
    computed:{
        registrationError:function(){
            if(this.emailError || this.passwordError || this.passwordConfirmError || this.matchingError){
                return true
            } else {
                return false
            }
        }
    },
    methods:{
        register(){
            if(!this.email){
                this.emailError = true;
                this.errMsg = 'E-mail is missing';
                return
            }
            if(!this.password){
                this.passwordError = true;
                this.errMsg = 'Password is missing';
                return
            }
            if(!this.passwordConfirm){
                this.passwordConfirmError = true;
                this.errMsg = 'Password confirmation is missing';
                return
            }
            if(this.password !== this.passwordConfirm){
                this.matchingError = true
                this.errMsg = 'Passwords must match';
                return
            }
            let payload = {
                email: this.email,
                password: this.password
            }
            axios
                .post('http://localhost:3000/api/auth/signup',payload)
                .then((response) => {
                  console.log(response.data.message);
                  this.successMsg = response.data.message;
                })
                .catch(error => console.log(error))
            this.$router.push('/')
        },
        cleanMailError(){
            this.errMsg = null;
            this.emailError = false;
        },
        cleanPasswordError(){
            this.errMsg = null;
            this.passwordError = false;
            this.matchingError = false;
        },
        cleanPasswordConfirmError(){
            this.errMsg = null;
            this.passwordConfirmError = false;
            this.matchingError = false;
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
.inputError{
    border: 1px solid red;
}
</style>