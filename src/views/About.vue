<template>
  <div class="wrapper__home">
    <div id="tbd">
      <div>
        <p>
          Tip Nano:
          nano_3jpa68851np7yzfwdzentxzr1rai9eftni4sabxogrruttjws7y1mhhrqu7c
        </p>
        <p>Tip BTC: coming soon</p>
      </div>
    </div>
    <div class="loader__wrapper">
      <atom-spinner :animation-duration="1000" :size="60" :color="'#ff1d5e'" />
    </div>
  </div>
</template>

<script>
import { AtomSpinner } from "epic-spinners";

export default {
  name: "about",
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
  color: white;
  font-size: 20px;
  width: 100vw;
  text-align: left;
  font-family: "Lato";

  #tbd {
    padding-left: 20%;
  }

  .loader__wrapper {
    margin-left: auto;
    margin-right: auto;
    padding-top: 50px;
  }
}
</style>
