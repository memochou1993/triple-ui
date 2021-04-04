<template>
  <v-card
    v-if="resource"
  >
    <v-card-title
      class="headline indigo white--text"
    >
      <v-row
        class="text-center"
      >
        <v-col
          cols="12"
        >
          <span
            v-text="resource.name"
          />
        </v-col>
      </v-row>
    </v-card-title>
    <v-card-text
      class="pa-4"
    >
      <v-row
        justify="space-between"
      >
        <v-col
          cols="6"
          class="body-1 text-center py-0"
        >
          <StatementList
            :statements="subjectStatements"
            :onClick="fetchResource"
          />
        </v-col>
        <v-divider
          vertical
        />
        <v-col
          cols="6"
          class="body-1 text-center py-0"
        >
          <StatementList
            :statements="objectStatements"
            :onClick="fetchResource"
          />
        </v-col>
      </v-row>
    </v-card-text>
  </v-card>
</template>

<script>
import axios from 'axios';
import StatementList from '@/components/StatementList';

axios.defaults.headers.common.Authorization = `Bearer ${process.env.VUE_APP_API_TOKEN}`;

export default {
  name: 'Home',
  components: {
    StatementList,
  },
  data: () => ({
    resource: null,
  }),
  computed: {
    subjectStatements() {
      return this.resource?.subject_statements;
    },
    objectStatements() {
      return this.resource?.object_statements;
    },
  },
  created() {
    this.fetchResource(3); // FIXME
  },
  methods: {
    setResource(resource) {
      this.resource = resource;
    },
    fetchResource(id) {
      axios.get(`http://127.0.0.1:8000/api/user/resources/${id}`)
        .then(({ data }) => {
          this.setResource(data.data);
        });
    },
  },
};
</script>
