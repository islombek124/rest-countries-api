<script>
export default {
  data() {
    return {
      country: null,
      showCountry: false,
    };
  },
  computed: {
    countryId() {
      return this.$route.params.name;
    },
  },
  async created() {
    const response = await fetch(
      `https://restcountries.com/v3/name/${this.countryId}`
    );
    const res = await response.json();
    this.country = res[0];
    this.showCountry = true;
  },
};
</script>

<template>
  <div class="container py-5" v-if="showCountry">
    <div class="go-back">
      <router-link
        to="/"
        class="router-link d-flex align-items-center gap-2 shadow-sm p-2 px-4 rounded"
      >
        <svg
          width="19"
          height="12"
          viewBox="0 0 19 12"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M6.46447 0.107445L7.64298 1.28596L3.75389 5.17504L18.6031 5.17504L18.6031 6.82496L3.75389 6.82496L7.64298 10.714L6.46447 11.8926L0.57191 6L6.46447 0.107445Z"
            fill="#111517"
          />
        </svg>
        Back
      </router-link>
    </div>
    <div class="py-5 row align-items-center gap-4">
      <div class="flag col">
        <img :src="country.flags[0]" :alt="country.name.common" />
      </div>
      <div class="info col d-grid gap-4">
        <div class="col">
          <h2 class="fw-bold">
            {{ country.name.official }}
          </h2>
        </div>
        <div class="about row">
          <div class="col-md">
            <p>
              Native Name:
              <span>{{
                Object.values(country.name.nativeName)[0].common
              }}</span>
            </p>
            <p>
              Population: <span>{{ country.population }}</span>
            </p>
            <p>
              Region: <span>{{ country.region }}</span>
            </p>
            <p>
              Sub Region: <span>{{ country.subregion }}</span>
            </p>
            <p>
              Capital: <span>{{ country.capital.join(" ") }}</span>
            </p>
          </div>
          <div class="col-md">
            <p>
              Top Level Domain: <span>{{ country.tld.join(" ") }}</span>
            </p>
            <p>
              Currencies:
              <span
                v-for="currency in country.currencies"
                :key="currency.name"
                >{{ currency.name }}</span
              >
            </p>
            <p>
              Language:
              <span>{{ Object.values(country.languages).join(", ") }}</span>
            </p>
          </div>
        </div>
        <div class="borderC">
          Border Countries:
          <button
            class="m-1 btn rounded shadow-sm"
            v-for="border in country.borders"
            :key="border"
          >
            {{ border }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.flag img {
  width: 560px;
  height: 400px;
  object-fit: contain;
}

.about p {
  font-weight: 600;
}

.about p span {
  font-weight: normal;
}

.router-link {
  background: white;
}

.dark * {
  color: white;
}

.dark .router-link {
  background: #2b3844;
}

.dark .router-link svg path {
  fill: white;
}

@media (max-width: 560px) {
  .flag img {
    width: 320px;
    height: 230px;
    object-fit: contain;
  }
}
</style>
