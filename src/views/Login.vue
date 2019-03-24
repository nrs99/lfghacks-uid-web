<template>
  <center><div class="login">
    <img alt="Vue logo" src="../assets/logo.png" style="width:300px;height:200px;">
    <!-- <HelloWorld v-bind:msg="message"/> -->

    <br>Username:
    <input type="text" name="usrname" v-model="username">
    <br>Password:
    <input type="text" name="pswd" v-model="password">
    

    <!-- <button type="submit" @click="createAccount" value="Submit">Create Account</button> -->
    <center><button type="submit" @click="verifyAccount" value="Submit">Login</button></center>

  </div></center>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src
import axios from "axios";

interface LoginResponse {
  token:string
}

@Component({
  components: {
    HelloWorld
  }
})
export default class Home extends Vue {
  message = "Welcome to Your Vue.js +yoyoyo";
  username = "";
  password = "";
  createAccount() {
    console.log(this.username);
    const body = {
      username: this.username,
      password: this.password
    };
    axios
      .post("https://lfghacks.ngrok.io/account", body)
      .then(response => {
        console.log(response);
      })
      .catch(error => {
        console.log(error);
      });
  }

  verifyAccount() { // Make a request for a user with a given ID
    console.log(this.username);
    const body = {
      username: this.username,
      password: this.password
    };
    axios
      .post<LoginResponse>("https://lfghacks.ngrok.io/login", body)
      .then(response => {
        console.log(response.data.token);
        this.$router.push('/login/authorize');
      })
      .catch(error => {
        console.log(error);
      });
  }
}
</script>
