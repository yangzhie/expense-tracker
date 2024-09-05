<template>
    <h3>Add transaction</h3>
    <form id="form">
        <div class="form-control">
            <label for="text">Transaction</label>
            <input type="text" id="text" placeholder="Enter transaction">
        </div>
        <div class="form-control">
            <label for="amount">
                Amount <br />
                (negative: expense, positive: income)
            </label>
            <input type="number" id="amount" placeholder="Enter amount">
        </div>
        <button class="btn">Add transation</button>
    </form>
</template>