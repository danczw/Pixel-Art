<template>
  <div class="home">
    <particle />
  </div>
</template>

<script>
// @ is an alias to /src
import particle from "@/components/particle.vue";

export default {
  name: "Home",
  components: {
    particle,
  },
};
</script>
