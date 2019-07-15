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
      >
        <b-form-input
          id="email"
          v-model="form.email"
          type="email"
          required
          placeholder="Enter email"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Student Name:" label-for="name">
        <b-form-input id="name" v-model="form.name" required placeholder="Enter name"></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-3"
        v-model="form.password"
        label="Password:"
        label-for="password"
      >
        <b-form-input id="password" type="password" required minlength="8" new-password placeholder="Enter password" aria-describedby="password-help-block"></b-form-input>
        <b-form-text id="password-help-block">
          Your password must be  at least 8 characters long.
        </b-form-text>
      </b-form-group>

      <b-form-group id="input-group-4" label="Confirm Password:" label-for="confPassword">
        <b-form-input id="confPassword" type="password" required minlength="8" v-on:input="confPassword" placeholder="Confirm password"></b-form-input>
      </b-form-group>

      <b-form-group 
        label="Inscription to modules"
        id="input-group-5"
        v-bind:key="module.id"
        v-for="module in modules"
      >
        <input type="checkbox" :id="key" :value="key" v-model="form.modules">
        <label :for="module.title"> {{ module.title }} </label>
      </b-form-group>
 
     <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  data() {                                
    return {
      form: {
        email: "",
        name: "",
        password: "",
        modules: [],
      },
      modules: [
          {
            id: 1,
            title: "Module 1",
            acronym: "M1"
          },
          {
            id: 2,
            title: "Module 2",
            acronym: "M2"
          },
          {
            id: 3,
            title: "Module 3",
            acronym: "M3"
          },
          {
            id: 4,
            title: "Module 4",
            acronym: "M4"
          },
        ]
    };
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      alert(JSON.stringify(this.form));
    },
    confPassword: (confPassword) => {
      const password=document.getElementById("password").value
      if(password != confPassword){
        document.getElementById("confPassword").style.border="red"
      }else{
        document.getElementById("confPassword").style.border="none"
      }
    }
  }
};
</script>
<style>
  
</style>