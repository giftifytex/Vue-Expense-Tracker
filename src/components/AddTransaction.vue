<template>
    <div class="mt-6">
        <h3 class="font-bold">Add new transaction</h3>
        <hr class="mb-3">
        <form @submit.prevent="onSubmit">
            <div class="flex flex-col gap-1">
                <label for="" class="text-xs font-bold">Text</label>
                <input type="text" placeholder="Enter text..." class="p-1 rounde-sm" v-model="text">
            </div>
            <div class="flex flex-col gap-1 my-2">
                <label for="" class="text-xs font-bold">Amount <br><span>(negative - expense, positive - income)</span></label>
                <input type="text" placeholder="Enter amount..." class="p-1 rounde-sm" v-model="amount">
            </div>

            <div class="flex flex-col gap-1 my-4">
                <button class="bg-purple-500 text-white text-xs p-1.5 rounded-sm">Add transaction</button>
            </div>
        </form>
    </div>
</template>

<script setup>
import {ref} from "vue";
import {useToast} from "vue-toastification";

const toast = useToast();
const text = ref('');
const amount = ref('');
const emit = defineEmits(['transactionSubmitted']);

const onSubmit = () => {
    if(!text.value || !amount.value){
        toast.error('Both fields must be filled');
        return;
    }
    const transactionData = {
        text: text.value,
        amount: parseFloat(amount.value)
    }
     emit('transactionSubmitted', transactionData);
    text.value = "";
    amount.value = "";
}
</script>