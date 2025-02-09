<template>
  <div id="app">
    <h1>Budget Tracker</h1>
    <BudgetForm @expense-added="addExpense" />
    <BudgetList :expenses="expenses" @expense-removed="removeExpense" />
  </div>
</template>

<script>
import BudgetForm from './components/BudgetForm.vue'
import BudgetList from './components/BudgetList.vue'

export default {
  name: 'App',
  components: {
    BudgetForm,
    BudgetList
  },
  data() {
    return {
      expenses: JSON.parse(localStorage.getItem("expenses")) || []
    }
  },
  methods: {
    addExpense(expense) {
      this.expenses.push(expense)
      this.saveExpenses()
    },
    removeExpense(id) {
      this.expenses = this.expenses.filter(exp => exp.id !== id)
      this.saveExpenses()
    },
    saveExpenses() {
      localStorage.setItem("expenses", JSON.stringify(this.expenses))
    }
  }
}
</script>

<style>
/* Reset and typography */
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  font-family: Arial, sans-serif;
}

/* Blue–Red Gradient Background */
body {
  background:#002D62;
 
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
}

/* Main container styling */
#app {
  width: 100%;
  max-width: 500px;
  padding: 20px;
  margin: 10px;
}

/* Headings */
h1 {
  text-align: center;
  margin-bottom: 20px;
}

/* Glass effect for forms */
form {
  background: rgba(255, 255, 255, 0.15);
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  border: 1px solid rgba(255, 255, 255, 0.18);
  margin-bottom: 20px;
}

/* Input fields styling */
input {
  width: 100%;
  margin-bottom: 10px;
  padding: 10px;
  border: none;
  border-radius: 5px;
  background: rgba(255, 255, 255, 0.25);
  color: #fff;
  font-size: 1em;
  transition: box-shadow 0.3s ease;
}

input:focus {
  outline: none;
  box-shadow: 0 0 5px rgba(255,255,255,0.8);
}

/* Button styling with hover animation */
button {
  width: 100%;
  padding: 10px;
  border: none;
  border-radius: 5px;
  background: rgba(30, 60, 114, 0.7);
  color: #fff;
  cursor: pointer;
  transition: background 0.3s ease, transform 0.3s ease;
}

button:hover {
  background: rgba(30, 60, 114, 1);
  transform: translateY(-3px);
}

/* Responsive Design */
@media (max-width: 600px) {
  #app {
    width: 90%;
    padding: 10px;
  }
  
  input, button {
    font-size: 0.9em;
  }
  
  h1 {
    font-size: 1.5em;
  }
}
</style>