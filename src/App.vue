<script>
import Nav from "@/components/Nav.vue";
export default {
  components: { Nav },
};
</script>

<template>
  <div class="wrapper w-100 mx-auto">
    <Nav />
  </div>
  <router-view v-slot="{ Component }">
    <Transition name="slide" mode="out-in">
      <component :is="Component"></component>
    </Transition>
  </router-view>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Nunito+Sans:wght@400;600;800&display=swap");

body {
  font-family: "Nunito Sans", sans-serif;
  background: #f2f2f2;
}

.dark {
  background: #202c36;
}

a {
  text-decoration: none;
  color: currentColor;
  max-width: max-content;
}

li {
  list-style: none;
}

.slide-enter-active,
.slide-leave-to {
  transition: opacity 0.7s, transform 0.9s;
}

.slide-enter-from,
.slide-leave-to {
  opacity: 0;
  transform: translateY(5%);
}
</style>
