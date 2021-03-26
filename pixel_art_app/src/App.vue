<template>
  <div class="wrapper">
    <div class="content">
      <p>hi</p>
    </div>

    <div class="nav">
      <div class="nav__item">
        <p><router-link to="/">Home</router-link></p>
      </div>
      <div class="nav__item">
        <p><router-link to="/about">About</router-link></p>
      </div>
    </div>
    <router-view />
  </div>
  
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  .wrapper {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  
    .nav {
      padding: 10px;
      width: 50px;
      height: 90vh;
      position: absolute;
      right: 0;

      .nav__item {
        // margin: 10px;
        min-height: 60px;

        p {
          transform: rotate(90deg);
          text-anchor: middle;
        }
      }
    }
    .nav a {
      font-weight: bold;
      color: #2c3e50;
    }

    .nav a.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
