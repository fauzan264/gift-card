<script setup>
const emit = defineEmits(['download'])
</script>

<template>
    <div class="flex justify-center">
        <button @click="$emit('download')" class="bg-green-500 text-white w-50 px-8 py-2 rounded hover:bg-green-600">
            Download
        </button>
    </div>
</template>
