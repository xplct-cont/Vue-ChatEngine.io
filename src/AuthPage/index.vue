<template>
    <div class="login-page mx-auto col-md-4 p-3" style="margin-top: 100px;">
      <div class="card p-2 ml-2" style="background: linear-gradient(60deg, #29323c 0%, #485563 100%)">
        <form @submit.prevent="login">
          <div class="title mb-3 ml-2">Login</div>
          <input placeholder="Username" class="mb-3 ml-2 bg-light rounded inp" type="text" v-model="username" />
          <br />
          <input placeholder="Password" class="mb-3 ml-2 bg-light rounded inp" type="password" v-model="password">
          <br />

          <div class="d-flex justify-content-end"><button type="submit" class="mb-2 btn bg-primary col-md-3 text-light">Login</button></div> <br>
          <a href="#" type="button" id="openModalBtn" class="btn" style="color:white; text-decoration:none; margin-left: 10px; margin-bottom: 10px; font-size: 12px;">Register an account</a>
        </form>
        <div> 
   </div>

   <div id="myModal" class="modal mx-auto col-md-4 p-3">
      <div class="modal-content p-3" style="background: linear-gradient(60deg, #29323c 0%, #485563 100%)">
       <span class="close" style="cursor:pointer;">&times;</span>
        <form @submit.prevent="signup">
          <div class="title mb-1">Sign Up</div>
          <input
            class="input mb-3 bg-light rounded inp" placeholder="Username" type="text" v-model="username" />
          <br />
          <input placeholder="Password" class="mb-3 bg-light rounded inp" type="password" v-model="password" />
          <br />
          <input placeholder="Email" class="mb-3 bg-light rounded inp" type="text" v-model="email" />
          <br />
          <input placeholder="First name" class="mb-3 bg-light rounded inp" type="text" v-model="first_name" />
          <br />
          <input placeholder="Last name" class="mb-3 bg-light rounded inp" type="text" v-model="last_name" />
          <br />
          <button type="submit" class="mb-2 btn bg-primary text-light">Sign Up</button>
        </form>
       </div>
    </div>


      </div>
    </div>
  </template>
  
  <script>
  import { loginRest, signupRest } from "./api";

  export default {
    data() {
      return {
        username: "",
        password: "",
        email: "",
        first_name: "",
        last_name: "",
      };
    },
    methods: {
      login() {
        loginRest(this.username, this.password)
          .then((response) =>
            this.$emit("onAuth", { ...response.data, secret: this.password })
          )
          .catch((error) => console.log("Login error", error));
      },
      signup() {
        signupRest(
          this.username,
          this.password,
          this.email,
          this.first_name,
          this.last_name
        )
          .then((response) =>
            this.$emit("onAuth", { ...response.data, secret: this.password })
          )
          .catch((error) => console.log("Sign up error", error));
      },
    },   
  };


  </script>
