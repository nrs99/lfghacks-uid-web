<template>
  <center>
    <div class="login">
      <div class="form">
        <h1>Login</h1>
        <label>Username:</label>
        <input type="text" name="usrname" v-model="username">
        <label>Password:</label>
        <input type="password" name="pswd" v-model="password">
        <button type="submit" @click="verifyAccount" value="Submit">Login</button>
      </div>
    </div>
  </center>
</template>

<style lang="scss" scoped>
.login {
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
export default class Home extends Vue {
  message = "Welcome to Your Vue.js +yoyoyo";
  username = "";
  password = "";

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
        localStorage.setItem('token',response.data.token);
        this.$router.push("/authorize");
      })
      .catch(error => {
        console.log(error);
        alert(error);
      });
  }
}
</script>
