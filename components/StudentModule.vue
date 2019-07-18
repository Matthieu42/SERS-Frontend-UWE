<template>
  <b-list-group-item>
    <b-list-group horizontal>
      <b-list-group-item>{{ modules }}</b-list-group-item>
      <b-list-group-item >Assignment : </b-list-group-item>
      <b-list-group-item>Lab Tests : </b-list-group-item>
      <b-list-group-item>Written Exam : </b-list-group-item>
      <!-- <b-list-group-item v-if="marks.average<40">
        <b-button variant="outline-primary">Pay</b-button>
      </b-list-group-item> -->
    </b-list-group>
  </b-list-group-item>
</template>

<script>
import axios from "axios";

export default {
  props: ["userId","moduleId"],
  data() {
    return {
      modules: []
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get(process.env.frontUrl + ""+ userId, config);
      this.modules = res.data;
    } catch (error) {
      console.error(error);
    }
  },
};
</script>

<style>
</style>
