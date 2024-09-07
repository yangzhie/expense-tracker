<template>
    <h3>Add transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Transaction</label>
            <input type="text" id="text" v-model="text" placeholder="Enter transaction">
        </div>
        <div class="form-control">
            <label for="amount">
                Amount <br />
                (negative: expense, positive: income)
            </label>
            <input type="text" id="amount" v-model="amount" placeholder="Enter amount">
        </div>
        <button class="btn">Add transation</button>
    </form>
</template>

<script setup>
    import { ref } from 'vue'
    import { useToast } from 'vue-toastification'

    const text = ref('')
    const amount = ref('')
    const toast = useToast()

    // validation using vue-toastification
    const onSubmit = () => {
        if(!text.value || !amount.value) {
            toast.error("Both fields must be filled")
            return
        }

        console.log(text.value, amount.value) 

        // clearing fields
        text.value = ""
        amount.value = ""
    }
</script>