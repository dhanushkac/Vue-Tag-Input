<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">Tag Input</div>
    </v-app-bar>

    <v-main>
      <tag-container />
    </v-main>
  </v-app>
</template>

<script>
import TagContainer from "./components/TagContainer.vue";

export default {
  name: "App",
  components: {
    TagContainer,
  },
};
</script>
