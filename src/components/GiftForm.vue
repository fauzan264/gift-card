<script setup>
const props = defineProps(['form'])
</script>

<template>
    <div class="space-y-2">
        <input v-model="form.dear" placeholder="Dear" class="block w-full border p-2 rounded" />
        <textarea v-model="form.message" placeholder="Message" class="block w-full border p-2 rounded" />
        <input v-model="form.from" placeholder="From" class="block w-full border p-2 rounded" />
    </div>
</template>

<style scoped>
</style>
