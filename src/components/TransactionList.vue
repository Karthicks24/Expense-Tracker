<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    transactions:{
        type:Array,
        required: true,
    }
});
const emit = defineEmits(["transactionDeleted"]);

const transaction_Delete = (id)=>{
    emit('transactionDeleted',id)
}
</script>

<template>
    <h3 style="margin-bottom: 3px">History</h3> <hr>
            <ul class="list" v-for="(transaction, index) in transactions" :key="transaction.id">
                <li class="history">
                    {{transaction.text}}<span :class="transaction.amount>0?'positive':'negative'">Rs.{{ transaction.amount }}</span>
                    <button class="del-button" @click="transaction_Delete(transaction.id)">X</button>
                </li>
            </ul>
</template>