<template>
  <div class="wrapper">
    <div class="wrapper__content">
      <router-view />
    </div>
    <div class="wrapper__nav">
      <div class="outer">
        <div class="inner">
          <router-link to="/">Home</router-link>
        </div>
      </div>
      <div class="outer">
        <div class="inner">
          <router-link to="/color">Color</router-link>
        </div>
      </div>
      <div class="outer">
        <div class="inner">
          <router-link to="/bandw">B & W</router-link>
        </div>
      </div>
      <div class="outer">
        <div class="inner">
          <!-- <router-link to="/about">About</router-link> -->
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  overflow: hidden;
  text-align: center;
  color: #2c3e50;

  .wrapper {
    display: flex;
    flex-direction: row;

    .wrapper__nav {
      height: 90%;
      min-height: 600px;
      width: 10px;
      display: flex;
      flex-direction: column;
      position: absolute;
      right: 10px;

      .outer {
        display: flex;
        margin: auto;
        max-width: 1000px;
        justify-content: space-between;
        text-align: center;
        list-style-type: none;
        writing-mode: tb-rl;
        align-items: center;

        .inner {
          width: 30px;
          text-transform: uppercase;
          cursor: pointer;
          color: white;
          margin: auto;

          a {
            text-decoration: none;
            color: #385877;
            font-size: 30px;
          }
        }

        .inner:hover {
          // background-image: url("https://scottyzen.sirv.com/Images/v/button.png");
          border-radius: 5px;
          background-color: white;
          background-size: 100% 100%;
          animation: spring 300ms ease-out;
          text-shadow: 0 -1px 0 black;
          font-weight: bold;

          a {
            color: black;
          }
        }
        // .inner:active {
        //   transform: translateY(4px);
        //   color: white;
        // }
      }

      @keyframes spring {
        15% {
          -webkit-transform-origin: center center;
          -webkit-transform: scale(1.2, 1.1);
        }
        40% {
          -webkit-transform-origin: center center;
          -webkit-transform: scale(0.95, 0.95);
        }
        75% {
          -webkit-transform-origin: center center;
          -webkit-transform: scale(1.05, 1);
        }
        100% {
          -webkit-transform-origin: center center;
          -webkit-transform: scale(1, 1);
        }
      }
    }
  }
}
</style>
