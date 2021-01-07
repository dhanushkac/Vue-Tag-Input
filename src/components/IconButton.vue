<template>
  <v-tooltip bottom>
    <template v-slot:activator="{ on, attrs }">
      <v-btn
        icon
        x-small
        color="grey"
        v-bind="attrs"
        v-on="on"
        @click="onClick"
      >
        <v-icon>{{ icon }}</v-icon>
      </v-btn>
    </template>
    <span>{{ toolTipText }}</span>
  </v-tooltip>
</template>

<script>
export default {
  props: {
    toolTipText: {
      type: String,
    },
    icon: {
      type: String,
    },
    onClick: {
      type: Function,
    },
  },
};
</script>