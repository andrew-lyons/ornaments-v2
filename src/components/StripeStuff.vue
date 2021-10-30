<template>
    <div>
        <div class="slider">
            <input type="range" min="10" max="250" step="10" v-model="amount">
            <h2>${{amount}}</h2>
        </div>

        <stripe-element-card
            ref="elementRef"
            pk="pk_live_51JoyPIIkjxKMhNqcxh1T0Q2hCvWZYGOzo75lLlh2hWGYbnnqpevNMpco6O6xhVb1sNeyTzvLHhgnzNcvNLYkxKXy005m8LgAV6"
            @token="tokenCreated"
            @error="error"
        />

        <div class="checkout">
          <a @click="submit">Submit Donation</a>
          <img :src="st" alt="">
        </div>
    </div>
</template>

<script>
import { StripeElementCard } from '@vue-stripe/vue-stripe';
import st from '../assets/02.png'

export default {
  components: {
    StripeElementCard,
  },
  data() {
    return {
      token: null,
      amount: 10,
      st: st
    };
  },
  methods: {
    submit() {
      this.$refs.elementRef.submit();
    },
    tokenCreated(params) {
      this.$emit('charge', params)
    },
    error(err) {
      console.log(err)
    }
  }
}
</script>

<style scoped lang="scss">
    .slider {
        display: flex;
        width: 100%;
        margin-bottom: 24px;
        margin-top: 36px;

        input[type=range] {
          width: 66%;
        }

        h2 {
          margin: 0 auto;
        }
    }

    .checkout {
      display: flex;
      justify-content: center;
      align-items: center;

      @media only screen and (max-width: 640px) {
        flex-wrap: wrap;
      }

      a {
        font-weight: 400;
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 8px;
        background-color: rgba(159, 212, 208, 0.75);
        cursor: pointer;
        padding: 12px 16px;
        box-shadow: grey 0px 0px 10px 2px;
        margin-right: 24px;

        transition: background-color 0.5s;

        &:hover {
          background-color: rgba(159, 212, 208, 1);
        }

        @media only screen and (max-width: 640px) {
          width: 100%;
          margin: 0 0 24px 0;
        }
      }
    }
</style>