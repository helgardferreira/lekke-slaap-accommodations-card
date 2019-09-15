<template>
  <div id="app">
    <!-- <h1>Search Results</h1> -->

    <div class="appointments">
      <accommodations-card
        name="Tsala Treetop Lodge"
        rating="4.3"
        reviewCount="1"
        :detailsMap="
          new Map([
            ['type', 'Hotel'],
            ['checkIn', '14:00 to 00:00'],
            ['checkOut', '11:00'],
            [
              'address',
              {
                text: 'Off N2, Plettenberg Bay',
                href:
                  'https://www.google.com/maps/dir//Tsala+Treetop+Lodge,+Off+N2+10km+W+Of+Plettenberg,+Plettenberg+Bay,+6600'
              }
            ]
          ])
        "
      >
        <p slot="extract">
          <strong>Tsala Treetop Lodge</strong> is a lavish celebration of the
          spirit of Africa.
        </p>
        <p slot="pricing">
          <strong>R12 070</strong> for <strong>2 people</strong> per night
        </p>
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

p {
  margin: 0;
  padding: 0;
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
