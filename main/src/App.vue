<template>
  <div id="app">
    <div>Kiểm tra token tại application</div>
  </div>
</template>

<script>
var createHost = require("cross-domain-storage/host");
var storageHost = createHost([
  {
    origin: "http://localhost:8080",
    allowedMethods: ["get", "set", "remove"],
  },
]);
console.log(storageHost);
export default {
  name: "App",
  data: () => ({
    token: "",
  }),
  mounted() {
    const token = localStorage.getItem("token");
    console.log(token);
    if (token) {
      // xu ly api
    } else {
      // redirect;
      // const link = document.createElement("a");
      // link.href = " http://localhost:8080";
      // document.body.appendChild(link);
      // link.click();
    }
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
