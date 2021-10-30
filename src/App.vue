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
              <h3>If you're here to honor your baby, click any of the ornaments for more pictures and personalizations.</h3>
              <h3>If you're here to support, click the ornament with the blue halo.</h3>
              <h3>To read more about the purpose, <a class="bt" @click="scrollRead()">click here.</a></h3>
            </div>
          </div>

          <div class="container-column-left">
            <Clickable 
              delay="4s"
              :identifier="1" 
              :active="selector == 1" 
              @selected="selected"
              :img="images[1][0]"
              :config="{
                name: true,
                date: true,
                dates: false,
                donatePerson: true
              }"
            />
            <Clickable
              delay="5s"
              :identifier="2" 
              :active="selector == 2" 
              @selected="selected"
              :img="images[2][0]"
              :config="{
                name: true,
                date: false,
                dates: true,
                donatePerson: true
              }"
            />
            <Clickable
              delay="6s"
              style="box-shadow: blue 0 0 30px -10px;"
              class="sixf"
              :identifier="3" 
              :active="selector == 3" 
              @selected="selected"
              :img="images[3][0]"
              :config="{
                name: true,
                date: true,
                dates: false,
                donatePerson: true
              }"
            />
          </div>

          <div class="container-column-left sixd">
            <Clickable
              delay="4s"
              style="box-shadow: blue 0 0 30px -10px;"
              :identifier="3" 
              :active="selector == 3" 
              @selected="selected"
              :img="images[3][0]"
              :config="{
                name: true,
                date: true,
                dates: false,
                donatePerson: true
              }"
            />
            <Clickable
              delay="5s"
              :identifier="4" 
              :active="selector == 4" 
              @selected="selected"
              :img="images[4][0]"
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
              <h3>If you're here to honor your baby, click any of the ornaments for more pictures and personalizations.</h3>
              <h3>If you're here to support, click the ornament with the blue halo.</h3>
              <h3>To read more about the purpose, <a class="bt" @click="scrollRead()">click here.</a></h3>
            </div>
          </div>
          
          <div class="container-column-right">
            <Clickable
              class="sixf"
              delay="6s"
              :identifier="4" 
              :active="selector == 4" 
              @selected="selected"
              :img="images[4][0]"
              :config="{
                name: true,
                date: true,
                dates: false,
                donatePerson: true
              }"
            />
            <Clickable
              delay="3s"
              :identifier="5" 
              :active="selector == 5" 
              @selected="selected"
              :img="images[5][0]"
              :config="{
                name: true,
                date: false,
                dates: true,
                donatePerson: true
              }"
            />
            <Clickable
              delay="4s"
              :identifier="6" 
              :active="selector == 6" 
              @selected="selected"
              :img="images[6][0]"
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
          <a class="backarrow" @click="selector = 0; opacity()">
            <svg viewBox="0 0 39.446224 31.030203" height="31.030203" width="39.446224">
              <g>
                <path
                  d="m 14.656952,30.835576 c -0.224941,-0.123103 -2.716842,-2.558809 -7.1674311,-7.0058 -3.752433,-3.749399 -6.85588096,-6.81715 -6.89655296,-6.817226 -0.04067,-7.5e-5 -0.174181,-0.158787 -0.296688,-0.352694 -0.176925,-0.280037 -0.229899,-0.465216 -0.257535,-0.900247 -0.07069,-1.112723 -0.684935,-0.40499 7.20690896,-8.3037468 5.2517961,-5.256396 7.1560641,-7.116129 7.4344021,-7.260536 0.767958,-0.398431 1.735802,-0.172797 2.335336,0.544439 0.55363,0.662318 0.624101,1.467849 0.193481,2.21162 -0.0488,0.08429 -2.423095,2.485824 -5.276207,5.336739 -3.0383451,3.0360058 -5.1657861,5.2185798 -5.1351191,5.2681988 0.03796,0.06142 4.3592191,0.08472 15.7160031,0.08472 h 15.663645 l 0.289687,0.160497 c 0.754166,0.417834 0.979342,0.830213 0.979342,1.793526 0,0.627933 -0.01973,0.720849 -0.220509,1.038205 -0.25856,0.408692 -0.639558,0.687025 -1.120487,0.818554 -0.267574,0.07318 -3.798777,0.09464 -15.761761,0.09579 -8.479313,8.12e-4 -15.4342351,0.02947 -15.4553801,0.06369 -0.02115,0.03421 2.239131,2.335938 5.0228361,5.114942 2.783705,2.779004 5.135178,5.15597 5.225495,5.282146 0.349576,0.488372 0.439309,1.063257 0.259998,1.665701 -0.11111,0.373304 -0.889067,1.208336 -1.125746,1.208336 -0.0818,0 -0.170046,0.03448 -0.196093,0.07663 -0.02605,0.04215 -0.278083,0.07407 -0.560078,0.07093 -0.392958,-0.0044 -0.593264,-0.04977 -0.857547,-0.194406 z"
                  style="fill:#000000;stroke-width:0.0766283" />
              </g>
            </svg>
          </a>

          <div class="container-form">
            <div class="container-form-image">
              <ImageCarousel :img="images[selector]" />
              <h3 style="margin-top: 6px;">
                Please note that the ornaments will be displayed at the Marietta, Ohio Holiday Tree Walk 
                through the month of December. We will send/offer pick up for the ornaments after the Tree Walk is over.
              </h3>
              <h3 style="margin-top: 6px; margin-bottom: 6px;">These ornaments are 4 inch acrylic discs with personalized engraving.</h3>
              <h3>All donations from this effort will go to Sufficient Grace Ministries.</h3>
            </div>

            <Form :curId="selector" />
          </div>
        </div>
      </transition>
    </main>
    <main id="readmore" v-if="!active">
      <div class="bg" />
      <div class="readmore-text">
        <h3>
          Hello! My husband, Andrew, and I recently lost our first baby, Nora Marjorie, 
          in October of this year. It was the hardest thing that we have ever been through. 
          We have realized since, that pregnancy loss and baby loss continues to be a taboo 
          subject in our world. We hope to increase awareness in honor of our sweet Nora, and 
          recognize the realness of your baby's life, even though they are no longer here with you.
        </h3>

        <h3>
          Our family got a tree for the Holiday Tree Walk held in Marietta, Ohio at East Muskingum Park, 
          in memory of Nora. I have found so much community with those who have shared their stories of 
          loss with me, and I thought that it would be great to honor other babies gone too soon as well. 
          I decided to offer ornaments in memory of these babies that will be displayed on the tree all 
          through December for everyone to acknowledge and celebrate. All proceeds/donations will go to 
          Sufficient Grace Ministries (<a class="bt" href="https://sufficientgraceministries.org">Link To Site</a>), the organization that blessed 
          us with professional pictures of Nora, a perfectly sized gown and hat for her, and other resources. 
        </h3>

        <h3>
          We are so sorry for your loss, but we want to honor your sweet babies. Once the Tree Walk is over in 
          January, you will get to keep the personalized ornament via either pick up or mail. If you have not 
          lost a baby yourself but would like to donate to this cause, we appreciate you! We would love to add a 
          special ornament to recognize that you support us and our sweet babies (See the "we stand with you" ornament).
        </h3>
      </div>
    </main>
  </div>
