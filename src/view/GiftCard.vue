<script setup>
import { ref } from 'vue'
import GiftForm from '../components/GiftForm.vue'
import FileUpload from '../components/FileUpload.vue'
import CanvasGiftCard from '../components/CanvasGiftCard.vue'
import DownloadButton from '../components/DownloadButton.vue'

const form = ref({ dear: '', message: '', from: '' })
const imageFile = ref(null)
const canvasRef = ref(null)

const handleFile = (file) => {
    imageFile.value = file
}

const downloadImage = () => {
    const canvas = canvasRef.value?.getCanvas?.()
    if (!canvas) return
    const link = document.createElement('a')
    link.download = 'gift-card.png'
    link.href = canvas.toDataURL()
    link.click()
}
</script>

<template>
    <div class="min-h-screen bg-violet-100 flex items-center justify-center p-4">
        <div class="max-w-xl w-full bg-white p-6 rounded-2xl shadow space-y-6">
            <h1 class="text-3xl font-bold text-center">Gift Card Generator</h1>
            
            <CanvasGiftCard
                :dear="form.dear"
                :message="form.message"
                :from="form.from"
                :imageFile="imageFile"
                ref="canvasRef"
            />
            
            <FileUpload @file-selected="handleFile" />
            <GiftForm v-model:form="form" />
            <DownloadButton @download="downloadImage" />
        </div>
    </div>
</template>
