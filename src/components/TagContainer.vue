<template>
  <v-container>
    <v-row class="text-center mt-12">
      <v-col md="4" offset-md="4">
        <div class="tags-input">
          <v-row>
            <v-col md="10">
              <span class="mr-2">
                <tag
                  v-for="(item, index) in tags"
                  :name="item"
                  :onClose="onClose"
                  :key="index"
                ></tag>
              </span>
              <input
                class="ma-2"
                type="text"
                placeholder="Enter your text..."
                v-model="tagName"
                @keydown.188.prevent="onAdd"
              />
            </v-col>
            <v-col md="2" class="d-flex justify-space-around" v-if="isDirty">
              <icon-button
                toolTipText="Copy all"
                icon="mdi-content-copy"
                :onClick="onCopy"
              ></icon-button>
              <icon-button
                toolTipText="Clear all"
                icon="mdi-close"
                :onClick="onClear"
              ></icon-button>
            </v-col>
          </v-row>
        </div>
        <div
          class="d-flex justify-space-between text-caption grey--text text--darken-2 mt-1"
        >
          <div>Enter a comma after each tag</div>
          <div :class="!isValid ? 'red--text' : ''">
            {{ totalCharacters }} / {{ maxLength }}
          </div>
        </div>
      </v-col>
    </v-row>
    <v-snackbar v-model="isOpen" timeout="2000">
      Copied to clipboard
      <template v-slot:action="{ attrs }">
        <v-btn color="blue" text v-bind="attrs" @click="isOpen = false">
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </v-container>
</template>

<script>
import IconButton from "./IconButton.vue";
import Tag from "./Tag.vue";

export default {
  components: { Tag, IconButton },
  data: () => ({
    tags: ["developer", "ngrx"],
    tagName: "",
    maxLength: 500,
    isOpen: false,
  }),
  methods: {
    onClose: function (tag) {
      this.tags = this.tags.filter((item) => item !== tag);
    },
    onAdd: function () {
      if (!this.isValid && !!this.tagName) {
        return;
      }

      const tagsToAdd = [...this.tagName.split(",")].map((item) => item.trim());

      this.tags = [...this.tags, ...tagsToAdd];
      this.tagName = "";
    },
    onClear: function () {
      this.tags = [];
    },
    onCopy: async function () {
      const textToCopy = this.tags.join();
      await navigator.clipboard.writeText(textToCopy);
      this.isOpen = true;
    },
  },
  computed: {
    totalCharacters: function () {
      return (
        this.tags.reduce((length, value) => value.length + length, 0) +
        this.tagName.length
      );
    },
    isValid: function () {
      return this.totalCharacters <= this.maxLength;
    },
    isDirty: function () {
      return this.tags.length > 0;
    },
  },
};
</script>

<style scoped>
.tags-input {
  display: flex;
  flex-wrap: wrap;
  background-color: #fff;
  border: 1px solid #d8d8d8;
  border-radius: 0.25rem;
  padding: 1rem;
  text-align: left;
}

input {
  outline: none;
  border: none;
}
</style>