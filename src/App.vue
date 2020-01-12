<template>
  <v-app>
    <app-bar title="Ewas ränteberäkning" />
    <v-content class="mt-5">
      <interest
        v-on:amountPerYear="amountPerYear = $event"
        v-on:amountPerMonth="amountPerMonth = $event"
        class="mt-5"
      />
    </v-content>
    <v-footer color="deep-purple accent-4" dense fixed>
      <v-chip>
        År:
        <span class="display-1">{{ amountPerYear }}</span>kr
      </v-chip>
      <v-spacer></v-spacer>
      <v-chip>
        Månad:
        <span class="display-1">{{ amountPerMonth }}</span>kr
      </v-chip>
    </v-footer>
  </v-app>
</template>

<script>
import Interest from "./components/Interest";
import AppBar from "./components/AppBar";

export default {
  name: "App",

  components: {
    Interest,
    AppBar
  },

  data: () => ({
    amountPerYear: 0,
    amountPerMonth: 0
  })
};
</script>
