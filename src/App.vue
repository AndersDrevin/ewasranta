<template>
  <v-app>
    <app-bar title="Ewas ränteberäkning" />
    <v-content>
      <interest class="mt-2" />
    </v-content>
    <!-- <v-footer>
      <v-chip>Per år: 20000 kr. Billigt!</v-chip>
    </v-footer>-->
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
    //
  })
};
</script>
