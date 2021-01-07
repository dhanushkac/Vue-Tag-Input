<template>
  <v-chip class="ma-1" close @click:close="onClose(name)">
    {{ name }}
  </v-chip>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
    },
    onClose: {
      type: Function,
    },
  },
};
</script>

<style>
</style>