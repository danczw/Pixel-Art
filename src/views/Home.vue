<template>
  <div class="wrapper__home">
    <div id="tbd">More is being worked on... come back in a while...</div>
    <div class="loader__wrapper">
      <atom-spinner :animation-duration="1000" :size="60" :color="'#ff1d5e'" />
    </div>
  </div>
</template>

<script>
import { AtomSpinner } from "epic-spinners";

export default {
  name: "Home",
  components: {
    AtomSpinner,
  },
};
</script>

<style lang="scss" scoped>
.wrapper__home {
  display: flex;
  flex-direction: column;
  justify-content: center;
  color: rgb(147, 29, 63);
  font-size: 20px;
  width: 100vw;
  font-family: "Lato";

  .loader__wrapper {
    margin-left: auto;
    margin-right: auto;
    padding-top: 50px;
  }
}
</style>
