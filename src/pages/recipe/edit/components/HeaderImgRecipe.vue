<template>
  <div class="header-recipe">
    <div class="flex-content">
      <v-btn icon color="success" v-on:click="onBack">
        <v-icon>arrow_back</v-icon>
      </v-btn>

      <h1>{{ recipe.name }}</h1>
    </div>

    <v-img
      v-bind:src="recipe.img"
      v-bind:lazy-src="recipe.img"
      max-height="170"
    >
    </v-img>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { FormProps } from "../formProps";

export default Vue.extend({
  name: "HeaderImgRecipeCompnet",
  props: {
    recipe: { required: true },
  } as FormProps,
  methods: {
    onBack() {
      this.$router.back();
    },
  },
});
</script>

<style scoped>
.header-recipe .v-image {
  margin: 0.5rem 0 2rem 0;
}
.flex-content {
  display: flex;
  align-items: center;
}
h1 {
  margin-left: 2rem;
}
</style>