<template>
  <v-app>
    <v-main>
      <v-container
        class="my-10"
      >
        <router-view />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'App',
  created() {
    this.$vuetify.theme.dark = true;
  },
};
</script>
