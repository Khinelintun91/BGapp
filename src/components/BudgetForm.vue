<template>
  <div class="budget-form-container">
    <h2>Add Expense</h2>
    <form @submit.prevent="addExpense">
      <input type="text" v-model="expenseName" placeholder="Expense Name" required />
      <input type="number" v-model.number="expenseAmount" placeholder="Amount" required />
      <button type="submit">Add Expense</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'BudgetForm',
  data() {
    return {
      expenseName: "",
      expenseAmount: null
    }
  },
  methods: {
    addExpense() {
      if (this.expenseName && this.expenseAmount > 0) {
        const newExpense = {
          id: Date.now(),
          name: this.expenseName,
          amount: this.expenseAmount,
          date: new Date().toLocaleString()
        }
        this.$emit("expense-added", newExpense)
        this.expenseName = ""
        this.expenseAmount = null
      }
    }
  }
}
</script>

<style scoped>
.budget-form-container h2 {
  
  text-align: center;
  margin-bottom: 10px;
  font-size: 1.3em;
}

form {
  display: flex;
  flex-direction: column;
}

input {
  margin-bottom: 10px;
  margin-top: 5px;
  padding: 10px;
  border: none;
  border-radius: 5px;
  font-size: 1em;
  width: 90%;
  background-color: aliceblue;
  color: black;
}

button {
  transition: background 0.3s ease, transform 0.3s ease;
  padding: 10px;
  border: none;
  border-radius: 5px;
  background: rgba(30, 60, 114, 0.7);
}
.budget-form-container{
  
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  border: 1px solid rgba(255, 255, 255, 0.18);
  margin-bottom: 20px;
}

button:hover {
  background: rgba(30, 60, 114, 1);
  transform: translateY(-2px);
}
</style>