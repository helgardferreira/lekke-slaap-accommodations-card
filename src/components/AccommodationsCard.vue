<template>
  <div class="accommodation-card">
    <header>
      <h4 class="header-text">
        Tsala Treetop Lodge
      </h4>
      <div
        class="header-img"
        :style="{
          backgroundImage: `url(${bkgImg})`
        }"
      ></div>
    </header>
    <!-- <aside class="premium-banner">
      Premium
    </aside> -->
    <div class="extract">
      <slot name="extract">
        Book your accommodation now at <strong>{{ name }}</strong>
      </slot>
    </div>
    <div v-if="showDetails" class="details">
      <ul>
        <transition-group name="slide">
          <li
            v-for="(detail, index) in details"
            :key="`${index}-${detail}`"
            :class="{
              'detail-top': index === 0,
              'detail-middle': index > 0 && index < details.length - 1,
              'detail-bottom': index === details.length - 1
            }"
          >
            {{ detail }}
          </li>
        </transition-group>
      </ul>
    </div>
    <button v-else @click="mapDetails">View More</button>
  </div>
</template>

<script>
export default {
  name: "AccommodationsCard",
  props: ["name", "detailsObject"],
  data() {
    return {
      bkgImg: require("../assets/tsala-treetop-lodge-1.jpeg"),
      details: [],
      showDetails: false
    };
  },
  methods: {
    mapDetails() {
      this.showDetails = true;
      for (const [index, [key, value]] of Object.entries(
        this.detailsObject
      ).entries()) {
        setTimeout(() => {
          if (key === "checkIn") this.details.push(`Check in from ${value}`);
          else if (key === "checkOut")
            this.details.push(`Check out at ${value}`);
          else this.details.push(value);
        }, index * 200);
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
button {
  margin: 0 10px 0 0;
  font-size: 0.8rem;
  background: #f9703e;
  color: white;
  border: 0;
  padding: 5px 10px;
  border-radius: 0 4px 0 0;
  outline: 0;
  cursor: pointer;
}

button:hover {
  background: #de3a11;
}

.accommodation-card {
  width: 300px;
  overflow: hidden;
  border-radius: 10px;
  background: #1f2933;
  header {
    position: relative;
  }
}

main {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.header-img {
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  height: 200px;
}

.header-text {
  background: rgba(0, 0, 0, 0.7);
  max-width: calc(90% - 70px);
  text-align: left;
  position: absolute;
  top: 15%;
  z-index: 1000;
  overflow: hidden;
  border-radius: 0 50px 50px 0;
  // transition: 0.3s opacity ease-in;
  margin: 0;
  padding: 20px 35px;
  color: white;
}

.premium-banner {
  text-align: right;
  clip-path: polygon(0% 0%, 100% 0, 100% 100%, 10% 100%);
  border-radius: 0 0 0 100px;
  background: #e9b949;
  margin: 0;
  padding: 10px;
  color: #1f2933;
}

.extract {
  color: white;
  font-size: 0.8rem;
  background: #f9703e;
  border-radius: 5px;
  margin: 10px;
  padding: 10px;
}

.details {
  color: white;
  font-size: 1rem;
  margin: 10px;
  ul {
    margin: 0;
    padding: 0;
    li {
      background: #f9703e;
      list-style-type: none;
      margin: 0;
      padding: 2px 0 2px 10px;
    }
  }
}

.detail-top {
  border-radius: 5px 5px 0 0;
  border-bottom: 2px solid #ffe8d9;
}

.detail-middle {
  border-radius: 0;
  border-bottom: 2px solid #ffe8d9;
}

.detail-bottom {
  border-radius: 0 0 5px 5px;
}

.slide-enter-active,
.slide-leave-active {
  transition: transform 0.3s ease-out;
}

.slide-enter,
.slide-leave-to {
  transform: translateX(-100px);
}
</style>
