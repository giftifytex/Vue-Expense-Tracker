<template>
    <div class="mt-4">

        <h3 class="font-bold mb-1">History</h3>
        <hr class="mb-3">
        <ul class="flex flex-col gap-1">
            <li v-for="transaction in transactions" :key="transaction.id" class="flex justify-between relative bg-white shadow-md p-2 text-xs border-r-4  group" :class="transaction.amount < 0 ? 'border-red-700' : 'border-green-500'">
                {{ transaction.text }} <span class="">${{ transaction.amount }}</span>
                <button class="absolute top-0 left-[-20px] px-2 py-1 bg-red-700 text-gray-100 opacity-0 group-hover:opacity-100 transition-all" @click="handleDelete( transaction.id )">x</button>
            </li>
            <!-- <li class="flex justify-between relative bg-white shadow-md p-2 text-xs border-r-4 border-red-700 group">
                Cash <span class="">-$400</span>
                <button class="absolute top-0 left-[-20px] px-2 py-1 bg-red-700 text-gray-100 opacity-0 group-hover:opacity-100 transition-all">x</button>
            </li>  -->
        </ul>
    </div>
</template>
<script setup>
import { defineProps } from 'vue';

const emit = defineEmits(['deleteTransaction']);
const props = defineProps({
    transactions: {
        type: Array,
        required: true
    }
});

const handleDelete = (id) => {
    let transactionId = id;
    emit('deleteTransaction', transactionId);
}
 
</script>