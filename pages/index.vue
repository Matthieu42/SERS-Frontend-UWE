<template>
  <div id="login">
    <b-form inline>
      <label class="sr-only" for="email">Email</label>
      <b-input-group prepend="@" class="mb-2 mr-sm-2 mb-sm-0">
        <b-input id="email" placeholder="Email" v-model="email"></b-input>
      </b-input-group>
      <label class="sr-only" for="password">Password</label>
      <b-input-group class="mb-2 mr-sm-2 mb-sm-0">
        <b-input id="password" placeholder="Password" v-model="password"></b-input>
      </b-input-group>
      <b-form-checkbox class="mb-2 mr-sm-2 mb-sm-0">Remember me</b-form-checkbox>
      <b-button variant="primary">Login</b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
    }
  },
};
</script>

<style>
#login{
  padding-top: 50px;
}
</style>
