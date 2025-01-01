<script setup>
import { useToast } from 'vue-toastification';
import { ref } from 'vue';

const text = ref('');
const amount = ref('');
const toast = useToast();
const emit = defineEmits(['transactionSubmitted']);

const add_list = ()=>{
    if(!text.value || !amount.value){
        toast.error("Both fiels must be filled")
        return
    }
    const transactionData = {
        text : text.value,
        amount : parseFloat(amount.value)
    }

    emit("transactionSubmitted",transactionData);
    
    text.value = '';
    amount.value= '';
}
</script>

<template>
    <h3 style="margin-top: 20px; margin-bottom: 3px;">New Transactions</h3> <hr>
            <form @submit.prevent="add_list" class="form">
                <div class="input">
                    <label for="text">
                        Text
                    </label>
                    <input type="text" id="text" v-model="text" placeholder="Enter text..">
                </div>
                <div class="input">
                    <label for="amount">
                        Amount<br>
                        (Include, - for your expense)
                    </label>
                    <input type="text" id="amount" v-model="amount" placeholder="Enter amount..">
                </div>
                <button class="add-btn">Add Transaction</button>
            </form>
</template>