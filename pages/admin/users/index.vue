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
      striped
      hover
      :items="users"
      :fields="fields"
      :filter="filter"
      :tbody-tr-class="needResit"
    >
      <template slot="name" slot-scope="row">
        <nuxt-link :to="'/student/' + row.item.id">{{ row.value }}</nuxt-link>
      </template>

      <template slot="actions" slot-scope="row">
        <b-button
          size="sm"
          @click="row.toggleDetails"
        >{{ row.detailsShowing ? 'Hide' : 'Show' }} Modules</b-button>
      </template>
      <template slot="row-details" slot-scope="row">
        <b-card>
          <StudentTab :userId="row.item.id" />
        </b-card>
      </template>
    </b-table>
  </b-container>
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
      users: [],
      fields: [
        { key: "name", label: "Person Full name", sortable: true },
        { key: "email", label: "Email" },
        { key: "address", label: "Address" },
        { key: "actions", label: "Actions" }
      ],
      totalRows: 1,
      filter: null
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get(process.env.frontUrl + "users", config);
      this.users = res.data;
    } catch (error) {
      console.error(error);
    }
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
    //TODO
    needResit(user, type) {
      if (!user) return;
      if (user.average < 40) return "table-danger";
    }
  },
  head() {
    return {
      title: "Student List",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "List of all the students"
        }
      ]
    };
  }
};
</script>