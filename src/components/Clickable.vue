<template>
    <a ref="main" class="clickable" @click="click()">
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
    .clickable {
        display: flex;
        overflow: hidden;
        cursor: pointer;
        transition: opacity 5s;
        height: 200px;
        width: 200px;
        border: 1px solid black;
        border-radius: 50%;
        opacity: 1;
        box-shadow: gold 0 0 20px -5px;

        &:hover {
            background-color: white;
        }
    }

    .fade-in-full {
        opacity: 1;
    }
</style>