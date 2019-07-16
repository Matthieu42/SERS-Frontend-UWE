<template>
  <b-container fluid>
    <!-- User Interface controls -->
    <b-row>
      <b-col md="6" class="my-1">
        <b-form-group label-cols-sm="3" label="Filter" class="mb-0">
          <b-input-group>
            <b-form-input v-model="filter" placeholder="Type to Search"></b-form-input>
            <b-input-group-append>
              <b-button :disabled="!filter" @click="filter = ''">Clear</b-button>
            </b-input-group-append>
          </b-input-group>
        </b-form-group>
      </b-col>
    </b-row>

    <!-- Main table element -->
    <b-table
      show-empty
      stacked="md"
      :items="items"
      :fields="fields"
      :filter="filter"
      :tbody-tr-class="needResit"
    >
      <template slot="name" slot-scope="row"><nuxt-link :to="'/student/' + row.value.id">{{ row.value }}</nuxt-link></template>

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
    </b-table>
  </b-container>
</template>

<script>
import StudentModule from "~/components/StudentModule";

export default {
  components: {
    StudentModule
  },
  data() {
    return {
      items: [
        {
          id: 1,
          average: 40,
          name: "Corentin Grard",
          address: "regokper",
          email: "dgkorg@rdgok.com",
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
        },
        {
          id: 2,
          average: 21,
          name: "Jean Michel",
          address: "regokper",
          email: "dgkorg@rdgok.com"
        },
        {
          id: 3,
          average: 9,
          name: "Jessy Chevanas",
          address: "regokper",
          email: "dgkorg@rdgok.com"
        },
        {
          id: 4,
          average: 89,
          name: "Matthieu Tinnes",
          address: "regokper",
          email: "dgkorg@rdgok.com"
        },
        {
          id: 5,
          average: 38,
          name: "SEOIJGSG",
          address: "regokper",
          email: "dgkorg@rdgok.com"
        },
        {
          id: 6,
          average: 27,
          name: "IOJDG",
          address: "regokper",
          email: "dgkorg@rdgok.com"
        },
        {
          id: 7,
          average: 40,
          name: "RIOJS",
          address: "regokper",
          email: "dgkorg@rdgok.com"
        },
        {
          id: 8,
          average: 87,
          name: "dpkorg",
          address: "regokper",
          email: "dgkorg@rdgok.com"
        },
        {
          id: 9,
          average: 26,
          name: "fntkomg",
          address: "regokper",
          email: "dgkorg@rdgok.com"
        },
        {
          id: 10,
          average: 22,
          name: "rhtopk",
          address: "regokper",
          email: "dgkorg@rdgok.com"
        },
        {
          id: 11,
          average: 38,
          name: "dfbko",
          address: "regokper",
          email: "dgkorg@rdgok.com"
        },
        {
          id: 12,
          average: 29,
          name: "kpsgrop",
          address: "regokper",
          email: "dgkorg@rdgok.com"
        }
      ],
      fields: [
        { key: "name", label: "Person Full name", sortable: true },
        { key: "email", label: "Email" },
        { key: "address", label: "Address" },
        {
          key: "average",
          label: "Average",
          sortable: true,
          class: "text-center"
        },
        { key: "actions", label: "Actions" }
      ],
      totalRows: 1,
      filter: null
    };
  },
  computed: {
    sortOptions() {
      // Create an options list from our fields
      return this.fields
        .filter(f => f.sortable)
        .map(f => {
          return { text: f.label, value: f.key };
        });
    }
  },
  methods: {
    needResit(item, type) {
      if (!item) return;
      if (item.average < 40) return "table-danger";
    }
  }
};
</script>