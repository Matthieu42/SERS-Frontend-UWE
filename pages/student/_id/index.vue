<template>
  <div>
    <h2>{{ user.name }}</h2>
    email : {{ user.email }}
    <br>
    address : {{ user.address }}
    <StudentTab :userId="this.$route.params.id" />
  </div>
</template>

<script>
import StudentTab from "~/components/StudentTab";
import axios from "axios";

export default {
  components: {
    StudentTab
  },
  data() {
    return {
      user: {},
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
      const res = await axios.get(
        process.env.frontUrl + "/user/" + this.$route.params.id,
        config
      );
      this.user = res.data;
    } catch (error) {
      console.error(error);
    }

    try {
      const res = await axios.get(
        process.env.frontUrl + "/NoteExams/user/" + this.$route.params.id,
        config
      );
      this.modules = res.data;
    } catch (error) {
      console.error(error);
    }
  },
  computed: {
    average: (a, b, c) => {
      return (a + b + c) / 3;
    }
  }
};
</script>

<style>
</style>
