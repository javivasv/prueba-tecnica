<template>
  <div id="home">
    <v-col>
      <v-row justify="center">
        <v-col cols="6">
          <v-form ref="loginForm" v-on:submit.prevent="searchProfessionals()">
            <v-row justify="center">
              <v-text-field
                label="Buscar profesionales"
                v-model="professionals"
              ></v-text-field>
            </v-row>
            <v-row justify="center">
              <v-btn type="submit">Buscar</v-btn>
            </v-row>
          </v-form>
        </v-col>
      </v-row>
      <v-row justify="center">
        <v-col cols="6">
          <v-form ref="loginForm" v-on:submit.prevent="searchOffers()">
            <v-row justify="center">
              <v-text-field
                label="Buscar ofertas de trabajo"
                v-model="offers"
              ></v-text-field>
            </v-row>
            <v-row justify="center">
              <v-btn type="submit">Buscar</v-btn>
            </v-row>
          </v-form>
        </v-col>
      </v-row>
    </v-col>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
//import HelloWorld from "../components/HelloWorld.vue";

@Component({})
export default class Home extends Vue {
  professionals = "";
  offers = "";

  searchProfessionals() {
    console.log(this.professionals);
  }

  searchOffers() {
    console.log(this.offers);
  }
}

/*
export default Vue.extend({
  name: "Home",

  components: {
    HelloWorld,
  },
});
*/
</script>

<style lang="scss" scoped>
#home {
  width: 100%;
  height: 100%;
}

.col {
  height: 100%;
}

.row {
  width: 100%;
  height: 50%;
  margin: 0;
  align-content: center;
}

.v-form {
  height: 100%;
}
</style>
