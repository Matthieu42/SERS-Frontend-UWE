<template>
  <div>
    <b-list-group>
      <AdminModule
        id="app2"
        v-for="module in this.modules"
        :key="module.id"
        :name="module.title"
        :acronym="module.acronym"
        :exams="[]"
      />
    </b-list-group>
  </div>
</template>

<script>
import AdminModule from "~/components/AdminModule";
import axios from "axios";
export default {
  components: {
    AdminModule
  },
  data() {
    return {
      bordered: true,
      modules: null,
      striped: true
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      console.log(process.env.frontUrl);
      const res = await axios.get(process.env.frontUrl + "/modules", config);
      this.modules = res.data;
      console.log(this.modules);
    } catch (error) {
      console.error(error);
    }
  },
  head() {
    return {
      title: "Modules List",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "List of all the modules"
        }
      ]
    };
  }
};
</script>

<style>
#app2 {
  margin-top: 20px;
}
</style>
