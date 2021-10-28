<template>
    <div>
        <div class="slider">
            Heres the slider
        </div>

        <stripe-element-card
            ref="elementRef"
            pk="pk_live_51JoyPIIkjxKMhNqcxh1T0Q2hCvWZYGOzo75lLlh2hWGYbnnqpevNMpco6O6xhVb1sNeyTzvLHhgnzNcvNLYkxKXy005m8LgAV6"
            @token="tokenCreated()"
        />

        <button @click="submit()">Generate token</button>
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
    };
  },
  methods: {
    submit() {
      // this will trigger the process
      this.$refs.elementRef.submit();
    },
    tokenCreated(token) {
      console.log(token);
      // handle the token
      // send it to your server
    },
  }
};
</script>

<style scoped lang="scss">
    .slider {
        width: 100%;
        box-shadow: black 1px 1px 1px 1px;
        margin-bottom: 24px;
        margin-top: 12px;
    }
</style>