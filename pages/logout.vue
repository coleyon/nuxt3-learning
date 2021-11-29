<template>
  <v-row justify="center" align="center">
    <v-col class="text-center">
      <p>Logging out..</p>
    </v-col>
  </v-row>
</template>
<script>
export default {
  middleware: ['auth'],
  mounted() {
    console.debug('Entire finish');
    try {
      console.debug('logging out.... ');
      this.$auth.logout();
      console.debug('loggedin? ', this.$auth.loggedIn);
      this.$router.push('/info');
    } catch (err) {
      console.error(err);
    }
  },
};
</script>

<style scoped></style>
