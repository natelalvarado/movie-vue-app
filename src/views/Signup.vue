<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1 style="color: white; background-color: #f25555; font-family: georgia">
        Signup
      </h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label style="font-family: georgia">Name:</label>
        <input type="text" v-model="newUserParams.name" />
      </div>
      <div>
        <label style="font-family: georgia">Email:</label>
        <input type="email" v-model="newUserParams.email" />
      </div>
      <div>
        <label style="font-family: georgia">Password:</label>
        <input type="password" v-model="newUserParams.password" />
      </div>
      <div>
        <label style="font-family: georgia">Password confirmation:</label>
        <input type="password" v-model="newUserParams.password_confirmation" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newUserParams: {},
      errors: [],
    };
  },
  methods: {
    submit: function () {
      axios
        .post("/users", this.newUserParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/login");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
