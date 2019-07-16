<template>
  <div>
    <h2>{{ name }}</h2>
    email : {{ email }}
    average : {{ average }}
    <b-list-group>
      <StudentModule
        v-for="module in modules"
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
      id: "1",
      name: "cocodu34",
      email: "cocodu34@ibm.com",
      average: 34,
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
  }
};
</script>

<style>
</style>
