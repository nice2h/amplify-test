<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Welcome to Amplify Test Vue.js App" />
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import { API } from "aws-amplify";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
  setup() {
    const eventName = "SampleEventName";
    let apiName = "vmware";
    let path = "/test" + eventName;
    let myInit = {
      headers: {},
      response: true,
    };

    API.get(apiName, path, myInit)
      .then((response) => {
        console.log(response);
      })
      .catch((error) => {
        console.log(error.response);
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
