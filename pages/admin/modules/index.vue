<template>
  <div>
    <b-list-group>
      <AdminModule
        id="app2"
        v-for="module in this.modules"
        :key="module.id"
        :name="module.title"
        :acronym="module.acronym"
        :moduleId="module.id"
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
      const res = await axios.get(process.env.frontUrl + "modules", config);
      this.modules = res.data;
      var res2;
      for(var i=0; i < this.modules.length; i++) {
          res2 =  await axios.get(process.env.frontUrl + "component/module/" + this.modules[i].id, config);
          this.modules[i].exams = res2.data.components;
      }
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
