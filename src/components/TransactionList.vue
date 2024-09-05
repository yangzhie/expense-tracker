<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li 
            v-for="transaction in transactions" 
            v-bind:key="transaction.id"
            v-bind:class="transaction.amount < 0 ? 'minus' : 'plus'"
        >
            {{ transaction.text }} <span>${{transaction.amount}}</span>
            <button class="delete-btn">x</button>
        </li>
    </ul>
</template>

<script setup>
    // defineProps lets you access props from parent component
    import { defineProps } from 'vue'

    const props = defineProps({
        // single prop
        transactions: {
            type: Array,
            Required: true
        }
    })
</script>