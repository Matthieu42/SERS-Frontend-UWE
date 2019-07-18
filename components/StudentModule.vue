<template>
  <b-list-group-item>
    <b-list-group horizontal>
      <b-list-group-item>[{{ moduleAcronym }}] {{ moduleName }} : {{ average }}</b-list-group-item>
      <b-list-group-item
        v-for="component in components"
        :key="component.id"
      >{{ component.name }} ({{ component.percentage }}%) : {{ component.note }}</b-list-group-item>
      <b-list-group-item v-if="average<40">
        <b-button variant="outline-primary">Pay</b-button>
      </b-list-group-item>
    </b-list-group>
  </b-list-group-item>
</template>

<script>
import axios from "axios";

export default {
  props: ["userId", "moduleId", "moduleName", "moduleAcronym"],
  data() {
    return {
      components: [],
      average: 0
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
        process.env.frontUrl +
          "NoteExams/module/user/" +
          this.userId +
          "/" +
          this.moduleId,
        config
      );
      this.components = res.data;
    } catch (error) {
      console.error(error);
    }
    this.components.forEach(component => {
      this.average += component.note * (component.percentage / 100);
    });
  }
};
</script>

<style>
</style>
