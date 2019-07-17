<template>
  <div>
    <b-list-group>
      <AdminModule id="app2"
        v-for="module in user.modules"
        :key="module.id"
        :name="module.name"
        :acronym="module.acronym"
        :exams="module.exams"
      />
    </b-list-group>
  </div>
</template>

<script>
import AdminModule from "~/components/AdminModule";

export default {
  components: {
    AdminModule
  },
  data() {
    return {
      bordered: true,
      striped: true,
      user: {
        username: "BB",
        modules: [
          {
            id: 1,
            name: "Module 1",
            acronym: "MD1",
            exams: 
              [
                {
                  name: "Test1",
                  date: "15/07/2019"
                },
                {
                  name: "Test2",
                  date: "15/07/2019"
                },
                {
                  name: "Test3",
                  date: "15/07/2019"
                },
              ]
          },
          {
            id: 1,
            name: "Module 2",
            acronym: "MD1",
            exams: 
              [
                {
                  name: "Test1",
                  date: "15/07/2019"
                },
                {
                  name: "Test2",
                  date: "15/07/2019"
                }
              ]
          }
          
        ]
      }
    }
  }
}

</script>

<style>

  #app2 {
    margin-top: 20px;
  }

</style>
