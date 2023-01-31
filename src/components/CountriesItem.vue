<script>
export default {
  props: {
    data: Array,
  },
};
</script>

<template>
  <li
    class="rounded shadow-sm w-100 p-0 position-relative"
    v-for="country in data"
    :key="country.name.common.toLowerCase()"
  >
    <div class="flag w-100">
      <img :src="country.flags[1]" class="w-100" :alt="country.name.common" />
    </div>
    <div class="info p-4">
      <h2 class="title fs-4 fw-bold">
        {{ country.name.common }}
      </h2>
      <div class="info2 pt-4">
        <p>
          Population: <span>{{ country.population }}</span>
        </p>
        <p>
          Region: <span>{{ country.region }}</span>
        </p>
        <p>
          Capital: <span>{{ Array(country.capital).join(" ") }}</span>
        </p>
      </div>
    </div>
    <router-link :to="`/country/${country.name.common}`">
      <button class="btn btn-secondary p-1 position-absolute bottom-0 end-0">
        Learn More
      </button>
    </router-link>
  </li>
</template>

<style scoped>
li {
  max-width: 265px;
  overflow: hidden;
  background: white;
}

.flag img {
  height: 160px;
  object-fit: cover;
}

p {
  font-weight: 600;
}

p span {
  font-weight: normal;
}

.dark * {
  color: white;
}

.dark li {
  background: #2b3844;
}
</style>
