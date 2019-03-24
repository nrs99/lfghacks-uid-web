<template>
  <div id="example-3">
    <h3>What personal data would you like to share with the provider?</h3>
    <input type="checkbox" id="Age" value="Age" v-model="checkedNames">
    <label for="Age">Age</label>
    <input type="checkbox" id="Over21" value="Over21" v-model="checkedNames">
    <label for="Over21">Over21</label>
    <input type="checkbox" id="SSN" value="SSN" v-model="checkedNames">
    <label for="SSN">SSN </label>
    <input type="checkbox" id="CardPayment" value="CardPayment" v-model="checkedNames">
    <label for="CardPayment">CardPayment</label>

    <br>
    <span>You want to verify: {{ checkedNames }}</span>
  </div>
</template>
<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import axios from "axios";


@Component
export default class Authorize extends Vue {
  checkedNames: string[] = [];

  passSelectValues() {
    console.log(this.checkedNames);
    const body = {
      types: this.checkedNames
    };
    axios
      .post("https://lfghacks.ngrok.io/user/key", body)
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
      })
      .catch(error => {
        console.log(error);
      });
  }

}

</script>




