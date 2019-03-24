<template>
  <div class="home">
    <div class="form">
      <h1>Create Account</h1>
      <label>Full name:</label>
      <input type="text" name="fullname" v-model="fullname">
      <label>Username:</label>
      <input type="text" name="usrname" v-model="username">
      <label>Password:</label>

      <input type="password" name="pswd" v-model="password">
      <button type="submit" @click="createAccount" value="Submit">Submit</button>
    </div>
    <!-- <HelloWorld v-bind:msg="message"/> -->
  </div>
</template>

<style lang="scss" scoped>
.home {
  text-align: center;
  .form {
    display: inline-block;
    width: 200px;
    text-align: left;
    > * {
      display: block;
    }
    button {
      margin-top: 10px;
    }
    input {
      margin-bottom: 15px;
    }
  }
}
</style>


<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src
import axios from "axios";

interface LoginResponse {
  token: string;
}

@Component({
  components: {
    HelloWorld
  }
})
export default class CreateAccount extends Vue {
  fullname = "";
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
        alert('recieved!')
      })
      .catch(error => {
        console.log(error);
        alert(error);
      });
  }

  verifyAccount() {
    // Make a request for a user with a given ID
    console.log(this.username);
    const body = {
      username: this.username,
      password: this.password
    };
    axios
      .post<LoginResponse>("https://lfghacks.ngrok.io/login", body)
      .then(response => {
        console.log(response.data.token);
        alert('Account created');
      })
      .catch(error => {
        alert(error);
        console.log(error);
      });
  }
}
</script>
