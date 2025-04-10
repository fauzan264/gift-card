<script setup>
import { watch, onMounted, ref, defineProps, nextTick } from 'vue'

const props = defineProps(['dear', 'message', 'from', 'imageFile'])
const canvasRef = ref(null)
const image = new Image()

defineExpose({
    getCanvas: () => canvasRef.value
})

const draw = () => {
    const canvas = canvasRef.value
    if (!canvas) return

    const ctx = canvas.getContext('2d')
    if (!ctx) return

    canvas.width = image.width
    canvas.height = image.height

    ctx.clearRect(0, 0, canvas.width, canvas.height)
    ctx.drawImage(image, 0, 0)

    ctx.font = '24px "Dancing Script", cursive'
    ctx.fillStyle = '#5A4231'
    ctx.fillText(props.dear, 300, 220, 180)

 // ⬇️ Draw multiline message
    const lines = props.message.split('\n')
    const startY = 270
    const lineHeight = 55
    lines.forEach((line, i) => {
        ctx.fillText(line, 200, startY + i * lineHeight)
    })
    
    ctx.fillText(props.from, 280, 380, 200)
}

onMounted(() => {
    image.onload = draw
    image.src = '/gift-template.jpg'
})

watch(() => props.imageFile, (file) => {
    if (!file) return
    const reader = new FileReader()
    reader.onload = () => {
        image.src = reader.result
    }
    reader.readAsDataURL(file)
})

watch(() => [props.dear, props.message, props.from], () => nextTick(draw))
</script>

<template>
    <canvas ref="canvasRef" class="w-full border rounded shadow"></canvas>
</template>
