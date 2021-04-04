<template>
  <v-card
    v-if="resource"
  >
    <v-card-text
      class="pa-3"
    >
      <v-row
        justify="space-between"
      >
        <v-col
          cols="4"
          class="body-1 text-center px-2 py-0"
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
          cols="4"
          class="body-1 text-center px-2 py-0"
        >
          <v-list
            two-line
          >
            <v-list-item
              :ripple="false"
              :inactive="true"
            >
              <v-list-item-content
                class="text-center"
              >
                <span
                  v-text="`${resource.name}`"
                />
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-col>
        <v-divider
          vertical
        />
        <v-col
          cols="4"
          class="body-1 text-center px-2 py-0"
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
