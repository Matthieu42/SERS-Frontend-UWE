<template>
  <b-container class="bv-example-row">
  <b-row id="app">
      <b-col>[{{ acronym }}] {{ name }}</b-col>
  </b-row>
  <b-row>
    <b-col id="app" v-if="exams.length > 0">{{ exams[0].name }}, exam date : {{ exams[0].date }}</b-col>
    <b-col id="app" v-if="exams.length > 1">{{ exams[1].name }}, exam date : {{ exams[1].date }}</b-col>
    <b-col id="app" v-if="exams.length > 2">{{ exams[2].name }}, exam date : {{ exams[2].date }}</b-col>
  </b-row>
</b-container>
</template>

<script>
export default {
  props: ["name", "acronym", "exams"]
};
</script>

<style>
  #app {
    background-color: #bccef6;
    border-radius: 2px;
  }
</style>