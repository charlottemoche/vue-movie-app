<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>Signup</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <label for="name">Name:</label>
      <input type="text" id="name" name="name" value="" v-model="name" />
      <br />
      <br />
      <label for="email">Email:</label>
      <input type="text" id="email" name="email" value="" v-model="email" />
      <br />
      <br />
      <label for="password">Password:</label>
      <input type="password" id="password" name="password" value="" v-model="password" />
      <br />
      <br />
      <label for="password-confirmation">Password confirmation:</label>
      <input
        type="password"
        id="password-confirmation"
        name="password-confirmation"
        value=""
        v-model="passwordConfirmation"
      />
      <br />
      <br />
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      name: "",
      email: "",
      password: "",
      passwordConfirmation: "",
      errors: [],
    };
  },
  methods: {
    submit: function() {
      var params = {
        name: this.name,
        email: this.email,
        password: this.password,
        password_confirmation: this.passwordConfirmation,
      };
      axios
        .post("/api/users", params)
        .then(response => {
          console.log(response.data);
          this.$router.push("/login");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
