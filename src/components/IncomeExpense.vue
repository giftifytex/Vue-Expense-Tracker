<template>
    <div class="flex gap-6 bg-white drop-shadow-md px-6 py-4 mt-4">
        <div>
            <h4 class="uppercase text-xs py-1">Income</h4>
            <p class="text-green-500">+${{ income }}</p>
        </div>
        <span class="border border-gray-400"></span>
        <div>
            <h4 class="uppercase text-xs py-1">Expense</h4>
            <p class="text-red-500">${{ expenses }}</p>
        </div>
    </div>
</template>

<script setup>
    const props = defineProps({
        income : {
            type:Number,
            required: true,
        },
        expenses: {
            type:Number,
            required: true,
        }
    })
</script>