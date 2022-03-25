<template>
  <div>
    <v-text-field
      v-model="username"
      label="UserName"
      hide-details="auto"
    ></v-text-field>
    <v-text-field v-model="password" label="PassWord"></v-text-field>
    <v-button @click="loginMethod">Login</v-button>
  </div>
</template>
<script>
import axios from "axios";
var createGuest = require("cross-domain-storage/guest");
export default {
  name: "Login",
  data: () => ({
    username: "admin",
    password: "123456",
    token: "",
  }),

  methods: {
    setTokenToMainPage: function (token) {
      var bazStorage = createGuest("http://localhost:8081");
      bazStorage.set("token", token, function (error, data) {
        if (error) {
          console.log(error);
        } else {
          console.log(data);
          console.log("finish");
          window.location.href = "http://localhost:8081/";
        }
      });
    },
    loginMethod: async function () {
      try {
        const res = await axios.post(
          "https://file-managementt.herokuapp.com/authenticate",
          { username: this.username, password: this.password }
        );
        if (res !== null) {
          this.token = res.data.token;
          localStorage.setItem("token", this.token);
          console.log(res.data.token);
          localStorage.setItem("token", res.data.token);
          //setToken for page main
          //   setTimeout()
          this.setTokenToMainPage(res.data.token);
          //redirect
          //   window.location.href = "http://localhost:8081/";
        }
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>