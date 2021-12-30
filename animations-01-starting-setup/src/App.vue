<template>
  <router-view v-slot="slotProps">
    <transition name="fade-btn" mode="out-in">
      <component :is="slotProps.Component"></component>
    </transition>
  </router-view>
</template>  

<script>
export default {
  data() {
    return {
      animatiBlocko: false,
      dialogIsVisible: false,
      paraIsVisible: false,
      usasRvisibo: false,
      enterInterval: null,
      leaveInterval: null,
    };
  },
  methods: {
    beforeIngia(el) {
      console.log('Before Enter');
      console.log(el);
      el.style.opacity = 0;
    },
    ingiRa(el, done) {
      console.log('Enta');
      console.log(el);
      let round = 1;
      this.enterInterval = setInterval(() => {
        el.style.opacity = round * 0.01;
        round++;
        if (round > 100) {
          clearInterval(this.enterInterval);
          done();
        }
      }, 20);
    },

    beforeToka(el) {
      console.log('Before Toka');
      console.log(el);
      el.style.opacity = 1;
    },
    leave(el, done) {
      console.log('Leave');
      console.log(el);
      let round = 1;
      this.leaveInterval = setInterval(() => {
        el.style.opacity = 1 - round * 0.01;
        round++;
        if (round > 100) {
          clearInterval(this.leaveInterval);
          done();
        }
      }, 20);
    },
    afterLeave(el) {
      console.log('After Leave');
      console.log(el);
    },
    afterEnter(el) {
      console.log('After enter');
      console.log(el);
    },

    enterCancelled(el) {
      console.log('Enter cancel');
      console.log(el);
      clearInterval(this.enterInterval);
    },

    leaveCancelled(el) {
      console.log('Leave Cancel');
      console.log(el);
      clearInterval(this.leaveInterval);
    },

    showUsa() {
      this.usasRvisibo = true;
    },
    haidUsa() {
      this.usasRvisibo = false;
    },
    paraVisibility() {
      this.paraIsVisible = !this.paraIsVisible;
    },
    animateBlock() {
      this.animatiBlocko = true;
    },
    showDialog() {
      this.dialogIsVisible = true;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
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
  /* transition: transform 1.2s ease-out; */
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
  /* transform: translateX(-150px); */
  animation: slide-fade 2s ease-in-out forwards;
}

.fade-btn-enter-from,
.fade-btn-leave-to {
  opacity: 0;
}
.fade-btn-enter-active {
  transition: opacity 0.4s ease-in;
}

.fade-btn-leave-active {
  transition: opacity 0.4s ease-out;
}

.fade-btn-enter-to,
.fade-btn-leave-from {
  opacity: 1;
}

.route-enter-active {
  animation: slide-fade 0.8s ease-out;
}

.route-leave-active {
  animation: slide-fade 0.8s ease-in;
}

@keyframes slide-fade {
  0% {
    transform: translateX(0) scale(1);
  }

  70% {
    transform: translateX(-120px) scale(1.2);
  }

  100% {
    transform: translateX(-150px) scale(0.7);
  }
}
</style>