<template>
  <div>
    <h2>{{ user.username }} marks :</h2>
    <b-list-group>
      <StudentModule
        v-for="module in user.modules"
        :key="module.id"
        :name="module.name"
        :acronym="module.acronym"
        :marks="module.marks"
      />
    </b-list-group>
  </div>
</template>

<script>
import StudentModule from "~/components/StudentModule";

export default {
  components: {
    StudentModule
  },
  data() {
    return {
      user: {
        username: "BB"
      },
      modules: [
        {
          id: 1,
          name: "Module 1",
          acronym: "MD1",
          marks: {
            average: 23,
            assignment: 50,
            lab_Tests: 12,
            written_Exam: 84
          }
        },
        {
          id: 2,
          name: "Module 2",
          acronym: "MD2",
          marks: {
            average: 99,
            assignment: 24,
            lab_Tests: 76,
            written_Exam: 2
          }
        },
        {
          id: 3,
          name: "Module 3",
          acronym: "MD3",
          marks: {
            average: 50,
            assignment: 52,
            lab_Tests: 14,
            written_Exam: 74
          }
        }
      ]
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get(process.env.frontUrl + "/modules", config);
      this.modules = res.data;
    } catch (error) {
      console.error(error);
    }

    try {
      const res = await axios.get(process.env.frontUrl + "/user", config);
      this.user = res.data;
    } catch (error) {
      console.error(error);
    }
  }
};
</script>

<style>
</style>
