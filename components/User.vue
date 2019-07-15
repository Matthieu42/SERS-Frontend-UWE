<template>
  <b-list-group-item>
    <b-list-group horizontal>
      <b-list-group-item>[{{ acronym }}] {{ name }} : {{ marks.average }}</b-list-group-item>
      <b-list-group-item>Assignment : {{ marks.assignment }}</b-list-group-item>
      <b-list-group-item>Lab Tests : {{ marks.lab_Tests }}</b-list-group-item>
      <b-list-group-item>Written Exam : {{ marks.written_Exam }}</b-list-group-item>
      <b-list-group-item v-if="marks.average<40">
          <b-button variant="outline-primary">Pay</b-button>
      </b-list-group-item>
    </b-list-group>
  </b-list-group-item>
</template>

<script>
export default {
  props: ["name", "acronym", "marks"]
};
</script>

<style>
</style>
