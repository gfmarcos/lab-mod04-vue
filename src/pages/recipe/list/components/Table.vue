<template>
  <v-data-table
    :headers="header"
    :items="recipes"
    :items-per-page="5"
    class="elevation-1"
  ></v-data-table>

  <!--   <table class="table">
    <header-component />
    <tbody>
      <template v-for="recipe in recipes">
        <row-component :key="recipe.id" :recipe="recipe" />
      </template>
    </tbody>
  </table> -->
</template>

<script lang="ts">
import Vue, { PropOptions } from "vue";
import { Recipe } from "../viewModel";
import HeaderComponent from "./Header.vue";
import RowComponent from "./Row.vue";

export default Vue.extend({
  name: "TableComponent",
  data() {
    return {
      header: [
        { text: "Name", value: "name" },
        { text: "Description", value: "description" },
        { text: "Ingredients", value: "ingredients" },
      ],
    };
  },
  components: { HeaderComponent, RowComponent },
  props: {
    recipes: { required: true } as PropOptions<Recipe[]>,
    /*  recipes:{} */
  },
});
</script>

<style scoped>
.table {
  border-collapse: collapse;
  width: 100%;
}

.table tbody tr:nth-of-type(odd) {
  background-color: rgba(0, 0, 0, 0.05);
}
</style>
