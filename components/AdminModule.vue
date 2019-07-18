<template>
  <b-container class="bv-example-row">
    <b-row id="app">
      <b-col>[{{ acronym }}] {{ name }}</b-col>
    </b-row>
    <b-row>
    <b-col id="app" v-if="components.length > 0">{{ components[0].name }}, exam coef : {{ components[0].percentage }}</b-col>
    <b-col id="app" v-if="components.length > 1">{{ components[1].name }}, exam coef : {{ components[1].percentage }}</b-col>
    <b-col id="app" v-if="components.length > 2">{{ components[2].name }}, exam coef : {{ components[2].percentage }}</b-col>
    </b-row>
  </b-container>
</template>

<script>
import axios from "axios";

export default {
  props: ["name", "acronym", "moduleId"],
  data() {
    return {
      components: []
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get(
        process.env.frontUrl + "/component/module/" + this.moduleId,
        config
      );
      this.components = res.data.components;
    } catch (error) {
      console.error(error);
    }
  }
};
</script>

<style>
#app {
  background-color: #bccef6;
  border-radius: 2px;
}
</style>