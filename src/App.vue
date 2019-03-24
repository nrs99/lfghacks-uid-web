<template>
  <div id="app">
    <div id="nav">
      <img class='logo' src="./assets/logo.png" >
      <router-link class='brand' to="/">Universal Identity</router-link>
      <router-link to="/">Create Account</router-link>
      <router-link to="/login">Login</router-link> 
      <router-link to="/authorize">Authorize</router-link> 
    </div>
    <router-view id='view'/>
  </div>
</template>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
  * {
    box-sizing: border-box;
  }
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
}
#nav {
  background: #85E21E;
  vertical-align: top;
  height:62px;
  margin-bottom: 20px;
  .logo {
    margin: 5px;
    height: 52px;
    width: 52px;
    float: left;
  }
  .brand {
    float: left;
    padding-left: 0;
  }
  a {
    padding:20px;
    vertical-align: top;
    display: inline-block;
    font-weight: bold;
    color: #373737;
    text-decoration: none;
    &.router-link-exact-active {
    }
  }
}
input[type='text'] {
  width: 200px;
}

button {
  width: 200px;
  border: none;
  background: #85E21E;
  color: #373737;
  padding: 15px 30px;
  font-size: 14px;
  border-radius: 3px;
  &:hover {
    background-color: darken(#85E21E, 5%);
    cursor: pointer;
  }
}
</style>
