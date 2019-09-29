// 31:07
<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>ZipInfo</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ZipSearch v-on:get-zip="getZipInfo" />
      <ZipInfo v-bind:info="info" />
      <ClearInfo v-bind:info="info" v-on:clear-info="clearInfo" />
    </ion-content>
  </div>
</template>

<script>
import ZipSearch from "../components/ZipSearch";
import ZipInfo from "../components/ZipInfo";
import ClearInfo from "../components/ClearInfo";
export default {
  name: "home",
  components: {
    ZipSearch,
    ZipInfo,
    ClearInfo
  },
  data() {
    return {
      info: null
    };
  },
  methods: {
    async getZipInfo(zip) {
      const res = await fetch(
        `https://geodata.nationaalgeoregister.nl/locatieserver/free?fq=postcode:${zip}`
      );

      let data = await res.json();

      if (data.response.docs.length == 0) {
        this.showAlert();
      }

      this.info = await data.response.docs[0];
    },
    clearInfo() {
      this.info = null;
    },
    showAlert() {
      return this.$ionic.alertController
        .create({
          header: "Not valid",
          message: "Please enter a valid postcode",
          buttons: ["OK"]
        })
        .then(a => a.present());
    }
  }
};
</script>
