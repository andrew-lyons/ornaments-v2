<template>
  <div>
    <main class="page">
      <div ref="bg" class="background" />
      <transition name="fader" mode="out-in">
        <div class="container" key="uno" v-if="!active">
          <div class="container-column-mid mobile">
            <Draw />

            <div class="blurb" ref="blurbm">
              <h1>Hello! We're so glad you're here.</h1>
              <h3>Click any of the ornaments for more pictures and personalizations.</h3>
              <h3>If you're here to support, click the ornament with an orange halo in the bottom left.</h3>
              <h3>To read more about the purpose, click here.</h3>
            </div>
          </div>

          <div class="container-column-left">
            <Clickable 
              :identifier="1" 
              :active="selector == 1" 
              @selected="selected"
              :img="o1"
              :config="{
                name: true,
                date: true,
                dates: false,
                donatePerson: true
              }"
            />
            <Clickable 
              :identifier="2" 
              :active="selector == 2" 
              @selected="selected"
              :img="o2"
              :config="{
                name: true,
                date: false,
                dates: true,
                donatePerson: true
              }"
            />
            <Clickable 
              style="box-shadow: #dba065 0 0 30px 0;"
              :identifier="3" 
              :active="selector == 3" 
              @selected="selected"
              :img="o3"
              :config="{
                name: true,
                date: true,
                dates: false,
                donatePerson: true
              }"
            />
          </div>

          <div class="container-column-mid desktop">
            <Draw />

            <div class="blurb" ref="blurbd">
              <h1>Hello! We're so glad you're here.</h1>
              <h3>Click any of the ornaments for more pictures and personalizations.</h3>
              <h3>If you're here to support, click the ornament with an orange halo in the bottom left.</h3>
              <h3>To read more about the purpose, click here.</h3>
            </div>
          </div>
          
          <div class="container-column-right">
            <Clickable 
              :identifier="4" 
              :active="selector == 4" 
              @selected="selected"
              :img="o4"
              :config="{
                name: true,
                date: true,
                dates: false,
                donatePerson: true
              }"
            />
            <Clickable 
              :identifier="5" 
              :active="selector == 5" 
              @selected="selected"
              :img="o5"
              :config="{
                name: true,
                date: false,
                dates: true,
                donatePerson: true
              }"
            />
            <Clickable 
              :identifier="6" 
              :active="selector == 6" 
              @selected="selected"
              :img="o6"
              :config="{
                name: true,
                date: true,
                dates: false,
                donatePerson: true
              }"
            />
          </div>
        </div>
        <div class="container" key="dos" v-else >
          <div class="container-form">
            <div class="container-form-image">
              <img class="container-form-image-img" :src="selectedImage" alt="">
              <h3>Here would be a stipulation or explanation point etc. e a stipulation or here is another explanation point etc.</h3>
              <h3>Here would be a stipulation or explanation point etc.</h3>
              <h3>Here would be a stipulation or explanation point etc.</h3>
              <h3>Here would be a stipulation or explanation point etc.</h3>
              <h3>Here would be a stipulation or explanation point etc.</h3>
            </div>

            <Form :curId="selector" />
          </div>
        </div>
      </transition>
    </main>
  </div>
</template>

<script>
import Draw from './components/Draw.vue'
import Clickable from './components/Clickable.vue'
import Form from './components/Form.vue'
import o1 from './assets/ornaments/1/circle.svg'
import o2 from './assets/ornaments/2/circle.svg'
import o3 from './assets/ornaments/3/circle.svg'
import o4 from './assets/ornaments/4/circle.svg'
import o5 from './assets/ornaments/5/circle.svg'
import o6 from './assets/ornaments/6/circle.svg'

export default {
  name: 'App',
  components: { Draw,  Clickable, Form },
  data() {
    return {
      selector: 0,
      selectedImage: '',
      cardNum: 0,
      o1: o1,
      o2: o2,
      o3: o3,
      o4: o4,
      o5: o5,
      o6: o6
    }
  },
  methods: {
    selected(arr) {
      this.selector = arr[0].id
      this.selectedImage = arr[0].src
    }
  },
  computed: {
    active() {
      return this.selector > 0 
    }
  },
  mounted() {
    setTimeout(() => {
      this.$refs.bg.classList.add('fade-in')
      this.$refs.blurbd.classList.add('visible')
      this.$refs.blurbm.classList.add('visible')
    }, 250)
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

  hr {
    width: 90%;
    border-radius: 2px;
  }

  .fader-enter-active, .fader-leave-active {
    transition: opacity .5s;
  }

  .fader-enter, .fader-leave-to /* .fade-leave-active below version 2.1.8 */ {
    opacity: 0;
  }

</style>

<style scoped lang="scss">
  .desktop {
    @media only screen and (max-width: 1024px) {
      display: none !important;
    }
  }

  .mobile {
    @media only screen and (min-width: 1025px) {
      display: none !important;
    }
  }

  .page {
    position: relative;
    width: 100vw;
    height: 100%;
  }

  .container {
    display: flex;
    flex-wrap: nowrap;
    justify-content: center;
    height: 100%;
    min-height: 100vh;

    @media only screen and (max-width: 1024px) {
      flex-wrap: wrap;
    }

    &-column {
      &-left, &-right, &-mid {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
        align-items: center;
      }

      &-left, &-right {
        margin-left: auto;
        margin-right: auto;
        width: 25%;
        align-content: space-between;
        padding: 50px 25px;

        @media only screen and (max-width: 1024px) {
          width: 100%;
          align-content: unset;
          flex-wrap: nowrap;
        }
      }
      
      &-mid {
        width: 50%;
        align-content: flex-start;

        @media only screen and (max-width: 1024px) {
          width: 100%;
        }
      }
    }

    &-form {
      width: 100%;
      display: flex;

      @media only screen and (max-width: 1024px) {
          flex-wrap: wrap;
      }

      &-image {
        width: 50%;
        margin: auto;
        text-align: center;

        @media only screen and (max-width: 1024px) {
            margin-top: 50px;
            width: 100%;
        }

        &-img {
          margin-bottom: 50px;
          
          @media only screen and (max-width: 640px) {
            width: 80vw;
          }
        }

        h3 {
          margin: 0 50px;
        }
      }
    }
  }

  .background {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-image: url('./assets/treeline.jpg');
    background-size: cover;
    background-position: 0% 40%;
    background-repeat: no-repeat;
    opacity: 0;
    z-index: -100;
    transition: opacity 15s;
  }

  .fade-in {
    opacity: 0.25;
  }

  h1 {
    font-weight: 300;
    font-size: 36px;
  }

  h2 {
    font-weight: 400;
    font-size: 24px;
  }

  .blurb {
    text-align: center;
    opacity: 0;
    transition: opacity 2s;

    h3 {
      margin: 12px 0;
    }

    &.visible {
      opacity: 1;
    }
  }
</style>
