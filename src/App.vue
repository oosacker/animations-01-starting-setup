<template>

  <!-- animation container -->
  <div class="container">
    <div class="block" :class="{animate: animatedBlock}"></div>
    <button @click="animateBtnHandler()">Animate</button>
  </div>

  <div class="container">
    <!-- adding transision for vue animation -->
    <!-- para is class name prefix -->
    <transition name="para">
      <!-- v-if will mount and unmount depending on state -->
      <p v-if="paraVisible">Sometimes visible</p>
    </transition>
    <button @click="paraToggleBtnClick()">Toggle paragraph</button>
  </div>

  <base-modal @close="hideDialog" v-if="dialogIsVisible">
    <p>This is a test dialog!</p>
    <button @click="hideDialog">Close it!</button>
  </base-modal>

  <div class="container">
    <button @click="showDialog">Show Dialog</button>
  </div>
</template>  

<script>
export default {
  data() {
    return { 
      dialogIsVisible: false,
      animatedBlock: false,
      paraVisible: false
    };
  },
  methods: {
    showDialog() {
      this.dialogIsVisible = true;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
    animateBtnHandler() {
      this.animatedBlock = !this.animatedBlock;
    },
    paraToggleBtnClick() {
      this.paraVisible = !this.paraVisible;
    }
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}
button {
  font: inherit;
  padding: 0.5rem 2rem;
  border: 1px solid #810032;
  border-radius: 30px;
  background-color: #810032;
  color: white;
  cursor: pointer;
}
button:hover,
button:active {
  background-color: #a80b48;
  border-color: #a80b48;
}
.block {
  width: 8rem;
  height: 8rem;
  background-color: #290033;
  margin-bottom: 2rem;

  /* the transition effect applies to transform lasting 0.5s */
  /* transition: transform 0.5s ease-in; */
}
.container {
  max-width: 40rem;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 2px solid #ccc;
  border-radius: 12px;
}
.animate {
  /* transform: translateX(-60px); */

  /* custom animations slow end, don't restart when finished */
  animation: slide-fade 1s ease-out forwards;
}

/* describe animation frames for box */
@keyframes slide-fade {
  0% {
    transform: translateX(0) scale(1);
  }
  50% {
    transform: translateX(-100px) scale(1.2);
  }
  100% {
    transform: translateX(-150px) scale(1);
  }
}

/* vue transition classes for adding the paragraph  */
.para-enter-from {
  opacity: 0;
  transform: translateY(-30px);
}
.para-enter-active {
  transition: all 0.3s ease-in;
}
.para-enter-to {
  opacity: 1;
  transform: translateY(0);
}

/* vue transition classes for removing the paragraph  */
.para-leave-from {
  opacity: 1;
  transform: translateY(0);
}
.para-leave-active {
  transition: all 0.3s ease-out;
}
.para-leave-to {
  opacity: 0;
  transform: translateY(-30px);
}
</style>