</template>

<script>
import Draw from './components/Draw.vue'
import Clickable from './components/Clickable.vue'
import Form from './components/Form.vue'
import ImageCarousel from './components/ImageCarousel.vue'
import o1 from './assets/10.svg'
import o2 from './assets/20.svg'
import o3 from './assets/30.svg'
import o4 from './assets/40.svg'
import o5 from './assets/50.svg'
import o6 from './assets/60.svg'

if (!("scrollBehavior" in document.documentElement.style)) {
  import("scroll-behavior-polyfill");
}

export default {
  name: 'App',
  components: { Draw,  Clickable, Form, ImageCarousel },
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
      o6: o6,
      images: [
        '00_cDJ9okgQj.jpg',
        [o1, '11_h-uwlPMVy.png', '12_pzwfqxw9TRk.png'],
        [o2, '21_oNzK9t_hZ.png', '22_t5tB8SeqS.png'],
        [o3, '31_G1ZkMaNmM.png', '32_kBxbYJO1K.png'],
        [o4, '41_xKzgqavPoG.png', '42_W_WEelCwi.png'],
        [o5, '51_X5BphHAuoYm.png', '52_K1cFjEh3f.png'],
        [o6, '61_Qt7vgxiY7.png', '62_TkFr0z6s_X5.png']
      ]
    }
  },
  methods: {
    selected(arr) {
      this.selector = arr[0].id
      this.selectedImage = arr[0].src
    },
    opacity() {
      this.$refs.bg.classList.add('fade-in')
    },
    scrollRead() {
      window.scrollTo({top: document.getElementById('readmore').getBoundingClientRect().top, behavior: 'smooth'})
    }
  },
  watch: {
    // whenever question changes, this function will run
  selector: function () {
      window.scrollTo({ top: 0, left: 0 })
    }
  },
  computed: {
    active() {
      return this.selector > 0 
    }
  },
  mounted() {
    setTimeout(() => {
      // this is the first time
      if (!localStorage.noFirstVisit) {
          // show the element
          // and do the animation you want
          this.$refs.bg.classList.add('transf')

          // check this flag for escaping this if block next time
          localStorage.noFirstVisit = true;
      }

      this.opacity()
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

  .sixf {
    @media only screen and (max-width: 640px) {
      display: none !important;
    }
  }

  .sixd {
    @media only screen and (min-width: 641px) {
      display: none !important;
    }
  }

  .bt {
    color: gray;
    cursor: pointer;
    text-decoration: underline;
  }

  #readmore {
    padding: 100px 300px;
    min-height: 600px;
    position: relative;

    @media only screen and (max-width: 1024px) {
      min-height: 800px;
      padding: 50px 100px;
    }

    @media only screen and (max-width: 640px) {
      padding: 24px 75px;
      min-height: 1000px;
    }

    .bg {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-image: url('./assets/03.jpg');
      background-size: cover;
      background-position: 0% 40%;
      background-repeat: no-repeat;
      opacity: 0.35;
      z-index: -100;
    }
  }

  .backarrow {
    position: fixed;
    top: 16px;
    left: 16px;
    width: 75px;
    height: 50px;
    z-index: 1000;
    cursor: pointer;
    background-color: white;
    opacity: 0.75;
    transition: opacity 0.75s;
    border-radius: 25%;
    box-shadow: black 2px 2px 10px -4px;
    display: flex;
    justify-content: center;
    align-items: center;

    &:hover {
      opacity: 1;
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

        @media only screen and (max-width: 640px) {
          padding: 25px;
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

  .transf {
    transition: opacity 15s;
  }

  .transt {
    transition: opacity 2s;
  }

  .background {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-image: url('./assets/00.jpg');
    background-size: cover;
    background-position: 0% 40%;
    background-repeat: no-repeat;
    opacity: 0;
    z-index: -100;
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

    h3 {
      margin: 12px 0;
    }
  }
</style>
