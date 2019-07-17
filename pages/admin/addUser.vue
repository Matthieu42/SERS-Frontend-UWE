<template>
  <div>
    <b-form @submit="onSubmit">
      <b-form-group id="email-group" label="Email address:" label-for="email">
        <b-form-input
          id="email"
          v-model="form.email"
          type="email"
          required
          placeholder="Enter email"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="firstname-group" label="Student First Name:" label-for="firstname">
        <b-form-input
          id="firstname"
          v-model="form.firstName"
          required
          placeholder="Enter frist name"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="lastname-group" label="Student Last Name:" label-for="lastname">
        <b-form-input id="lastname" v-model="form.lastName" required placeholder="Enter last name"></b-form-input>
      </b-form-group>

      <b-form-group id="address-group" label="Address:" label-for="address">
        <b-form-input id="address" v-model="form.address" required placeholder="Enter address"></b-form-input>
      </b-form-group>

      <b-form-group id="password-group" label="Password:" label-for="password">
        <b-form-input
          id="password"
          type="password"
          required
          minlength="8"
          new-password
          placeholder="Enter password"
          v-model="form.password"
          :state="passwordLength"
        ></b-form-input>
        <b-form-invalid-feedback
          :state="passwordLength"
        >Your password must be at least 8 characters long.</b-form-invalid-feedback>
        <b-form-valid-feedback :state="passwordLength">Looks Good.</b-form-valid-feedback>
      </b-form-group>

      <b-form-group id="confPassword-group" label="Confirm Password:" label-for="confPassword">
        <b-form-input
          id="confPassword"
          type="password"
          required
          minlength="8"
          v-model="form.confPassword"
          placeholder="Confirm password"
        ></b-form-input>
        <b-form-invalid-feedback :state="passwordMatch">Your passwords doesn't match</b-form-invalid-feedback>
        <b-form-valid-feedback :state="passwordMatch">Looks Good.</b-form-valid-feedback>
      </b-form-group>

      <b-form-group label="Inscription to modules" id="module-group">
        <b-form-checkbox-group
          id="module-group"
          v-model="form.modules"
          :options="modules"
          name="Inscription to modules"
          text-field="title"
        ></b-form-checkbox-group>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      form: {
        email: "",
        firstName: "",
        lastName: "",
        address: "",
        password: "",
        confPassword: "",
        modules: []
      },
      modules: []
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json,"
      }
    };
    try {
      const res = await axios.get(process.env.frontUrl + "/modules", config);
      this.modules = res.data;
    } catch (error) {
      console.error(error);
    }
  },
  methods: {
    onSubmit: evt => {
      evt.preventDefault();
    }
  },
  computed: {
    passwordLength: (a) => {
      return a.form.password.length > 8;
    },
    passwordMatch: (a) => {
      return (
        a.form.confPassword.length > 8 &&
        a.form.password === a.form.confPassword
      );
    }
  }
};
</script>
<style>
</style>