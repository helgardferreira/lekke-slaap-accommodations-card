<template>
  <div class="accommodation-card" @click="printBkgImg">
    <header>
      <h4 class="header-text">Tsala Treetop Lodge</h4>
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
  </div>
</template>

<script>
export default {
  name: "AccommodationsCard",
  props: ["name"],
  data() {
    return {
      bkgImg: require("../assets/tsala-treetop-lodge-1.jpeg")
    };
  },
  methods: {
    printBkgImg() {
      console.log(this.bkgImg);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
button {
  font-size: 25px;
  background: #c62735;
  color: white;
  border: 0;
  padding: 5px 15px;
  margin: 0 10px;
  border-radius: 4px;
  outline: 0;
  cursor: pointer;
}

.accommodation-card {
  width: 300px;
  height: 550px;
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

// .accommodation-card:hover .overlay {
//   opacity: 1;
//   background: rgba(0, 0, 0, 0.6);
//   transition: 0.3s opacity ease-out;
// }

.header-img {
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  height: 200px;
}

.header-text {
  background: rgba(0, 0, 0, 0.6);
  text-align: center;
  position: absolute;
  top: 10%;
  z-index: 1000;
  overflow: hidden;
  border-radius: 0 50px 50px 0;
  // transition: 0.3s opacity ease-in;
  padding: 20px 35px;
  color: white;
}

// .premium-banner {
//   text-align: right;
//   clip-path: polygon(0% 0%, 100% 0, 100% 100%, 10% 100%);
//   border-radius: 0 0 0 100px;
//   background: #000;
//   margin: 0;
//   padding: 10px;
//   color: #fff;
// }

.extract {
  color: white;
  text-align: right;
  font-size: 0.8rem;
  background: #f9703e;
  border-radius: 50px 0 0 50px;
  margin: 10px 0 10px 10px;
  padding: 10px;
}
</style>