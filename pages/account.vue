<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card class="logo py-4 d-flex justify-center">
        <v-card-text>
          <div class="mb-2">
            <h1>Account</h1>
          </div>
          <div>
            <ul>
              <li>version:</li>
              <li>server:</li>
              <li>host:</li>
            </ul>
          </div>

          <hr class="mb-4 mt-4" />

          <div class="mb-2">
            <h1>AppInfo</h1>
          </div>
          <div>
            <ul>
              <li>version:</li>
              <li>server:</li>
              <li>host:</li>
            </ul>
          </div>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  layout: 'login',
};
</script>

<style scoped></style>
