<template>
  <b-list-group>
    <StudentModule
      v-for="module in modules"
      :key="module.id"
      :userId="userId"
      :moduleId="module.id"
      :moduleName="module.title"
      :moduleAcronym="module.acronym"
    />
  </b-list-group>
</template>

<script>
import StudentModule from "~/components/StudentModule";
import axios from "axios";
export default {
  components: {
    StudentModule
  },
  props: ["userId"],
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
    console.log(process.env.frontUrl + "module/user/" + this.userId);
    try {
      const res = await axios.get(
        process.env.frontUrl + "module/user/" + this.userId,
        config
      );
      this.modules = res.data.modules;
    } catch (error) {
      console.error(error);
    }
  }
};
</script>

<style>
</style>
