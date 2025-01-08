<script lang="ts">
    let currentValue: string = '';
    let operator: string = '';
    let previousValue: string = '';
    let result: string = '';
  
    function handleNumber(number: string) {
      currentValue += number;
    }
  
    function handleOperator(op: string) {
      if (currentValue === '') return;
      operator = op;
      previousValue = currentValue;
      currentValue = '';
    }
  
    function calculate() {
      if (!previousValue || !currentValue || !operator) return;
      const prev = parseFloat(previousValue);
      const curr = parseFloat(currentValue);
  
      switch (operator) {
        case '+':
          result = (prev + curr).toString();
          break;
        case '-':
          result = (prev - curr).toString();
          break;
        case '*':
          result = (prev * curr).toString();
          break;
        case '/':
          result = (prev / curr).toString();
          break;
      }
  
      currentValue = result;
      operator = '';
      previousValue = '';
    }
  
    function clear() {
      currentValue = '';
      operator = '';
      previousValue = '';
      result = '';
    }
  </script>
  
  <div class="flex items-center justify-center min-h-screen bg-gray-100">
    <div class="w-80 bg-white rounded-lg shadow-md p-4">
      <div class="mb-4 p-2 text-right bg-gray-200 rounded-md text-2xl font-mono h-16 flex items-center justify-end overflow-x-auto">
        {currentValue || result || '0'}
      </div>
      <div class="grid grid-cols-4 gap-2">
        {#each ['7', '8', '9'] as num}
          <button on:click={() => handleNumber(num)} class="btn">{num}</button>
        {/each}
        <button on:click={() => handleOperator('/')} class="btn operator">/</button>
  
        {#each ['4', '5', '6'] as num}
          <button on:click={() => handleNumber(num)} class="btn">{num}</button>
        {/each}
        <button on:click={() => handleOperator('*')} class="btn operator">*</button>
  
        {#each ['1', '2', '3'] as num}
          <button on:click={() => handleNumber(num)} class="btn">{num}</button>
        {/each}
        <button on:click={() => handleOperator('-')} class="btn operator">-</button>
  
        <button on:click={() => handleNumber('0')} class="btn">0</button>
        <button on:click={clear} class="btn clear">C</button>
        <button on:click={calculate} class="btn equals col-span-2">=</button>
        <button on:click={() => handleOperator('+')} class="btn operator">+</button>
      </div>
    </div>
  </div>
  
  <style>
    .btn {
      @apply p-4 text-xl font-medium rounded-md bg-gray-100 hover:bg-gray-200 active:bg-gray-300;
    }
  
    .operator {
      @apply bg-blue-500 text-white hover:bg-blue-600;
    }
  
    .clear {
      @apply bg-red-500 text-white hover:bg-red-600;
    }
  
    .equals {
      @apply bg-green-500 text-white hover:bg-green-600;
    }
  </style>
  