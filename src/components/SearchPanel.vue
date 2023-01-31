<script>
export default {
  props: {
    updateTermHandler: Function,
    selectedRegion: String,
  },
  data() {
    return {
      buttons: [
        {
          title: "Africa",
          name: "africa",
        },
        {
          title: "America",
          name: "america",
        },
        {
          title: "Asia",
          name: "asia",
        },
        {
          title: "Europe",
          name: "europe",
        },
        {
          title: "Oceania",
          name: "oceania",
        },
      ],
      term: "",
    };
  },
  methods: {
    changeHandler(e) {
      this.term = e.target.value;
      this.updateTermHandler(this.term);
    },
  },
};
</script>

<template>
  <div class="navbar py-4">
    <div class="container gap-3">
      <div class="input-group flex-nowrap shadow-sm">
        <span class="input-group-text px-3" id="addon-wrapping">
          <svg
            width="18"
            height="18"
            viewBox="0 0 18 18"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              clip-rule="evenodd"
              d="M12.5 11H11.7L11.4 10.7C12.4 9.6 13 8.1 13 6.5C13 2.9 10.1 0 6.5 0C2.9 0 0 2.9 0 6.5C0 10.1 2.9 13 6.5 13C8.1 13 9.6 12.4 10.7 11.4L11 11.7V12.5L16 17.5L17.5 16L12.5 11ZM6.5 11C4 11 2 9 2 6.5C2 4 4 2 6.5 2C9 2 11 4 11 6.5C11 9 9 11 6.5 11Z"
              fill="#848484"
            />
          </svg>
        </span>
        <input
          type="text"
          class="form-control p-3"
          placeholder="Search for a country…"
          aria-label="Search for a country…"
          aria-describedby="addon-wrapping"
          :value="term"
          @input="changeHandler"
        />
      </div>
      <!--  -->
      <div class="dropdown">
        <button
          class="btn border-0 dropdown-toggle shadow-sm p-3"
          type="button"
          data-bs-toggle="dropdown"
          aria-expanded="false"
        >
          Filter by Region
        </button>
        <ul class="dropdown-menu shadow-sm">
          <button
            class="dropdown-item"
            v-for="btn in buttons"
            :key="btn.name"
            @click="$emit('changeReg', $event.target.innerHTML.toLowerCase())"
          >
            {{ btn.title }}
          </button>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
.input-group {
  width: 35%;
}

.dropdown button {
  background: white;
}

.dark *,
.dark *::placeholder {
  color: white;
}

.dark .input-group input,
.dark .input-group span,
.dark .dropdown button,
.dark .dropdown ul {
  background: #2b3844;
  border: none;
}

.dark .dropdown ul button:hover {
  background: rgba(0, 0, 0, 0.1);
}

@media (max-width: 995px) {
  .input-group {
    width: 100%;
  }
}
</style>
