<template>
  <div id="login">
    <b-form inline @submit="onSubmit">
      <label class="sr-only" for="email">Email</label>
      <b-input-group prepend="@" class="mb-2 mr-sm-2 mb-sm-0">
        <b-input id="email" placeholder="Email" v-model="login.mail"></b-input>
      </b-input-group>
      <label class="sr-only" for="password">Password</label>
      <b-input-group class="mb-2 mr-sm-2 mb-sm-0">
        <b-input id="password" placeholder="Password" v-model="login.password"></b-input>
      </b-input-group>
      <b-form-checkbox class="mb-2 mr-sm-2 mb-sm-0">Remember me</b-form-checkbox>
      <b-button type="submit" variant="primary">Login</b-button>
    </b-form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => {
    return {
      login: {
        mail: "",
        password: ""
      }
    };
  },
  methods: {
    async onSubmit(evt) {
      evt.preventDefault();
      const config = {
        headers: {
          Accept: "application/json"
        },
        body: this.login
      };
      try {
        const res = await axios.post(process.env.frontUrl + "login", config);
        console.log(res.data);
        if(res.data.answer == "failure") {
          alert('Authentification failed')
        } else {
          alert('Authentification successed')
        }
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>

<style>
#login {
  padding-top: 50px;
}
</style>
