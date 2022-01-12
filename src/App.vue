<template>
  <main>
    <h1>Welcome</h1>
    <div class="red-orb" />
    <div class="teal-orb" />
    <div class="gold-orb" />
    <div class="green-orb" />
    <div class="purple-orb" />
  </main>
</template>

<script>

if (!("scrollBehavior" in document.documentElement.style)) {
  import("scroll-behavior-polyfill");
}

export default {
  name: 'App',
  data() {
    return {
      
    }
  },
  methods: {},
  computed: {},
  mounted() {

  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@300;400;500&display=swap');  

  html, body {
    margin: 0;
    font-family: 'Quicksand', sans-serif;
    overflow-x: hidden;
  }

  html, body, main {
    background: #131126;
  }

</style>

<style scoped lang="scss">
  main {
    position: relative;
    height: 100vh;
    width: 100vw;
    overflow: hidden;

    --red-top: 15vh;
    --red-left: 39vw;
    --red-size: 24.3vw;
    --red-filter: blur(75px);
    --red-transform: rotate(95deg);

    --teal-top: 46vh;
    --teal-left: 36vw;
    --teal-size: 17.7vw;
    --teal-filter: blur(60px);
    --teal-transform: rotate(91deg);

    --gold-top: 32vh;
    --gold-left: 50vw;
    --gold-size: 16.8vw;
    --gold-filter: blur(60px);
    --gold-transform: rotate(40deg);

    --green-top: 41vh;
    --green-left: 50vw;
    --green-size: 16.8vw;
    --green-filter: blur(37px);
    --green-transform: rotate(98deg);

    --purple-top: 42vh;
    --purple-left: 52vw;
    --purple-size: 23.4vw;
    --purple-filter: blur(40px);
    --purple-transform: rotate(110deg);
  }

  .red-orb {
    position: absolute;
    top: var(--red-top);
    left: var(--red-left);
    width: var(--red-size);
    height: var(--red-size);
    filter: var(--red-filter);
    transform: var(--red-transform);
    background: #FF4400;
    mix-blend-mode: screen;
    border-radius: 42%;
  }

  .teal-orb {
    position: absolute;
    top: var(--teal-top);
    left: var(--teal-left);
    width: var(--teal-size);
    height: var(--teal-size);
    filter: var(--teal-filter);
    transform: var(--teal-transform);
    background: radial-gradient(217.68% 217.68% at 27.97% 49.05%, #5AE9FD 0%, rgba(90, 233, 253, 0) 100%);
    mix-blend-mode: screen;
    border: 20.8557px solid #00E29A;
    border-radius: 177.496px;
  }

  .gold-orb {
    position: absolute;
    top: var(--gold-top);
    left: var(--gold-left);
    width: var(--gold-size);
    height: var(--gold-size);
    filter: var(--gold-filter);
    transform: var(--gold-transform);
    background: conic-gradient(from 180deg at -3.84% 155.69%, #FFE072 0deg, rgba(255, 216, 75, 0) 360deg);
    mix-blend-mode: screen;
    border-radius: 243.066px;
  }

  .green-orb {
    position: absolute;
    top: var(--green-top);
    left: var(--green-left);
    width: var(--green-size);
    height: var(--green-size);
    filter: var(--green-filter);
    transform: var(--green-transform);
    background: radial-gradient(50% 50% at -50% -35.62%, #38FF70 0%, rgba(74, 224, 116, 0.65) 100%);
    mix-blend-mode: screen;
    border-radius: 197.628px;
  }

  .purple-orb {
    position: absolute;
    top: var(--purple-top);
    left: var(--purple-left);
    width: var(--purple-size);
    height: var(--purple-size);
    filter: var(--purple-filter);
    transform: var(--purple-transform);
    background: radial-gradient(158.99% 50% at 50% 132.15%, #8B78FF 0%, rgba(99, 73, 255, 0.37) 100%);
    mix-blend-mode: screen;
    border-radius: 218.305px;
  }
</style>
