<template>
  <div id="offer">
    <v-row id="content-row" justify="center">
      <v-col cols="6">
        <v-row>
          <v-card v-if="gotOffer"> </v-card>
        </v-row>
      </v-col>
    </v-row>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import axios from "axios";

@Component({})
export default class Offer extends Vue {
  offer: any;
  gotOffer = false;

  async created() {
    const id = this.$route.params.id;

    try {
      const res = await axios.get(`https://torre.co/api/opportunities/${id}`);
      this.offer = res.data;
      this.gotOffer = true;
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
