<template>
  <div>
    <v-card class="mx-auto" max-width="600">
      <v-card-title>VÄLJ LÅNAT BELOPP OCH RÄNTA</v-card-title>
      <v-card-subtitle>Ändra genom att trycka på + och - eller dra i handtaget</v-card-subtitle>

      <v-card-text>
        <v-row>
          <v-col>Lånat belopp</v-col>
        </v-row>
        <v-row>
          <v-col class="text-left">
            <span class="display-3 font-weight-light" v-text="amt"></span>
            <span class="subheading font-weight-light mr-1">kr</span>
          </v-col>
        </v-row>

        <v-row>
          <v-col>
            <v-slider v-model="amount" max="300000" min="10000" step="1000">
              <template v-slot:prepend>
                <v-icon @click="decAmount">mdi-minus</v-icon>
              </template>

              <template v-slot:append>
                <v-icon @click="incAmount">mdi-plus</v-icon>
              </template>
            </v-slider>
          </v-col>
        </v-row>
        <v-row>
          <v-col>Ränta</v-col>
        </v-row>
        <v-row class="mb-4" justify="space-between">
          <v-col class="text-left">
            <span class="display-3 font-weight-light" v-text="interest"></span>
            <span class="subheading font-weight-light mr-1">%</span>
          </v-col>
          <v-col class="text-right">
            <p>{{ interestComment }}</p>
          </v-col>
        </v-row>

        <v-row>
          <v-col>
            <v-slider v-model="interest" min="1" max="10" :color="color" step="0.5" ticks="always">
              <template v-slot:prepend>
                <v-icon :color="color" @click="decrement">mdi-minus</v-icon>
              </template>

              <template v-slot:append>
                <v-icon :color="color" @click="increment">mdi-plus</v-icon>
              </template>
            </v-slider>
          </v-col>
        </v-row>

        <v-row style="display: none;">
          <v-col>
            <v-chip>
              Ränta per år:
              <span class="display-1">{{ amountYear }}</span>kr
            </v-chip>
          </v-col>
          <v-col>
            <v-chip>
              Ränta per månad:
              <span class="display-1">{{ amountMonth }}</span>kr
            </v-chip>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>
  </div>
</template>
<script>
export default {
  data: () => ({
    interest: 1,
    interval: null,
    amount: 10000
  }),

  computed: {
    amt() {
      return Number(this.amount).toLocaleString();
    },
    color() {
      if (this.interest < 3) return "teal darken-4";
      if (this.interest < 5) return "teal lighten-2";
      if (this.interest < 7) return "orange lighten-2";
      if (this.interest < 9) return "orange";
      if (this.interest < 11) return "deep-orange darken-1";
      return "red";
    },
    interestComment() {
      if (this.interest < 3) return "Husränta (låg)";
      if (this.interest < 5) return "Billån (normal)";
      if (this.interest < 7) return "Blancolån (dyrare)";
      if (this.interest < 9) return "Dyrt lån";
      if (this.interest < 11) return "Ockerränta, skärp dig! :)";
      return "red";
    },
    amountYear() {
      var ay = (this.amount * this.interest) / 100;
      this.$emit("amountPerYear", ay);
      return ay;
    },
    amountMonth() {
      var am = Math.round(this.amountYear / 12);
      this.$emit("amountPerMonth", am);
      return am;
    }
  },

  methods: {
    incAmount() {
      this.amount += 1000;
    },
    decAmount() {
      this.amount -= 1000;
    },
    decrement() {
      this.interest -= 0.5;
    },
    increment() {
      this.interest += 0.5;
    }
  }
};
</script>