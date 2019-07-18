<template>
  <b-container class="bv-example-row">
    <b-row id="app">
      <b-col>[{{ acronym }}] {{ name }}</b-col>
  </b-row>
  <b-row>
    <b-col id="app" v-if="exams.length > 0">{{ exams[0].name }}, exam coef : {{ exams[0].percentage }}</b-col>
    <b-col id="app" v-if="exams.length > 1">{{ exams[1].name }}, exam coef : {{ exams[1].percentage }}</b-col>
    <b-col id="app" v-if="exams.length > 2">{{ exams[2].name }}, exam coef : {{ exams[2].percentage }}</b-col>
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