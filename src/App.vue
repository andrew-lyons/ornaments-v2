<template>
  <main>
    <div class="bodytext" :style="{ '--align-content': squareAR ? 'center' : 'space-between' }">
      <h1 class="bodytext-title">Welcome</h1>
      <h2 class="bodytext-subtitle">This year, we honored over 120 babies and donated $2,500 to Pregnancy + Infant Loss organization Sufficient Grace Ministries.</h2>
      
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
          <h2 class="bodytext-inputs-text-arrow one">^</h2>
          <h2 class="bodytext-inputs-text-arrow two">^</h2>
          <h4>(We don't send spam emails, promise!)</h4>
        </div>

        <div class="bodytext-inputs-submit">
          <div class="bodytext-inputs-submit-input">
            <input v-model="email" class="input-1" type="text" placeholder="Drop your email for updates!">
            <input v-model="msg" type="text" placeholder="Send us a message. (Optional)">
          </div>

          <div class="bodytext-inputs-submit-button">
            <a
              class="bodytext-inputs-submit-button-submitEmail"
              @click="sendMail"
            >{{userFeedback()}} {{confirmedMsg}}</a>
          </div>
        </div>
      </div>
    </div>

    <lottie
      class="lottie-main-al"
      :class="squareAR ? 'lottie-main-al-extrashift' : ''"
      :options="{ animationData: animation }"
    />
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
  metaInfo: () => ({
    title: 'Honoring Our Babies',
    htmlAttrs: {
      lang: 'en',
      amp: undefined
    },
    meta: [
      { name: 'description', content: 'Pregnancy and Infant Loss has a stigma. We want to ensure if you experience loss, you have help and support.' }
    ],
  }),
  components: {
    'lottie': Lottie
  },
  data() {
    return {
      squareAR: false,
      email: '',
      msg: '',
      sent: false,
      loading: false,
      confirmed: false,
      confirmedMsg: ''
    }
  },
  methods: {
    onResize() {
      if (window.innerWidth >= 1024) {
        this.squareAR = window.innerHeight / window.innerWidth >= 0.69;
      } else {
        this.squareAR = false;
      }
    },
    async sendMail() {
      if (this.sent) {
        return
      }
      this.sent = true;

      const body = {
        email: this.email,
        msg: this.msg
      }

      const options = {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(body)
      }

      this.loading = true;

      await fetch('https://express-nora.herokuapp.com/email', options)
      .then((res) => res.json())
      .then((res) => {
        console.log(res);
        this.loading = false;
        this.confirmed = res.ok;
        this.confirmedMsg = res.msg;
      })
      .catch((err) => {
        this.loading = false;
        this.confirmed = false;
        this.confirmedMsg = err;
        console.log('err: ', err)
      });
    },
    userFeedback() {
      if (this.sent) {
        if (this.loading) {
          return '...';
        }
        if (!this.loading && this.confirmed) {
          return '✓';
        }
        if (!this.loading && !this.confirmed) {
          return '✗';
        }
      }
      else {
        return 'Submit';
      }
    }
  },
  computed: {
    animation() {
      return animationData;
    }
  },
  mounted() {
    this.onResize();
    // Register an event listener when the Vue component is ready
    window.addEventListener('resize', this.onResize)
  },
  beforeDestroy() {
    // Unregister the event listener before destroying this Vue instance
    window.removeEventListener('resize', this.onResize)
  }
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
    display: flex;
    flex-wrap: wrap;
  }

  .bodytext {
    --h1-f: 36px;
    --h1-l: calc(var(--h1-f) + 8px);
    --h2-f: 24px;
    --h2-l: calc(var(--h2-f) + 8px);
    --li-f: 16px;
    --li-l: calc(var(--li-f) + 12px);
    --align-content: space-between;

    position: relative;
    display: flex;
    flex-wrap: wrap;
    align-content: var(--align-content);
    z-index: 10;
    width: 45%;
    padding: 50px;
    color: rgb(42, 59, 80);

    @media (max-width: 1440px) {
      padding: 50px;
    }

    @media (max-width: 1366px) {
      padding: 50px;
    }

    @media (max-width: 1024px) {
      --h1-f: 30px;
      --h2-f: 24px;
      padding: 25px 50px;
    }

    @media (max-width: 820px) {
      align-content: flex-start;
      width: 70%;
    }

    @media (max-width: 640px) {
      width: 100%;
      padding: 50px;

      --li-f: 24px;
    }

    @media (min-width: 1536px) {
      --h1-f: 48px;
      --h2-f: 32px;
      --li-f: 20px;
    }

    @media (min-width: 1800px) {
      --h1-f: 56px;
      --h2-f: 40px;
      padding: 100px 50px;
    }

    &-title {
      margin: 0 0 12px 0;
      font-size: var(--h1-f);
      line-height: var(--h1-l);
    }

    &-subtitle {
      margin: 0 0 12px 0;
      font-size: var(--h2-f);
      line-height: var(--h2-l);
    }

    &-list {
      h2 {
        margin-top: 0;
        margin-bottom: 12px;
        font-size: var(--h2-f);
        line-height: var(--h2-l);
      }

      ul {
        margin-top: 0;

        @media (max-width: 820px) {
          max-width: 66%;
        }

        @media (max-width: 640px) {
          max-width: unset;
        }
      }

      li {
        font-size: var(--li-f);
        line-height: var(--li-l);

        &::marker {
          color: #2a3b50;
        }
      }
    }

    &-inputs {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;

      @media (max-width: 820px) {
        justify-content: left;
      }

      @media (max-width: 640px) {
        justify-content: center;
      }

      &-text {
        position: relative;
        margin-bottom: 24px;

        @media (max-width: 640px) {
          text-align: center;
        }

        &-arrow {
          @media (min-width: 1025px) {
            display: none;
          }

          @media (max-width: 640px) {
            display: none;
          }

          position: absolute;
          transform: rotate(180deg);
          left: -24px;

          &.one {
            top: -6px;
          }

          &.two {
            top: 12px;
          }
        }

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
      }

      &-submit {
        display: flex;
        flex-wrap: nowrap;
        width: 100%;
        justify-content: space-evenly;

        @media (max-width: 820px) {
          justify-content: left;
          flex-wrap: wrap;
        }

        @media (max-width: 640px) {
          justify-content: center;
        }

        &-input {
          display: flex;
          flex-wrap: wrap;

          @media (max-width: 640px) {
            justify-content: center;
          }

          input {
            width: calc(100% - 12px);
            padding: 12px 0 12px 12px;
            border: none;
            border-radius: 6px;
            box-shadow: 2px 3px 3px 1px #2a3b50;
            font-size: 16px;
            line-height: 20px;
          }

          @media (max-width: 1024px) {
            max-width: 60%;
          }

          @media (max-width: 640px) {
            max-width: unset;
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
          cursor: pointer;
          transition: all .25s;

          @media (max-width: 1024px) {
            margin-top: 24px;
            margin-left: 24px;
          }

          @media (max-width: 820px) {
            width: 100%;
            margin-left: 0;
          }

          @media (max-width: 640px) {
            justify-content: center;
          }

          &-submitEmail {
            font-size: 24px;
            line-height: 24px;
            text-decoration: none;
            color: #2a3b50;
            padding: 24px;
            border-radius: 12px;
            background-color: #FFFFFF;
            transition: all .25s;
            box-shadow: 2px 3px 3px 1px #2a3b50;

            @media (max-width: 1024px) {
              padding: 12px;
            }

            &:hover {
              background-color: #2a3b50;
              color: #FFFFFF;
            }
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
    position: fixed;
    right: -10%;
    z-index: 9;

    &-extrashift {
      right: -30%;
    }

    @media (max-width: 820px) {
      right: -90%;
      bottom: -10%;
    }

    @media (max-width: 768px) {
      right: -75%;
      bottom: -10%;
    }

    @media (max-width: 640px) {
      right: -90%;
      bottom: 0;
      opacity: 0.25;
    }

    @media (max-width: 450px) {
      right: -110vw;
    }
  }

</style>
