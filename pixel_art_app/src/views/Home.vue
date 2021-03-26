<template>
  <div class="home">
    <bwArt />
  </div>
</template>

<script>
// @ is an alias to /src
import bwArt from "@/components/bwArt.vue";

export default {
  name: "Home",
  components: {
    bwArt,
  },
};
</script>
