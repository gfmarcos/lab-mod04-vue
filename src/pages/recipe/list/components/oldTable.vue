<template>
  <v-data-table
    :headers="header"
    :items="recipes"
    :items-per-page="3"
    class="elevation-1"
  >
    <template v-slot:item.actions="{ item }">
            <v-btn text icon :to="routeEdit">
        <v-icon>edit</v-icon>
      </v-btn>
    </template>
  </v-data-table>

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
import { baseRoutes } from "../../../../router";

export default Vue.extend({
  name: "TableComponent",
  data() {
    return {
      header: [
        { text: "Name", value: "name" },
        { text: "Description", value: "description" },
        { text: "Actions", value: "actions", sortable: false },
      ],
    };
  },
  components: { HeaderComponent, RowComponent },
  props: {
    recipes: { required: true } as PropOptions<Recipe[]>,
    /*  recipes:{} */
  },
  computed: {
    routeEdit(): string {
      return `${baseRoutes.recipe}/1`;
    },
  },
  methods: {
    hola() {
      console.log("HHHHHHHHH");
    },
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
