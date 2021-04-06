<template>
  <div class="wrapper__component">
    <div class="art">
      <canvas id="canvas1"> <img src="" id="image1" /> </canvas>
    </div>
    <div id="btn" @click="effect">
      <span class="noselect">Click me!</span>
      <div id="circle"></div>
    </div>
    <div class="donation">
      <router-link to="/about"
        ><p>keep this website and my passion running</p></router-link
      >
    </div>
  </div>
</template>

<script>
import { useStore } from "vuex";

export default {
  name: "bandw",

  setup() {
    const store = useStore();
    return { store };
  },

  mounted() {
    this.setImageSource();
  },

  methods: {
    setImageSource() {
      const image1 = document.getElementById("image1");
      image1.src = this.store.state.imageBaW;

      const canvas = document.getElementById("canvas1");
      canvas.width = window.innerWidth * 0.66 * 0.607;
      canvas.height = window.innerWidth * 0.66 * 0.607;
    },
    effect() {
      const button = document.getElementById("btn");
      button.remove();

      const image1 = document.getElementById("image1");
      const canvas = document.getElementById("canvas1");
      const ctx = canvas.getContext("2d");
      ctx.drawImage(image1, 0, 0, canvas.width, canvas.height);
      const pixels = ctx.getImageData(0, 0, canvas.width, canvas.height);
      // remove to initialy show image:
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      let particlesArray = [];
      const numberOfParticles = 2000;

      // calculate brightness based on human perception
      function calculateBrightness(red, green, blue) {
        return Math.sqrt(
          red * red * 0.299 + green * green * 0.587 + blue * blue * 0.114
        );
      }

      let mappedImage = [];
      for (let y = 0; y < canvas.height; y++) {
        let row = [];
        for (let x = 0; x < canvas.width; x++) {
          const red = pixels.data[y * 4 * pixels.width + x * 4];
          const green = pixels.data[y * 4 * pixels.width + (x * 4 + 1)];
          const blue = pixels.data[y * 4 * pixels.width + (x * 4 + 2)];
          const brightness = calculateBrightness(red, green, blue) / 110;
          const cellBrightness = brightness;
          const cell = [cellBrightness];
          row.push(cell);
        }
        mappedImage.push(row);
        this.store.commit("pushMappedImageRow", row);
      }

      class Particle {
        constructor() {
          this.x = Math.random() * canvas.width;
          this.y = 0;
          this.speed = 0;
          this.velocity = Math.random() * 0.5;
          this.size = Math.random() * 1.1 + 0.9;
          this.position1 = Math.floor(this.y);
          this.position2 = Math.floor(this.x);
        }
        update() {
          this.position1 = Math.floor(this.y);
          this.position2 = Math.floor(this.x);
          this.speed = mappedImage[this.position1][this.position2][0];
          let movement = 2.5 - this.speed + this.velocity;

          this.y += movement;
          if (this.y >= canvas.height) {
            this.y = 0;
            this.x = Math.random() * canvas.width;
          }
        }
        draw() {
          ctx.beginPath();
          ctx.fillStyle = "white";
          ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
          ctx.fill();
        }
      }

      function init() {
        for (let i = 0; i < numberOfParticles; i++) {
          particlesArray.push(new Particle());
        }
      }
      init();

      function animate() {
        ctx.globalAlpha = 0.05;
        ctx.fillStyle = "rgb(0, 0, 0)";
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        ctx.globalAlpha = 0.2;
        for (let i = 0; i < particlesArray.length; i++) {
          particlesArray[i].update();
          ctx.globalAlpha = particlesArray[i].speed * 0.5;
          particlesArray[i].draw();
        }
        requestAnimationFrame(animate);
      }
      animate();
    },
  },
  beforeUnmount: function () {
    const image1 = document.getElementById("image1");
    image1.src = "";
  },
};
</script>

<style lang="scss" scoped>
.wrapper__component {
  .art {
    #canvas1 {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      filter: blur(0.5px) contrast(1.05);
    }
  }

  #btn {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: rgb(25, 255, 255);
    height: 40px;
    width: 150px;
    border: none;
    border-radius: 10px;
    color: black;
    font-size: 25px;
    transition: 1s;
    -webkit-tap-highlight-color: transparent;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    padding-top: 5px;
  }

  #btn #circle {
    width: 5px;
    height: 5px;
    background: transparent;
    border-radius: 50%;
    position: absolute;
    top: 0;
    left: 50%;
    overflow: hidden;
    transition: 100ms;
  }

  .noselect {
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }

  #btn:hover {
    background: transparent;
    color: white;
  }

  #btn:hover #circle {
    height: 40px;
    width: 150px;
    left: 0;
    border-radius: 0;
    border-bottom: 2px solid rgb(255, 29, 94);
    color: white;
  }

  .donation {
    color: rgb(83, 83, 83);
    position: absolute;
    bottom: 0;
    padding-bottom: 10px;
    width: 100%;

    .donation p {
      text-align: center;
    }
  }
}
</style>
