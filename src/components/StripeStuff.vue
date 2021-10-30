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

        <button @click="submit">Generate token</button>
    </div>
</template>

<script>
import { StripeElementCard } from '@vue-stripe/vue-stripe';
export default {
  components: {
    StripeElementCard,
  },
  data() {
    return {
      token: null,
      amount: 10
    };
  },
  methods: {
    submit() {
      // this will trigger the process
      this.$refs.elementRef.submit();
    },
    tokenCreated(params) {
      console.log(params);
      // handle the token
      // send it to your server

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
</style>