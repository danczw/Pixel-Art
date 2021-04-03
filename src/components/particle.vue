<template>
  <div class="wrapper">
    <div class="art">
      <canvas id="canvas1"></canvas>
      <canvas id="canvas2"></canvas>
      <canvas id="canvas3"></canvas>
    </div>
  </div>
</template>

<script>
export default {
  name: "particle",
  setup() {},
  mounted() {
    this.background();
    this.effect();
    this.effect_two();
  },
  methods: {
    effect() {
      const canvas = document.getElementById("canvas1");
      const ctx = canvas.getContext("2d");
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
      let particleArray = [];
      let adjustX = window.innerWidth / 200; // move text on x-axis
      let adjustY = window.innerWidth / 85; // move text on y-axis

      // handke mouse
      const mouse = {
        x: null,
        y: null,
        radius: 150,
      };
      window.addEventListener("mousemove", function (e) {
        mouse.x = e.x;
        mouse.y = e.y;
      });

      ctx.fillStyle = "white";
      ctx.font = "30px Arial";
      ctx.fillText("Digital", 30, 30);
      // ctx.fillText("Distance", 30, 30);
      const textData = ctx.getImageData(0, 0, 200, 200); // check scan area

      class Particle {
        constructor(x, y) {
          this.x = x;
          this.y = y;
          this.size = 4;
          this.baseX = this.x;
          this.baseY = this.y;
          this.density = Math.random() * 30 + 1;
        }
        draw() {
          ctx.fillStyle = "white";
          ctx.beginPath();
          ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
          ctx.closePath();
          ctx.fill();
        }
        update() {
          let dx = mouse.x - this.x;
          let dy = mouse.y - this.y;
          let distance = Math.sqrt(dx * dx + dy * dy);
          let forceDirectionX = dx / distance;
          let forceDirectionY = dy / distance;
          let maxDistance = mouse.radius;
          let force = (maxDistance - distance) / maxDistance;
          let directionX = forceDirectionX * force * this.density;
          let directionY = forceDirectionY * force * this.density;
          if (distance < mouse.radius) {
            this.x -= directionX;
            this.y -= directionY;
          } else {
            if (this.x !== this.baseX) {
              let dx = this.x - this.baseX;
              this.x -= dx / 5;
            }
            if (this.y !== this.baseY) {
              let dy = this.y - this.baseY;
              this.y -= dy / 5;
            }
          }
        }
      }
      function init() {
        particleArray = [];
        for (let y = 0, y2 = textData.height; y < y2; y++) {
          for (let x = 0, x2 = textData.width; x < x2; x++) {
            if (textData.data[y * 4 * textData.width + x * 4 + 3] > 128) {
              let positionX = x + adjustX;
              let positionY = y + adjustY;
              particleArray.push(new Particle(positionX * 9, positionY * 9)); // change size of effect
            }
          }
        }
      }
      init();

      function animate() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        for (let i = 0; i < particleArray.length; i++) {
          particleArray[i].draw();
          particleArray[i].update();
        }
        connect();
        requestAnimationFrame(animate);
      }
      animate();

      function connect() {
        let opacityValue = 1;
        for (let a = 0; a < particleArray.length; a++) {
          for (let b = a; b < particleArray.length; b++) {
            let dx = particleArray[a].x - particleArray[b].x;
            let dy = particleArray[a].y - particleArray[b].y;
            let distance = Math.sqrt(dx * dx + dy * dy);

            if (distance < 20) {
              // change distance limit to connect dots
              opacityValue = 1 - distance / 20;
              let dx = mouse.x - particleArray[b].x;
              let dy = mouse.y - particleArray[b].y;
              let mouseDistance = Math.sqrt(dx * dx + dy * dy);

              if (mouseDistance < mouse.radius / 2) {
                particleArray[a].size = 5;
                ctx.strokeStyle = `rgba(255, 25, 25, ${opacityValue})`;
              } else if (mouseDistance < mouse.radius - 50) {
                particleArray[a].size = 4;
                ctx.strokeStyle = `rgba(255, 100, 100, ${opacityValue})`;
              } else if (mouseDistance < mouse.radius) {
                particleArray[a].size = 3;
                ctx.strokeStyle = `rgba(255, 200, 200, ${opacityValue})`;
              } else {
                particleArray[a].size = 2;
                ctx.strokeStyle = `rgba(255, 255, 255, ${opacityValue})`;
              }

              ctx.lineWidth = 2;
              ctx.beginPath();
              ctx.moveTo(particleArray[a].x, particleArray[a].y);
              ctx.lineTo(particleArray[b].x, particleArray[b].y);
              ctx.stroke();
            }
          }
        }
      }
    },
    effect_two() {
      const canvas = document.getElementById("canvas2");
      const ctx = canvas.getContext("2d");
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
      let particleArray = [];
      let adjustX = window.innerWidth / 200; // move text on x-axis
      let adjustY = window.innerWidth / 40; // move text on y-axis

      // handke mouse
      const mouse = {
        x: null,
        y: null,
        radius: 150,
      };
      window.addEventListener("mousemove", function (e) {
        mouse.x = e.x;
        mouse.y = e.y;
      });

      ctx.fillStyle = "white";
      ctx.font = "30px Arial";
      ctx.fillText("Distance", 30, 30);
      // ctx.fillText("Distance", 30, 30);
      const textData = ctx.getImageData(0, 0, 200, 200); // check scan area

      class Particle {
        constructor(x, y) {
          this.x = x;
          this.y = y;
          this.size = 5;
          this.baseX = this.x;
          this.baseY = this.y;
          this.density = Math.random() * 30 + 1;
        }
        draw() {
          ctx.fillStyle = "white";
          ctx.beginPath();
          ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
          ctx.closePath();
          ctx.fill();
        }
        update() {
          let dx = mouse.x - this.x;
          let dy = mouse.y - this.y;
          let distance = Math.sqrt(dx * dx + dy * dy);
          let forceDirectionX = dx / distance;
          let forceDirectionY = dy / distance;
          let maxDistance = mouse.radius;
          let force = (maxDistance - distance) / maxDistance;
          let directionX = forceDirectionX * force * this.density;
          let directionY = forceDirectionY * force * this.density;
          if (distance < mouse.radius) {
            this.x -= directionX;
            this.y -= directionY;
          } else {
            if (this.x !== this.baseX) {
              let dx = this.x - this.baseX;
              this.x -= dx / 5;
            }
            if (this.y !== this.baseY) {
              let dy = this.y - this.baseY;
              this.y -= dy / 5;
            }
          }
        }
      }
      function init() {
        particleArray = [];
        for (let y = 0, y2 = textData.height; y < y2; y++) {
          for (let x = 0, x2 = textData.width; x < x2; x++) {
            if (textData.data[y * 4 * textData.width + x * 4 + 3] > 128) {
              let positionX = x + adjustX;
              let positionY = y + adjustY;
              particleArray.push(new Particle(positionX * 9, positionY * 9)); // change size of effect
            }
          }
        }
      }
      init();

      function animate() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        for (let i = 0; i < particleArray.length; i++) {
          particleArray[i].draw();
          particleArray[i].update();
        }
        connect();
        requestAnimationFrame(animate);
      }
      animate();

      function connect() {
        let opacityValue = 1;
        for (let a = 0; a < particleArray.length; a++) {
          for (let b = a; b < particleArray.length; b++) {
            let dx = particleArray[a].x - particleArray[b].x;
            let dy = particleArray[a].y - particleArray[b].y;
            let distance = Math.sqrt(dx * dx + dy * dy);

            if (distance < 20) {
              // change distance limit to connect dots
              opacityValue = 1 - distance / 20;
              let dx = mouse.x - particleArray[b].x;
              let dy = mouse.y - particleArray[b].y;
              let mouseDistance = Math.sqrt(dx * dx + dy * dy);

              if (mouseDistance < mouse.radius / 2) {
                particleArray[a].size = 5;
                ctx.strokeStyle = `rgba(25, 255, 255, ${opacityValue})`;
              } else if (mouseDistance < mouse.radius - 50) {
                particleArray[a].size = 4;
                ctx.strokeStyle = `rgba(100, 255, 255, ${opacityValue})`;
              } else if (mouseDistance < mouse.radius) {
                particleArray[a].size = 3;
                ctx.strokeStyle = `rgba(175, 230, 255, ${opacityValue})`;
              } else {
                particleArray[a].size = 2;
                ctx.strokeStyle = `rgba(255, 255, 255, ${opacityValue})`;
              }

              ctx.lineWidth = 2;
              ctx.beginPath();
              ctx.moveTo(particleArray[a].x, particleArray[a].y);
              ctx.lineTo(particleArray[b].x, particleArray[b].y);
              ctx.stroke();
            }
          }
        }
      }
    },
    background() {
      const canvas = document.getElementById("canvas3");
      const ctx = canvas.getContext("2d");
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;

      let particleArray = [];

      // create particle
      class Particle {
        constructor(x, y, directionX, directionY, size, color) {
          this.x = x;
          this.y = y;
          this.directionX = directionX;
          this.directionY = directionY;
          this.size = size;
          this.color = color;
        }
        // draw individual particle
        draw() {
          ctx.beginPath();
          ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2, false);
          ctx.fillStyle = "rgba(25, 255, 255, 0.2)";
          ctx.fill();
        }
        update() {
          if (this.x > canvas.width || this.x < 0) {
            this.directionX = -this.directionX;
          }
          if (this.y > canvas.height || this.y < 0) {
            this.directionY = -this.directionY;
          }
          // move particles
          this.x += this.directionX;
          this.y += this.directionY;
          // draw particles
          this.draw();
        }
      }
      function init() {
        particleArray = [];
        let numberOfParticles = (canvas.height * canvas.width) / 15000;
        for (let i = 0; i < numberOfParticles; i++) {
          let size = Math.random() * 5 + 1;
          let x = Math.random() * (innerWidth - size * 2 - size * 2) + size * 2;
          let y =
            Math.random() * (innerHeight - size * 2 - size * 2) + size * 2;
          let directionX = Math.random() * 5 - 2.5;
          let directionY = Math.random() * 5 - 2.5;
          let color = "rgba(25, 255, 255, 0.2)";

          particleArray.push(
            new Particle(x, y, directionX, directionY, size, color)
          );
        }
      }
      init();
      animate();
      // check if particles are close enough and connect
      function connect() {
        let opacityValue = 1
        for (let a = 0; a < particleArray.length; a++) {
          for (let b = 0; b < particleArray.length; b++) {
            let distance = (
              ((particleArray[a].x - particleArray[b].x)
              * (particleArray[a].x - particleArray[b].x))
              + ((particleArray[a].y - particleArray[b].y)
              * (particleArray[a].y - particleArray[b].y))
            )
            if (distance < canvas.width/10 * canvas.height/10) {
              opacityValue = 1 - (distance / 10000);
              ctx.strokeStyle = `rgba(25, 75, 75, ${opacityValue})`
              ctx.lineWidth = 1;
              ctx.beginPath;
              ctx.moveTo(particleArray[a].x, particleArray[a].y);
              ctx.lineTo(particleArray[b].x, particleArray[b].y)
              ctx.stroke();
            }
          }
        }
      }

      function animate() {
        requestAnimationFrame(animate);
        ctx.clearRect(0, 0, innerWidth, innerHeight);

        for (let i = 0; i < particleArray.length; i++) {
          particleArray[i].update();
        }    
        connect();
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
#canvas1 {
  top: 0;
  left: 0;
  position: absolute;
}

#canvas2 {
  top: 0;
  left: 0;
  position: absolute;
}

#canvas3 {
  top: 0;
  left: 0;
  position: absolute;
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
</style>
