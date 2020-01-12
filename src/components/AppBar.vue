<template>
  <div class="mb-2">
    <v-app-bar color="deep-purple accent-4" dark fixed>
      <v-toolbar-title>{{ title }}</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon @click.stop="dialog = true">
        <v-icon>mdi-heart</v-icon>
      </v-btn>
    </v-app-bar>

    <v-dialog v-model="dialog" max-width="290">
      <v-card>
        <v-card-title class="headline">Klåfingriga Ewa! &#128522;</v-card-title>

        <v-card-text>Va snygg du är idag Ewa! &#128525;</v-card-text>

        <v-card-actions>
          <v-spacer></v-spacer>

          <v-btn color="green darken-1" text @click="dialog = false">Åh, Tack!</v-btn>

          <v-btn color="green darken-3" text @click="dialog = false">Jag vet</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>
<script>
export default {
  props: ["title"],
  data() {
    return {
      dialog: false
    };
  }
};
</script>