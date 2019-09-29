<template>
  <ion-card v-if="info">
    <ion-card-header>
      <ion-card-subtitle>{{ info.postcode }}</ion-card-subtitle>
      <ion-card-title>{{ info.woonplaatsnaam }}</ion-card-title>
    </ion-card-header>

    <ion-card-content>
      <ion-list>
        <ion-item>
          <ion-label>
            <strong>Provincie:</strong>
            {{ info.provincienaam }}
          </ion-label>
        </ion-item>
      </ion-list>
    </ion-card-content>
  </ion-card>
</template>

<script>
export default {
  name: "ZipInfo",
  props: ["info"]
};
</script>