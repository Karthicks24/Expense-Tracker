<script setup>
    import { defineProps } from 'vue';
    const props = defineProps({
        income:{
            type:Number,
            required:true
        },
        expense:{
            type:Number,
            required:true
        }
    })
</script>

<template>
    <section class="amount-box">
            <div class="amount">
                <h4>Income</h4>
                <p class="green">+Rs.{{income}}</p>
            </div>
            <div class="amount">
                <h4>Expense</h4>
                <p class="red">Rs.{{expense}}</p>
            </div>
        </section>
</template>
