<template>
  <v-app>
    <v-main>  
      <Page/>
    </v-main>
  </v-app>
</template>

<script>
import Page from './views/Page';

export default {
  name: 'App',

  components: {
    Page,
  },

  data: () => ({
    //
  }),
};
</script>
