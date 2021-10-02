<template>
  <div id="home">
    <v-col>
      <v-row id="content-row" justify="center">
        <v-col cols="6">
          <v-row>
            <v-btn @click="searchJobs = false">Profesionales</v-btn>
            <v-btn @click="searchJobs = true">Ofertas de trabajo</v-btn>
          </v-row>
          <template v-if="!searchJobs">
            <v-form v-on:submit.prevent="searchProfessionals('search')">
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
            <template>
              <v-card v-for="result of this.results" :key="result.username">
                <v-row>{{ result.username }}</v-row>
              </v-card>
            </template>
            <v-row>
              <v-btn
                v-if="this.previous"
                @click="searchProfessionals('previous')"
                >Anterior</v-btn
              >
              <v-btn v-if="this.next" @click="searchProfessionals('next')"
                >Siguiente</v-btn
              >
            </v-row>
          </template>
          <template v-if="searchJobs">
            <v-form v-on:submit.prevent="searchOffers('search')">
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
            <template>
              <v-card v-for="result of this.results" :key="result.id">
                <v-row>{{}}</v-row>
              </v-card>
            </template>
            <v-row>
              <v-btn v-if="this.previous" @click="searchOffers('previous')"
                >Anterior</v-btn
              >
              <v-btn v-if="this.next" @click="searchOffers('next')"
                >Siguiente</v-btn
              >
            </v-row>
          </template>
        </v-col>
      </v-row>
    </v-col>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import axios from "axios";
//import HelloWorld from "../components/HelloWorld.vue";

@Component({})
export default class Home extends Vue {
  professionals = "";
  offers = "";
  results = [] as any;
  previous = null as any;
  next = null as any;
  searchJobs = false;

  async searchProfessionals(action: string) {
    const body = {
      name: { term: this.professionals },
    };

    try {
      let res: any;
      if (action === "search") {
        res = await axios.post(
          `https://search.torre.co/people/_search/?[offset=0&size=10&aggregate=false]`,
          body
        );
      } else if (action === "next") {
        res = await axios.post(
          `https://search.torre.co/people/_search/?[offset=0&size=10&after=${this.next}&aggregate=false]`,
          body
        );
      } else if (action === "previous") {
        res = await axios.post(
          `https://search.torre.co/people/_search/?[offset=0&size=10&before=${this.previous}&aggregate=false]`,
          body
        );
      }

      this.results = (res.data as any).results;
      this.previous = (res.data as any).pagination.previous;
      this.next = (res.data as any).pagination.next;
    } catch (error) {
      console.log(error);
    }
  }

  async searchOffers(action: string) {
    console.log(this.offers);

    const body = {
      objective: { term: this.offers },
    };

    try {
      let res: any;
      if (action === "search") {
        res = await axios.post(
          `https://search.torre.co/opportunities/_search/?[offset=0&size=10&aggregate=false]`,
          body
        );
      }
      /*else if (action === "next") {
        res = await axios.post(
          `https://search.torre.co/people/_search/?[offset=0&size=10&after=${this.next}&aggregate=false]`,
          body
        );
      } else if (action === "previous") {
        res = await axios.post(
          `https://search.torre.co/people/_search/?[offset=0&size=10&before=${this.previous}&aggregate=false]`,
          body
        );
      }
      */

      console.log(res);
      this.results = (res.data as any).results;
      this.previous = (res.data as any).pagination.previous;
      this.next = (res.data as any).pagination.next;
    } catch (error) {
      console.log(error);
    }
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
  margin: 0;
  align-content: center;
}

#content-row {
  height: 100%;
}

.v-form {
  height: 100%;
}
</style>
