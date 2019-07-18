<template>
  <div>
    <b-form @submit="onSubmit">
      <b-form-group id="email-group" label="Email address:" label-for="email">
        <b-form-input
          id="email"
          v-model="form.mail"
          type="email"
          required
          placeholder="Enter email"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="name-group" label="Student Name:" label-for="name">
        <b-form-input id="name" v-model="form.name" required placeholder="Enter name"></b-form-input>
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
        <b-form-checkbox
          v-for="module in modules"
          v-model="form.modules"
          :key="module.id"
          :value="module.id"
          inline
        >{{ module.title }}</b-form-checkbox>
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
        mail: "",
        name: "",
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
    async onSubmit(evt) {
      console.log(this.form.modules);
      evt.preventDefault();
      const config = {
        headers: {
          Accept: "application/json"
        },
        body: this.form
      };
      try {
        const res = await axios.post(
          process.env.frontUrl + "/signup",
          this.form,
          config
        );
        var resData = res.data;
        console.log(resData);
        if (resData.answer == "failure") {
          alert("inscription failed");
        } else {
          alert("Success");
        }
      } catch (error) {
        console.error(error);
      }
    }
  },
  computed: {
    passwordLength: a => {
      return a.form.password.length > 8;
    },
    passwordMatch: a => {
      return (
        a.form.confPassword.length > 8 &&
        a.form.password === a.form.confPassword
      );
    }
  },
  head() {
    return {
      title: "New Student",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Add a student to the system"
        }
      ]
    };
  }
};
</script>
<style>
</style>