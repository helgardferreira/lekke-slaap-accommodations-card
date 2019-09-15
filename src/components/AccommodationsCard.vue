<template>
  <div class="accommodation-card">
    <header
      @click="
        goTo('https://www.lekkeslaap.co.za/akkommodasie/tsala-treetop-lodge')
      "
    >
      <h4 class="header-text">
        {{ name }}
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
    <button class="primary-btn" v-if="!showDetails" @click="mapDetails">
      View More
    </button>
    <div class="details">
      <transition-group name="slide">
        <p
          v-for="(detail, index) in details"
          :key="`${detail}`"
          :class="{
            'detail-top': index === 0,
            'detail-middle': index > 0 && index < details.length - 1,
            'detail-bottom': index === details.length - 1
          }"
        >
          <a
            v-if="detail.href"
            :href="detail.href"
            target="_blank"
            rel="noopener noreferrer"
          >
            {{ detail.text }}
          </a>
          <template v-else>
            {{ detail }}
          </template>
        </p>
      </transition-group>
    </div>
  </div>
</template>

<script>
import Star from "../components/icons/Star";

export default {
  name: "AccommodationsCard",
  props: {
    name: {},
    detailsObject: {},
    rating: {
      default: 0
    },
    reviewCount: {
      default: 0
    }
  },
  components: {
    starIcon: Star
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
.primary-btn {
  margin: 12px;
  display: block;
  font-size: 14px;
  font-weight: bold;
  background: #f9703e;
  /* background: #323f4b; */
  color: #f5f7fa;
  border: 0;
  padding: 8px;
  border-radius: 4px;
  outline: 0;
  cursor: pointer;
}

.primary-btn:hover {
  background: #f35627;
  /* background: #1f2933; */
}

.accommodation-card {
  width: 300px;
  border: 1px solid #e4e7eb;
  overflow: hidden;
  border-radius: 8px;
  background: #f5f7fa;
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
  color: #f5f7fa;
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
    color: #e9b949;
    font-weight: bold;
    transition: background 1s;
  }
}

.extract {
  color: #1f2933;
  font-size: 18px;
  margin: 12px;
  padding: 0;
}

.pricing {
  color: #1f2933;
  font-size: 14px;
  margin: 12px;
  padding: 0;
}

.details {
  color: #f5f7fa;
  font-weight: bold;
  font-size: 14px;
  margin: 12px;
  p {
    background: #f9703e;
    /* background: #323f4b; */
    list-style-type: none;
    margin: 2px 0;
    padding: 8px;
  }
  a {
    color: #f5f7fa;
  }
  a:visited {
    color: #e4e7eb;
  }
  a:hover {
    color: #f5f7fa;
  }
}

.detail-top {
  border-radius: 4px 4px 0 0;
  /* border-bottom: 2px solid #f5f7fa; */
}

.detail-middle {
  border-radius: 0;
  /* border-bottom: 2px solid #f5f7fa; */
}

.detail-bottom {
  border-radius: 0 0 4px 4px;
}

.slide-enter-active,
.slide-leave-active {
  transition: all 0.5s ease-out;
}

.slide-enter,
.slide-leave-to {
  transform: translateX(-400px);
  opacity: 0;
}
</style>
