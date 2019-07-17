<template>
  <div>
    <template slot="name" slot-scope="row">
      <nuxt-link :to="'/student/' + row.value.id">{{ row.value }}</nuxt-link>
    </template>

    <template slot="email" slot-scope="row">{{ row.value }}</template>

    <template slot="address" slot-scope="row">{{ row.value }}</template>

    <template slot="actions" slot-scope="row">
      <b-button
        size="sm"
        @click="row.toggleDetails"
      >{{ row.detailsShowing ? 'Hide' : 'Show' }} Modules</b-button>
    </template>
    <template slot="row-details" slot-scope="row">
      <b-card>
        <b-list-group>
          <StudentModule
            v-for="module in row.item.modules"
            :key="module.id"
            :name="module.name"
            :acronym="module.acronym"
            :marks="module.marks"
          />
        </b-list-group>
      </b-card>
    </template>
  </div>
</template>

<script>
export default {};
</script>

<style>
</style>
