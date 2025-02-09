<template>
    <div class="expense-list-container">
      <h2>Expense List</h2>
      <ul>
        <li v-for="expense in expenses" :key="expense.id" class="expense-item">
          <div class="expense-info">
            <span class="expense-name">{{ expense.name }}</span>
            <span class="expense-date">{{ expense.date }}</span>
          </div>
          <div class="expense-actions">
            <span class="expense-amount">{{ expense.amount }} $</span>
            <button class="remove-button" @click="removeExpense(expense.id)">&#10005;</button>
          </div>
        </li>
      </ul>
      <h3 class="total-amount">Total: {{ totalAmount }} $</h3>
    </div>
  </template>
  
  <script>
  export default {
    name: 'BudgetList',
    props: ['expenses'],
    computed: {
      totalAmount() {
        return this.expenses.reduce((sum, expense) => sum + expense.amount, 0)
      }
    },
    methods: {
      removeExpense(id) {
        this.$emit("expense-removed", id)
      }
    }
  }
  </script>
  
  <style scoped>
  .expense-list-container {
    margin-top: 20px;
  }
  
  /* Reset list styles */
  ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  
  .expense-item {
    background: rgba(255, 255, 255, 0.1);
    margin: 10px 0;
    padding: 12px 15px;
    border-radius: 8px;
    transition: transform 0.3s ease, background 0.3s ease;
  }
  
  .expense-item:hover {
    transform: translateY(-3px);
    background: rgba(255, 255, 255, 0.15);
  }
  
  /* Layout for expense info and actions */
  .expense-info,
  .expense-actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .expense-info {
    margin-bottom: 5px;
  }
  
  .expense-name {
    font-weight: 600;
    font-size: 1em;
  }
  
  .expense-date {
    font-size: 0.8em;
    color: #dcdcdc;
  }
  
  .expense-amount {
    font-size: 1em;
    font-weight: 500;
  }
  
  /* Remove button styling */
  .remove-button {
    background: transparent;
    border: none;
    color: #fff;
    font-size: 18px;
    cursor: pointer;
    margin-left: 10px;
    transition: color 0.3s ease, transform 0.3s ease;
    width: 30px;
    height: 30px;
    line-height: 30px;
    text-align: center;
    flex-shrink: 0;
  }
  
  .remove-button:hover {
    color: #ff6b81;
    transform: scale(1.1);
  }
  
  .total-amount {
    margin-top: 20px;
    text-align: right;
    font-size: 1.2em;
    font-weight: bold;
  }
  
  /* Responsive adjustments for smaller screens */
  @media (max-width: 600px) {
    .expense-item {
      padding: 10px;
    }
  
    .expense-name {
      font-size: 0.95em;
    }
  
    .expense-date {
      font-size: 0.75em;
    }
  
    .expense-amount {
      font-size: 0.95em;
    }
  }
  </style>