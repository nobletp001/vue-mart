<template>
  <div class="top_offers">
    <v-container>
      <v-row>
        <v-col cols="12" md="4" v-for="(item, index) in items" :key="index">
          <HeaderItem :item="item" />
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" md="6">
          <v-hover v-slot="{ isHovering, props }">
            <div class="top_offers_box" v-bind="props">
              <img
                :style="`scale : ${isHovering ? 1.09 : 1}`"
                src="@/assets/images/iphones.webp"
                alt="iphones-Image"
              />
            </div>
          </v-hover>
        </v-col>
        <v-col cols="12" md="6">
          <v-hover v-slot="{ isHovering, props }">
            <div class="top_offers_box" v-bind="props">
              <img
                :style="`scale : ${isHovering ? 1.09 : 1}`"
                src="@/assets/images/laptops.webp"
                alt="laptops-Image"
              />
            </div>
          </v-hover>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
<script>
import { ref } from "vue";
import HeaderItem from "@/components/Home/components/HeaderItem";
export default {
  name: "TopOffer",
  components: {
    HeaderItem,
  },
  setup() {
    const items = ref([
      {
        src: require("@/assets/images/playstations.webp"),
        alt: "playstation-Image",
      },
      {
        src: require("@/assets/images/chairs.webp"),
        alt: "chairs-Image",
      },
      {
        src: require("@/assets/images/headset.webp"),
        alt: "headset-Image",
      },
    ]);

    return { items };
  },
};
</script>
<style lang="scss">
.top_offers {
  background: #f5f5f5;
  padding-top: 40px;
  &_box {
    overflow: hidden;
    border-radius: 10px;
    img {
      width: 100%;
      transition: 0.7s all ease-in-out;
      cursor: pointer;
    }
  }
}
</style>
