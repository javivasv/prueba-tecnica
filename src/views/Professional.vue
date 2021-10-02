<template>
  <div id="professional">
    <v-row id="content-row" justify="center">
      <v-col cols="6">
        <v-row>
          <v-card v-if="gotProfessional">
            <v-row>
              <v-avatar size="150" tile>
                <v-img :src="professional.person.picture"> </v-img>
              </v-avatar>
            </v-row>
            <h3>Nombre</h3>
            <v-row>{{ professional.person.name }}</v-row>
            <h3>Intereses</h3>
            <v-row
              v-for="interest of professional.interests"
              :key="interest.code"
              >{{ interest.name }}</v-row
            >
          </v-card>
        </v-row>
      </v-col>
    </v-row>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import axios from "axios";

@Component({})
export default class Professional extends Vue {
  professional: any;
  gotProfessional = false;

  async created() {
    const username = this.$route.params.username;

    try {
      const res = await axios.get(`https://torre.bio/api/bios/${username}`);
      this.professional = res.data;
      this.gotProfessional = true;
    } catch (error) {
      console.log(error);
    }
  }
}
</script>

<style lang="scss" scoped>
#professional {
  width: 100%;
  height: 100%;
}

.col {
  height: 100%;
}

.row {
  height: 100%;
  width: 100%;
  margin: 0;
  align-content: center;
}

#content-row {
  height: 100%;
}

.v-card {
  width: 100%;
  height: fit-content;
}
</style>
