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
export default {
  name: "color",
  mounted() {
    this.imageSource();
  },
  methods: {
    imageSource() {
      const image1 = document.getElementById("image1");
      image1.src =
        "data:image/jpeg;base64,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";

      const canvas = document.getElementById("canvas1");
      canvas.width = window.innerWidth * 0.66;
      canvas.height = window.innerWidth * 0.66 * 0.607;
    },
    effect() {
      const button = document.getElementById("btn");
      button.remove();

      const image1 = document.getElementById("image1");
      const canvas = document.getElementById("canvas1");
      const ctx = canvas.getContext("2d");

      let counter = 0;
      setInterval(function () {
        counter++;
      }, 600);

      ctx.drawImage(image1, 0, 0, canvas.width, canvas.height);
      const pixels = ctx.getImageData(0, 0, canvas.width, canvas.height);
      // remove to initialy show image:
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      let particlesArray = [];
      const numberOfParticles = 3000;

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
          const brightness = calculateBrightness(red, green, blue) / 70;
          const cellBrightness = brightness;
          const cellColor = `rgb(${red}, ${green}, ${blue})`;
          const cell = [cellBrightness, cellColor];
          row.push(cell);
        }
        mappedImage.push(row);
      }

      class Particle {
        constructor() {
          this.x = Math.random() * canvas.width;
          this.y = 0;
          this.speed = 0;
          this.velocity = Math.random() * 0.5;
          this.size = Math.random() * 1.5 + 1;
          this.position1 = Math.floor(this.y);
          this.position2 = Math.floor(this.x);
          this.angle = 0;
        }
        update() {
          this.position1 = Math.floor(this.y);
          this.position2 = Math.floor(this.x);
          if (
            mappedImage[this.position1] &&
            mappedImage[this.position1][this.position2]
          ) {
            this.speed = mappedImage[this.position1][this.position2][0] / 8;
          }
          let movement = 2.5 - this.speed + this.velocity;
          this.angle += this.speed / 5; // change angle (circle size) based on speed
          this.size = this.speed * 4 + 1; // change size based on speed based on brigthness

          // define effect restart
          if (counter % 50 === 0) {
            this.x = Math.random() * canvas.width;
            this.y = 0;
          }

          this.y += movement + Math.sin(this.angle) * 1.8; // change movement
          this.x += movement / 3 + Math.cos(this.angle) * 0.5; // change movement
          if (this.y >= canvas.height) {
            this.y = 0;
            this.x = Math.random() * canvas.width;
          }
          if (this.x >= canvas.width) {
            this.x = 0;
            this.y = Math.random() * canvas.height;
          }
        }
        draw() {
          ctx.beginPath();
          if (
            mappedImage[this.position1] &&
            mappedImage[this.position1][this.position2]
          ) {
            ctx.fillStyle = mappedImage[this.position1][this.position2][1];
            // ctx.strokeStyle = mappedImage[this.position1][this.position2][1];
          }
          // ctx.fillStyle = gradient1; // color gradient
          // ctx.strokeRect(this.x, this.y, this.size, this.size)
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
          // ctx.globalAlpha = particlesArray[i].speed * 0.5;
          ctx.globalAlpha = 1;
          particlesArray[i].draw();
        }
        requestAnimationFrame(animate);
      }
      animate();
    },
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
