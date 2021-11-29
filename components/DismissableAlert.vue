<template>
  <div>
    <v-alert
      v-model="alert"
      dismissible
      border="left"
      type="info"
      elevation="2"
      colored-border
    >
    </v-alert>
    {{ message }}
  </div>
</template>

<script>
export default {
  props: {
    alert: { type: Boolean, default: false },
    type: { type: String, default: 'info' },
    message: { type: String, default: '' },
  },
};
</script>
