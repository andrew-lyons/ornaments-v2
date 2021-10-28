<template>
  <div>
    <div ref="bg" class="background" />

    <main class="page">
      <transition name="fader" mode="out-in">
        <div class="container" key="uno" v-if="!active">
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

          <div class="container-column-mid">
            <Draw />

            <div class="blurb" ref="blurb">
              <h1>
                Hello! We're so glad you're here.
              </h1>

              <h2>
                Click any of the ornaments for more pictures and personalizations.
              </h2>
              
              <h2>
                If you're here to support, click the ornament with an orange halo in the bottom left.
              </h2>

              <h2>
                To read more about the purpose, click here.
              </h2>
              <!-- <span>
                Hello! My husband, Andrew, and I recently lost our first baby, Nora Marjorie, in October of this year. Our family got a tree for the Holiday Tree Walk held in Marietta, Ohio at East Muskingum Park, in memory of Nora. I thought that it would be great to honor other babies gone too soon as well. I decided to offer ornaments in memory of these babies that will be displayed on the tree all through December for everyone to acknowledge and celebrate. All proceeds/donations will go to Sufficient Grace Ministries (https://sufficientgraceministries.org), the organization that blessed us with professional pictures of Nora and other resources.
              </span>

              <span>
                Once the Tree Walk is over in January, you will get to keep the personalized ornament via either pick up or mail. If you have not lost a baby yourself but would like to donate to this cause, we appreciate you! We would love to add a special ornament to recognize that you support us and our sweet babies (See the special ornament for this).
              </span> -->
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
              <h2>Here would be a stipulation or explanation point etc. e a stipulation or here is another explanation point etc.</h2>
              <h2>Here would be a stipulation or explanation point etc.</h2>
              <h2>Here would be a stipulation or explanation point etc.</h2>
              <h2>Here would be a stipulation or explanation point etc.</h2>
              <h2>Here would be a stipulation or explanation point etc.</h2>
            </div>

            <Form />
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
      console.log(this.$refs.blurb)
      this.$refs.bg.classList.add('fade-in')
      this.$refs.blurb.classList.add('visible')
    }, 250)
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@300;400;500&display=swap');  

  html, body {
    margin: 0;
    font-family: 'Quicksand', sans-serif;
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
  .page {
    /* background-color: #355e3b; */
    height: 100vh;
    width: 100vw;
    overflow: hidden;
  }

  .container {
    display: flex;
    flex-wrap: nowrap;
    justify-content: center;
    height: 100%;

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
      }
      &-mid {
        align-content: flex-start;
        width: 50%;
      }
    }

    &-form {
      width: 100%;
      display: flex;

      &-image {
        width: 50%;
        margin: auto;
        text-align: center;

        &-img {
          margin-bottom: 50px;
        }

        h2 {
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
    background-size: 140%;
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

    &.visible {
      opacity: 1;
    }
  }
</style>
