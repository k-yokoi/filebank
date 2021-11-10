<template>
  <div id="app">
      <amplify-authenticator username-alias="email">
        <amplify-sign-up
      slot="sign-up"
      username-alias="email"
    ></amplify-sign-up>
    <amplify-sign-in slot="sign-in" username-alias="email"></amplify-sign-in>

    <HelloWorld msg="Welcome to Your Vue.js App"/>

  </amplify-authenticator>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}

</script>



<style>
body {
  margin: 0;
  background-color: white;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  text-align:center;
}
h4 {
  font-weight: 400;
  text-align: left;
}
h5 {
  font-weight: 400;
  text-align: left;
}
.pre {
  background: #f8f8f8
}
.container {
  text-align: center;
  margin-left: 30px;
}
.shifted {
  text-align: left;
}
section {
  margin-top: 30px;
}
article {
  margin-top: 30px;
}
.lineBreak {
  height: 0;
  border-bottom: 1px solid #ededed;
  margin: 1em 10%;
}
.form {
  display: inline-block;
  width: 320px;
}
inputRow {
  display: block;
  margin-top: 0.5em;
}
.input {
  width: 100%;
  font-size: 1em;
  padding: 0.5em;
  box-sizing: border-box;
  outline: none;
  border: none;
  border-bottom: 2px solid #2196F3;
}
.inputLabel {
  display: block;
  text-align: left;
}
.actionRow {
  display: flex;
  margin-top: 0.5em;
  text-align: right;
}
.action {
  font-size: 1em;
  border: none;
  outline: none;
  padding: 12px 50px;
  background-color: #ededed;
  cursor: pointer;
}
.footer {
  margin-top: 1em;
}
.footerLeft {
  float: left;
}
.footerRight {
  float: right;
}
.link {
  text-decoration: underline;
  cursor: pointer;
}
.error {
  background: orange;
  padding: 0.5em;
}
.nav {
  margin-bottom: 1em;
  display: flex;
  justify-content: space-between;
  background-color: #2196F3;
  color: #fff;
  padding: 1em;
}
.item {
  font-weight: 500;
  padding: 0 0.5em;
  cursor: pointer;
}
.nav > .greeting {
  font-weight: 500;
  color: #000;
  padding: 0 0.5em;
}
.nav > .main {
  flex-grow: 1;
  text-align: left;
}
.nav >.right {
  font-size: 0.8em;
}
.avatar {
  max-height: 150px;
}
.avatar-pic {
  max-height: 100px;
}
/* accordion */
.message {
  max-width: 500px;
  margin-left: auto;
  margin-right: auto;
}
.message-header {
  cursor: pointer;
}
.message-body   {
  padding: 0;
  max-height: 50em;
  width: 100%;
  overflow: hidden;
  transition: 0.3s ease all;
}
.is-closed .message-body {
  max-height: 0;
}
.is-primary .arrow {
  transform: rotateZ(90deg) translatex(-5px);
}
.arrow {
  display: inline-block;
}
.message-content {
  padding: 20px;
}
</style>
