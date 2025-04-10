<script setup>
const emit = defineEmits(['file-selected'])

const onChange = (e) => {
    const file = e.target.files[0]
    if (file) emit('file-selected', file)
}
</script>

<template>
    <input type="file" @change="onChange" accept="image/*" class="block w-full border p-2 rounded" />
</template>

<style scoped>
</style>
