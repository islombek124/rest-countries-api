<script>
import SearchPanel from "@/components/SearchPanel.vue";
import Countries from "@/components/Countries.vue";
export default {
  components: {
    SearchPanel,
    Countries,
  },
  data() {
    return {
      selectedRegion: "Africa",
      countries: null,
      term: "",
    };
  },
  methods: {
    apiData() {
      fetch(`https://restcountries.com/v3/region/${this.selectedRegion}`)
        .then((res) => res.json())
        .then((data) => (this.countries = data));
    },
    changeReg(region) {
      this.selectedRegion = region;
    },
    termos(e) {
      this.term = e.target.value;
    },
    onSearchHandler(countries, term) {
      if (term.length == 0) {
        return this.countries;
      }

      return this.countries.filter(
        (c) => c.name.common.toLowerCase().indexOf(term) > -1
      );
    },
    updateTermHandler(term) {
      this.term = term;
    },
  },
  mounted() {
    this.apiData();
  },
  updated() {
    if (this.selectedRegion) {
      this.apiData();
    }
  },
};
</script>

<template>
  <div class="main">
    <div class="container">
      <SearchPanel
        :updateTermHandler="updateTermHandler"
        :selectedRegion="selectedRegion"
        @changeReg="changeReg"
        @term="termos"
      />
      <Countries :data="onSearchHandler(countries, term)" />
    </div>
  </div>
</template>
