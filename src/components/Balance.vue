<template>
    <h4 class="uppercase text-xs">Your Balance</h4>
    <h1 class="text-lg font-bold text-gray-800">${{total}}</h1>
</template>

<script setup>
    const props = defineProps({
        total : {
            type: Number,
            required: true,
        }
    })
</script>