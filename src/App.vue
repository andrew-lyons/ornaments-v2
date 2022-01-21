<template>
  <main>
    <div class="bodytext">
      <h1 class="text title">Welcome</h1>
      <h2 class="text subtitle">This year, we honored 150 babies and donated $2,500 to Pregnancy + Infant Loss organization Sufficient Grace Ministries.</h2>
      <h2 class="text">To combat P+I Loss stigma, and to help provide for those who need it, we are working on:</h2>
      <ul>
        <li>An online store for P+I Loss memorials and gifts</li>
        <li>A community hub for support groups, and more</li>
        <li>A resource guide for podcasts, books, and more</li>
        <li>An organization directory for businesses and non-profits that can help or provide support</li>
        <li>Faith-based options for all the above</li>
        <li>And much more!</li>
      </ul>

      <div class="inputs">
        <h2 class="text" style="margin: 0;">If you want to keep in touch...</h2>
        <h4 class="italic" style="margin: 0;">(We don't send spam emails, promise!)</h4>
        <input class="input-1" type="text" placeholder="Drop your email for updates!">
        <input type="text" placeholder="Send us a message. (Optional)">
      </div>
      
      <div class="button">
        <a href="" class="submitEmail">Submit</a>
      </div>
    </div>
      <lottie class="lottie-main-al" :options="defaultOptions" v-on:animCreated="handleAnimation"/>
  </main>
</template>

<script>

if (!("scrollBehavior" in document.documentElement.style)) {
  import("scroll-behavior-polyfill");
}

import Lottie from 'vue-lottie';
import animationData from './assets/json/peace.json';

export default {
  name: 'App',
  components: {
    'lottie': Lottie
  },
  data() {
    return {
      redSize: 24.3,
      tealSize: 17.7,
      goldSize: 16.8,
      greenSize: 16.8,
      purpleSize: 23.4,
      incr: 1,
      defaultOptions: {animationData: animationData},
      animationSpeed: 1
    }
  },
  methods: {
      handleAnimation(anim) {
        this.anim = anim;
      }
  },
  computed: {},
  mounted() {}
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
    background: rgb(255, 246, 217);
  }
</style>

<style scoped lang="scss">
  main {
    position: relative;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
    display: flex;

    @media (max-width: 1024px) {
      flex-wrap: wrap;
    }
  }

  .bodytext {
    display: flex;
    flex-wrap: wrap;
    align-content: flex-start;
    position: relative;
    z-index: 10;
    width: 40%;
    padding: 50px;
    color: rgb(42, 59, 80);

    @media (max-width: 1024px) {
      width: 100%;
      padding: 25px;
    }
  }

  .text {
    margin: 0 0 12px 0;
  }

  .title {
    font-size: 36px;
    line-height: 36px;

    @media (max-width: 1024px) {
      font-size: 30px;
      line-height: 30px;
    }
  }

  h2 {
    @media (max-width: 1024px) {
      font-size: 18px;
      line-height: 20px;
    }
  }

  .italic {
    font-style: italic;
  }

  .inputs {
    input {
      width: calc(100% - 12px);
      padding: 12px 0 12px 12px;
      border: none;
      border-radius: 6px;
      box-shadow: 2px 3px 3px 1px #2a3b50;
    }

    .input-1 {
      margin-top: 24px;
      margin-bottom: 12px;

      @media (max-width: 1024px) {
        margin-top: 12px;
      }
    }
  }

  ul {
    margin-top: 0;
  }

  li {
    font-size: 16px;
    line-height: 24px;
  }

  li::marker {
    color: #2a3b50;
  }

  .lottie-main-al {
    width: calc(100vh * 1.136) !important;
    height: 100vh !important;
    margin: 0px !important;
    position: absolute;
    left: 40%;
    z-index: 9;

    @media (max-width: 1024px) {
      position: relative;
      width: 100vw !important;
    }
  }

  .button {
    width: 100%;
    margin-top: 32px;

    @media (max-width: 1024px) {
      margin-top: 24px;
    }
  }

  .submitEmail {
    font-size: 24px;
    line-height: 24px;
    text-decoration: none;
    color: #2a3b50;
    padding: 12px;
    border-radius: 12px;
    background-color: #FFFFFF;
    transition: background-color 0.25s, color 0.25s;

    @media (max-width: 1024px) {
      padding: 6px 12px;
    }

    &:hover {
      background-color: #2a3b50;
      color: #FFFFFF;
    }
  }
</style>
