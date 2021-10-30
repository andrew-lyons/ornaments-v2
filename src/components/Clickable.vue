<template>
    <a
        ref="main"
        :class="identifier == 3
                    ? 'last'
                    : identifier == 6
                        ? 'last'
                        : ''"
        class="clickable"
        @click="click()"
    >
        <!-- <svg class="outline" viewBox="0 0 100 100">
            <circle cx="50" cy="50" r="50"/>
        </svg> -->
        <img :src="img" alt="" ref="image" :id="identifier">
    </a>
</template>

<script>
export default {
    name: "Clickable",
    props: {
        identifier: { type: Number,  required: true },
        active:     { type: Boolean, required: true },
        img:        { required: false               },
        config:     { type: Object, required: false }
    },
    methods: {
        click() {
            this.$emit('selected', [this.$refs.image, this._props.config])
        }
    },
    mounted() {
        // setTimeout(() => {
        //     this.$refs.main.classList.add('fade-in-full')
        // }, 5000)
    }
}
</script>

<style lang="scss" scoped>
    .outline {
        position: absolute;
        width: 14vw;
        height: 14vw;
        z-index: -10;
        fill: none;
        stroke: blue;
    }

    .clickable {
        display: flex;
        overflow: hidden;
        cursor: pointer;
        transition: opacity 5s;
        height: 14vw;
        width: 14vw;
        border: 1px solid black;
        border-radius: 50%;
        opacity: 1;
        box-shadow: gold 0 0 20px -5px;

        &:hover {
            background-color: white;
        }

        img {
            max-width: 100%;
            max-height: 100%;
        }

        @media only screen and (max-width: 1024px) {
            height: 25vw;
            width: 25vw;
            margin: 0 25px;
        }

        @media only screen and (max-width: 640px) {
            height: 40vw;
            width: 40vw;
            margin: 0 15px;
        }
    }

    .fade-in-full {
        opacity: 1;
    }
</style>