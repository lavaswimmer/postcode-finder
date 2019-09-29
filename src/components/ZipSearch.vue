<template>
  <ion-grid>
    <form @submit="onSubmit">
      <ion-col>
        <ion-item>
          <ion-label>Postcode:</ion-label>
          <ion-input
            :value="zip"
            @input="zip = $event.target.value"
            placeholder="Enter postcode"
            name="zip"
          ></ion-input>
        </ion-item>
      </ion-col>
      <ion-col>
        <ion-button type="submit" color="primary" expand="block">Find</ion-button>
      </ion-col>
    </form>
  </ion-grid>
</template>

<script>
export default {
  name: "ZipSearch",
  data() {
    return {
      zip: ""
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      // Postcode Regex
      const isValidPostCode = /^[1-9][0-9]{3}[\s]?[A-Za-z]{2}$/i.test(this.zip);
      // test for valid postcode
      if (!isValidPostCode) {
        this.showAlert();
        this.zip = "";
      } else {
        this.$emit("get-zip", this.zip);
        this.zip = "";
      }
    },
    showAlert() {
      return this.$ionic.alertController
        .create({
          header: "Enter Postcode",
          message: "Please enter a valid postcode",
          buttons: ["OK"]
        })
        .then(a => a.present());
    }
  }
};
</script>

<style>
</style>