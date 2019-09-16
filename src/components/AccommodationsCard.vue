<template>
  <div class="accommodation-card">
    <!-- Add both click listener as well as keyboard listener for accessibility standards -->
    <header @click="goTo(lekkeLink)" @keyup.enter="goTo(lekkeLink)">
      <h4 class="header-text">
        <a :href="lekkeLink">
          {{ name }}
        </a>
      </h4>
      <div
        class="header-img"
        :style="{
          backgroundImage: `url(${bkgImg})`
        }"
      />
    </header>
    <div class="meta">
      <div class="rating">
        <star-icon
          v-for="(num, index) in 5"
          :key="`${index}-filled`"
          :primaryColor="starColors[index]"
          size="14"
          class="star"
        />

        &nbsp; ({{ reviewCount }})
      </div>
      <h5 class="premium-text">
        PREMIUM
      </h5>
    </div>
    <div class="extract">
      <slot name="extract">
        Book your accommodation now at <strong>{{ name }}</strong>
      </slot>
    </div>
    <div class="pricing">
      <slot name="pricing">
        Get a quote for <strong>{{ name }}</strong></slot
      >
    </div>
    <!-- Add both click listener as well as keyboard listener for accessibility standards -->
    <button
      class="primary-btn"
      v-if="!showDetails"
      @click="mapDetails"
      @keyup.enter="mapDetails"
    >
      View More
    </button>
    <app-details-list :details="details" />
  </div>
</template>

<script>
import Star from "../components/icons/Star";
import DetailsList from "../components/DetailsList";

export default {
  name: "AccommodationsCard",
  props: {
    name: {
      type: String
    },
    rating: {
      type: Number,
      default: 0
    },
    reviewCount: {
      type: Number,
      default: 0
    },
    lekkeLink: {
      type: String
    },
    detailsMap: {
      type: Map
    }
  },
  components: {
    starIcon: Star,
    appDetailsList: DetailsList
  },
  data() {
    return {
      bkgImg: require("../assets/tsala-treetop-lodge-1.jpeg"),
      details: [],
      showDetails: false,
      starColors: []
    };
  },
  mounted() {
    this.fillStars();
  },
  methods: {
    mapDetails() {
      this.showDetails = true;
      let count = 0;
      for (const [key, value] of this.detailsMap) {
        setTimeout(() => {
          if (key === "checkIn") this.details.push(`Check in from ${value}`);
          else if (key === "checkOut")
            this.details.push(`Check out at ${value}`);
          else this.details.push(value);
        }, count * 200);
        count++;
      }
    },
    fillStars() {
      for (let i = 0; i < Math.floor(this.rating); i++) {
        setTimeout(() => {
          this.starColors.push("#e9b949");
        }, 1 + i * 200);
      }
    },
    goTo(address) {
      window.location.assign(address);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "../assets/css/variables.scss";

.primary-btn {
  margin: 12px;
  display: block;
  font-size: 14px;
  font-weight: bold;
  background: $primary-color;
  color: $neutral-color-white;
  border: 0;
  padding: 8px;
  border-radius: 4px;
  outline: 0;
  cursor: pointer;
}

.primary-btn:hover,
.primary-btn:active,
.primary-btn:focus {
  background: $primary-color-dark;
  border: 2px solid $neutral-color-dark-grey;
}

.accommodation-card {
  width: 300px;
  border: 1px solid $neutral-color-light-grey;
  overflow: hidden;
  border-radius: 8px;
  background: $neutral-color-white;
  header {
    cursor: pointer;
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
  font-size: 16px;
  background: rgba(0, 0, 0, 0.7);
  max-width: calc(80% - 28px);
  text-align: left;
  position: absolute;
  top: 12%;
  z-index: 1000;
  overflow: hidden;
  border-radius: 0 50px 50px 0;
  margin: 0;
  padding: 14px;
  color: $neutral-color-white;
  a {
    color: $neutral-color-white;
    text-decoration: none;
  }
  a:visited {
    color: $neutral-color-white;
  }
  a:hover,
  a:active,
  a:focus {
    color: $neutral-color-white;
    text-decoration: underline;
  }
}

.meta {
  margin: 12px;
  display: flex;
  justify-content: space-between;

  .rating {
    font-size: 14px;
    padding: 0;
    display: flex;
    .star {
      display: block;
    }
  }

  .premium-text {
    font-size: 14px;
    margin: 0;
    display: inline-block;
    color: $accent-color-premium;
    font-weight: bold;
    transition: background 1s;
  }
}

.extract {
  color: $neutral-color-dark-grey;
  font-size: 18px;
  margin: 12px;
  padding: 0;
}

.pricing {
  color: $neutral-color-dark-grey;
  font-size: 14px;
  margin: 12px;
  padding: 0;
}
</style>
