<template>

  <v-form>
    <h1>{{recipe.name}}</h1>
    <!-- <img v-bind:src="recipe.img" alt="">
    <v-img v-bind:lazy-src="recipe.img" max-height="150"></v-img> -->
    <v-img
      v-bind:src="recipe.img"
      v-bind:lazy-src="recipe.img"
      max-height="150"
    >
      <template v-slot:placeholder>
        <v-row class="fill-height ma-0" align="center" justify="center">
          <v-progress-circular
            indeterminate
            color="grey lighten-5"
          ></v-progress-circular>
        </v-row>
      </template>
    </v-img>

    <v-text-field
      filled
      label="Name"
      :value="recipe.name"
      :rules="[resultRecipeError]"
      @input="(name) => onUpdateRecipe('name', name)"
      @click:append="onAddIngredient(ingredient)"
    />

    <v-text-field
      filled
      label="Ingredients"
      placeholder="Add ingredient"
      append-icon="add"
      v-model="ingredient"
      @click:append="onAddIngredient(ingredient)"
    />

    <ingredient-list-component
      :ingredients="recipe.ingredients"
      :on-remove-ingredient="onRemoveIngredient"
    />

    <v-alert
      :value="!recipeError.ingredients.succeeded"
      color="error"
      outlined
      >{{ recipeError.ingredients.message }}</v-alert
    >

    <v-textarea
      label="Description"
      filled
      placeholder="Description...."
      rows="10"
      :value="recipe.description"
      :no-resize="true"
      @input="(value) => onUpdateRecipe('description', value)"
    ></v-textarea>

    <v-alert
      :value="!recipeError.description.succeeded"
      color="error"
      outlined
      >{{ recipeError.description.message }}</v-alert
    >

    <v-btn type="button" color="success" @click.prevent="onSave">Save</v-btn>
  </v-form>

</template>

<script lang="ts">
import Vue from "vue";
import IngredientListComponent from "./IngredientList.vue";
import { FormProps } from "../formProps";

export default Vue.extend({
  name: "FormComponent",
  components: { IngredientListComponent },
  props: {
    recipe: { required: true },
    recipeError: { required: true },
    onUpdateRecipe: { required: true },
    onSave: { required: true },
    onRemoveIngredient: { required: true },
    onAddIngredient: { required: true },
  } as FormProps,
  data() {
    return {
      ingredient: "",
    };
  },
  computed: {
    resultRecipeError(): boolean | string {
      return this.recipeError.name.succeeded || this.recipeError.name.message;
    },
  },
});
</script>
