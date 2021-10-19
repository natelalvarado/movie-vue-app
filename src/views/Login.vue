<template>
  <div class="login">
    <form v-on:submit.prevent="submit()">
      <h1 style="color: white; background-color: #e75b16; font-family: georgia">
        Login
      </h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div style="font-family: georgia">
        <label>Email:</label>
        <input type="email" v-model="newSessionParams.email" />
      </div>
      <div style="font-family: georgia">
        <label>Password:</label>
        <input type="password" v-model="newSessionParams.password" />
      </div>
      <input
        style="
          background-color: #ddd;
          border: none;
          color: black;
          padding: 10px 20px;
          text-align: center;
          text-decoration: none;
          display: inline-block;
          margin: 4px 2px;
          cursor: pointer;
          border-radius: 16px;
        "
        type="submit"
        value="Submit"
      />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newSessionParams: {},
      errors: [],
    };
  },
  methods: {
    submit: function () {
      axios
        .post("/sessions", this.newSessionParams)
        .then((response) => {
          axios.defaults.headers.common["Authorization"] =
            "Bearer " + response.data.jwt;
          localStorage.setItem("jwt", response.data.jwt);
          this.$router.push("/");
        })
        .catch((error) => {
          console.log(error.response);
          this.errors = ["Invalid email or password."];
          this.newSessionParams = {};
        });
    },
  },
};
</script>
