<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <button @click="getRole">get Role from DynamoDB</button>
  <div v-if="data.status" class="role">
    {{ data.role }}
  </div>
  <!-- <HelloWorld msg="Welcome to Amplify Test Vue.js App" /> -->
</template>

<script>
import { reactive } from "vue";
// import HelloWorld from "./components/HelloWorld.vue";
import { API } from "aws-amplify";

export default {
  name: "App",
  components: {
    // HelloWorld,
  },
  setup() {
    const eventName = "test";
    let apiName = "vmware";
    let path = "/test/" + eventName;
    let myInit = {
      headers: {},
      response: true,
    };
    const data = reactive({
      status: false,
      response: false,
      role: false,
    });

    const getRole = () => {
      data.role = "Loading...";
      data.status = true;
      API.get(apiName, path, myInit)
        .then((response) => {
          console.log(response);
          if (response.data.length) {
            data.role = response.data[0].role;
            data.status = true;
          }
        })
        .catch((error) => {
          console.log(error.response);
          data.status = false;
        });
    };

    return {
      data,
      getRole,
    };
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
.role {
  margin-top: 10px;
  font-size: 20px;
  color: green;
}
</style>
