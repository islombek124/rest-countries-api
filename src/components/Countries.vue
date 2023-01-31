<script>
import CountriesItem from "./CountriesItem.vue";

export default {
  props: {
    data: Array,
  },
  components: { CountriesItem },
};
</script>

<template>
  <ul class="row row-cols-4 gap-5 justify-content-center py-4">
    <CountriesItem :data="data" />
  </ul>
</template>

<style scoped>
a {
  display: contents;
}
</style>
