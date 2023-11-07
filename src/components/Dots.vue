<template>
  <div class="container">
      <div 
          class="circle" 
          v-for="(circle, index) in circles" 
          v-bind:style="{
              left: circle.coordX + 'px', 
              top: circle.coordY + 'px',
              opacity: 1 - (0.2 * index),
          }">
      </div>
  </div>
</template>


<script>

export default {
  name: 'Dots',
  data() {
      return {
          circles: []
      }
  },
  methods: {
      handleMouseMove(event) {
          this.circles.forEach((circle, index) => {
              setTimeout(function () {
                  circle.coordX = event.clientX;
                  circle.coordY = event.clientY;
              }, index * 100)
          });
      },
  },
  mounted() {
      for (let i = 0; i < 5; i++) {
          this.circles.push({ coordX: 0, coordY: 0 });
      }
      window.addEventListener('mousemove', this.handleMouseMove);
  },
  beforeUnmount() {
      window.removeEventListener('mousemove', this.handleMouseMove);
  }
}
</script>

<style scoped>
  .circle {
      position: absolute;
      z-index: 10;
      width: 40px;
      height: 40px;
      border-radius: 20px;
      background-color: rgb(245, 24, 24);
  }


</style>