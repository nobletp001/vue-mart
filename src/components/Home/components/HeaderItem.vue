<template>
  <v-hover v-slot="{ isHovering, props }">
    <div class="top_offers_box" v-bind="props">
      <img
        :style="`scale : ${isHovering ? 1.09 : 1}`"
        :src="propsitem?.src"
        :alt="propsitem?.alt"
      />
    </div>
  </v-hover>
</template>

<script>
export default {
  name: "HeaderItem",
  props: ["item"],
  setup(props) {
    // Use onMounted to execute code after the component is mounte

    return { propsitem: props.item }; // Return the item prop directly
  },
};
</script>

<style lang=""></style>
