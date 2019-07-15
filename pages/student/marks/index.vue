<template>
  <div>
    <h2>{{ user.username }} marks :</h2>
    <b-list-group>
      <Module
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
import Module from "~/components/Module";

export default {
  components: {
    Module
  },
  data() {
    return {
      user: {
        username: "BB",
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
      }
    };
  }
};
</script>

<style>
</style>
