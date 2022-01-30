<template>
  <main>
    <div class="bodytext">
      <h1 class="bodytext-title">Welcome</h1>
      <h2 class="bodytext-subtitle">This year, we honored 150 babies and donated $2,500 to Pregnancy + Infant Loss organization Sufficient Grace Ministries.</h2>
      <div class="bodytext-list">
        <h2>To combat P+I Loss stigma, and to help provide for those who need it, we are working on:</h2>
        <ul>
          <li>An online store for P+I Loss memorials and gifts</li>
          <li>A community hub for support groups, and more</li>
          <li>A resource guide for podcasts, books, and more</li>
          <li>An organization directory for businesses and non-profits that can help or provide support</li>
          <li>Faith-based options for all the above</li>
          <li>And much more!</li>
        </ul>
      </div>

      <div class="bodytext-inputs">
        <div class="bodytext-inputs-text">
          <h2>If you want to keep in touch...</h2>
          <h4>(We don't send spam emails, promise!)</h4>
        </div>
        <div class="bodytext-inputs-submit">
          <div class="bodytext-inputs-submit-input">
            <input class="input-1" type="text" placeholder="Drop your email for updates!">
            <input type="text" placeholder="Send us a message. (Optional)">
          </div>

          <div class="bodytext-inputs-submit-button">
            <a href="" class="bodytext-inputs-submit-button-submitEmail">Submit</a>
          </div>
        </div>
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
  
  html, body, input {
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
    align-content: space-between;
    position: relative;
    z-index: 10;
    width: 45%;
    padding: 50px;
    color: rgb(42, 59, 80);

    @media (max-width: 1440px) {
      padding: 100px 50px;
    }

    @media (max-width: 1366px) {
      padding: 50px;
    }

    @media (max-width: 1024px) {
      width: 100%;
      padding: 25px;
    }

    @media (min-width: 1800px) {
      padding: 100px 50px;
    }

    &-title {
      margin: 0 0 12px 0;
      font-size: 36px;
      line-height: 36px;

      @media (min-width: 1536px) {
        font-size: 48px;
        line-height: 48px;
      }

      @media (min-width: 1800px) {
        font-size: 56px;
        line-height: 64px;
      }

      @media (max-width: 1024px) {
        font-size: 30px;
        line-height: 30px;
      }
    }

    &-subtitle {
      margin: 0 0 12px 0;

      @media (min-width: 1536px) {
        font-size: 32px;
        line-height: 36px;
      }
    }

    &-list {
      h2 {
        margin-top: 0;
        margin-bottom: 12px;

        @media (min-width: 1536px) {
          font-size: 32px;
          line-height: 36px;
        }
      }

      ul {
        margin-top: 0;
      }

      li {
        font-size: 16px;
        line-height: 24px;

        @media (min-width: 1536px) {
          font-size: 20px;
          line-height: 34px;
        }
      }

      li::marker {
        color: #2a3b50;
      }
    }

    &-inputs {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;

      &-text {
        h2, h4 {
          margin: 0;
        }

        h2 {
          @media (min-width: 1536px) {
            font-size: 32px;
            line-height: 32px;
          }
        }

        h4 {
          font-style: italic;
        }

        margin-bottom: 24px;
      }

      &-submit {
        display: flex;
        flex-wrap: nowrap;
        width: 100%;
        justify-content: space-evenly;

        &-input {
          display: flex;
          flex-wrap: wrap;

          input {
            width: calc(100% - 12px);
            padding: 12px 0 12px 12px;
            border: none;
            border-radius: 6px;
            box-shadow: 2px 3px 3px 1px #2a3b50;
            font-size: 16px;
            line-height: 20px;
          }

          .input-1 {
            margin-bottom: 12px;

            @media (max-width: 1024px) {
              margin-top: 12px;
            }
          }
        }

        &-button {
          display: flex;
          align-items: center;

          &-submitEmail {
            font-size: 24px;
            line-height: 24px;
            text-decoration: none;
            color: #2a3b50;
            padding: 24px;
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

          @media (max-width: 1024px) {
            margin-top: 24px;
          }
        }
      }
    }
  }

  .lottie-main-al {
    --dim: calc(100vh * 1.136);
    width: var(--dim) !important;
    height: 100vh !important;
    margin: 0px !important;
    position: absolute;
    right: -10%;
    z-index: 9;

    @media (max-width: 1024px) {
      position: relative;
      width: 100vw !important;
    }
  }

</style>
