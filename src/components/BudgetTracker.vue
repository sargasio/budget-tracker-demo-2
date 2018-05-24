<template>

<div class="flex items-center justify-center h-screen">
  <div>
  <p class="font-serif text-grey-darkest text-3xl text-center font-bold  py-8"> Budget tracker</p>
    <div class="flex justify-center py-2">
      <form @submit.prevent="addSpending">
        <input 
          v-model.number="budgetInput" 
          class="bg-transparent border-b border-teal text-grey text-center ml-8 mr-3" 
          placeholder="0.00"
          type="text" 
          aria-label="value"
        />

        <button
          class="flex-no-shrink bg-teal hover:bg-teal-dark border-teal hover:border-teal-dark text-sm border-4 text-white py-1 px-2 rounded"
          type="submit"
        >Save</button>
      </form>

    </div>
    <ul>
      <li v-for="spending in spendings">{{ spending | pricesInEuros }}</li>
    </ul>
    </div>
</div>

</template>

<script>
export default {
  data() {
    return {
      budgetInput: null,
      spendings: []
    };
  },
  methods: {
    addSpending() {
      if (this.checkIfNumber()) {
        this.spendings.unshift(this.budgetInput);
        this.budgetInput = null;
      } else {
        alert("you did not enter a number");
      }
    },
    checkIfNumber() {
      if (typeof this.budgetInput !== "number") {
        return false;
      }
      return true;
    }
  },
  filters: {
    pricesInEuros(value) {
      return "€ " + Number(value).toFixed(2);
    }
  }
};
</script>
