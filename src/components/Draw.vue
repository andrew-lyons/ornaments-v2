<template>
    <div class="canvas-con">
        <canvas ref="canvasRef" height="350" width="350" />
    </div>
</template>

<script>
import hands from '../assets/hands.json'
import leftFoot from '../assets/left-foot.json'
import rightFoot from '../assets/right-foot.json'

export default {
    name: "Draw",
    data() {
        return {
            num: 1.2727
        }
    },
    methods: {
        async drawWord(json, ctx, timeDelay) {
            for (const e of json) {
                await this.draw(e, ctx, timeDelay)
            }
        },
        async draw(json, ctx, timeDelay) {
            const coords = json['a']
            const firstX = coords[0]
            const firstY = coords[1]

            ctx.lineWidth = 1
            ctx.beginPath()

            const startX = firstX[0] * this.num
            const startY = firstY[0] * this.num

            ctx.moveTo(startX, startY)

            await this.delayed(firstX, firstY, ctx, timeDelay)
        },
        async delayed(firstX, firstY, ctx, timeDelay) {
            for (let i = 0; i < firstX.length; i++) {
                const nextX = firstX[i] * this.num
                const nextY = firstY[i] * this.num
                ctx.lineTo(nextX, nextY)
                ctx.stroke()
                await this.timer(timeDelay)
            }
        },
        async timer(ms) { 
            return new Promise(res => setTimeout(res, ms))
        }
    },
    mounted() {
        setTimeout(async() => {
            const canvas = this.$refs.canvasRef
            const ctx = canvas.getContext("2d")

            this.drawWord([rightFoot, leftFoot, hands], ctx, 10)
        }, 250)
    }
}
</script>

<style scoped>
.canvas-con {
    width: 100%;
    text-align: center;
}

canvas {
    padding: 25px 0px 25px 0px
}

</style>