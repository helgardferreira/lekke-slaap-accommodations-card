<template>
  <div id="app">
    <!-- <h1>Search Results</h1> -->

    <div class="appointments">
      <accommodations-card
        name="Tsala Treetop Lodge"
        :detailsObject="{
          type: 'Hotel',
          price: 'R12 070 for 2 people per night',
          checkIn: '14:00 to 00:00',
          checkOut: '11:00',
          address: 'Off N2, Plettenberg Bay'
        }"
      >
        <div slot="extract">
          <strong>Tsala Treetop Lodge</strong> is a lavish celebration of the
          spirit of Africa.
        </div>
      </accommodations-card>
    </div>
  </div>
</template>

<script>
import AccommodationsCard from "./components/AccommodationsCard.vue";

export default {
  name: "app",
  components: {
    AccommodationsCard: AccommodationsCard
  }
};
</script>

<style lang="scss">
body {
  width: 100vw;
  height: 100vh;
  margin: 10px 0;
  padding: 0;
  font-family: "NTR", sans-serif;
  background: #eee;
  h1 {
    text-align: center;
  }
}

#app {
  color: #2c3e50;
}

.appointments {
  display: flex;
  justify-content: center;
  flex-flow: row wrap;
}
</style>
