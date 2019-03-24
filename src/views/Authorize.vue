<template>
  <div class='auth'>
    <div class="form">
      <h3>What personal data would you like to share with a client?</h3>
      <input type="checkbox" id="Age" value="Age" v-model="checkedNames">
      <label for="Age">Age</label>
      <br>
      <input type="checkbox" id="Over21" value="Over21" v-model="checkedNames">
      <label for="Over21">Over21</label>
      <br>
      <input type="checkbox" id="SSN" value="SSN" v-model="checkedNames">
      <label for="SSN">SSN</label>
      <br>
      <input type="checkbox" id="CardPayment" value="CardPayment" v-model="checkedNames">
      <label for="CardPayment">CardPayment</label>
      <br>

       <label>Key Id:</label>
      <input type="text" name="key" v-model="key">
        <button type="submit" @click="createKey" value="Submit">Submit</button>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.auth {
  text-align: center;
  .form {
    display: inline-block;
    width: 200px;
    text-align: left;
    > * {
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
import axios from "axios";

@Component
export default class Authorize extends Vue {
  checkedNames: string[] = [];
  key: string = '8d0ba00b';

  createKey() {
    const token = localStorage.getItem('token');
    if(!token) return alert('you are not logged in')
    console.log(this.checkedNames);
    const body = {
      types: this.checkedNames,
      key: this.key
    };
    const options = {
      headers: {
        authorization: token
      }
    };
    console.log(options);
    axios
      .post("https://lfghacks.ngrok.io/user/key", body, options)
      .then(response => {
        console.log(response);
      })
      .catch(error => {
        console.log(error);
      });
  }

  verifyAccount() {
    // Make a request for a user with a given ID
    // console.log(this.username);
    // const body = {
    //   username: this.username,
    //   password: this.password
    // };
    // axios
    //   .post<LoginResponse>("https://lfghacks.ngrok.io/login", body)
    //   .then(response => {
    //     console.log(response.data.token);
    //   })
    //   .catch(error => {
    //     console.log(error);
    //   });
  }
}
</script>




