<template>
  <div>
    <b-form
      @submit="onSubmit"
      oninput="confPassword.setCustomValidity(confPassword.value != password.value ? 'Passwords do not match.' : "")"
      >
      <b-form-group
        id="input-group-1"
        label="Email address:"
        label-for="email"
        description="We'll never share your email with anyone else."
      >
        <b-form-input
          id="email"
          v-model="form.email"
          type="email"
          required
          placeholder="Enter email"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Your Name:" label-for="name">
        <b-form-input id="name" v-model="form.name" required placeholder="Enter name"></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-3"
        v-model="form.password"
        label="Password:"
        label-for="password"
      >
        <b-form-input id="password" type="password" required onchange="checkPassword" placeholder="Enter password"></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-4" label="Confirm Password:" label-for="confPassword">
        <b-form-input id="confPassword" type="password" required placeholder="Confirm password"></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>
    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>

  <p v-if="error">
    <ul>
      <li>{{ error }}</li>
    </ul>
  </p>

  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        error: "",
        email: "",
        name: "",
        password: ""
      }
    };
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      alert(JSON.stringify(this.form));
    },
    checkPassword: function(e) {
      var myRegex = new RegExp("?=.{8,}");
      if (!myRegex.test(password)) {
        return this.error = "Password height must be over 8";
      }
    }
  }
};
</script>