<template>
  <div class="col-md-4 col-md-offset-4">
    <initial-input @numFieldsChanged="inputChanged($event)"></initial-input>
    <p>{{result}}</p>
    <button :disabled="disBtn" @click="showInputsFields">Generate</button>
    <button @click="makeCalculations">Calculate</button>
    <gen-fields 
    v-if="show" 
    v-for="num in numFields"
    :numFields="numFields" 
    :id="num-1"
    @inputChanged="inputsToNumbers($event)"
    @operationChanged="operationSelected($event)"></gen-fields>
</div>
</template>

<script>
import Input from './components/Input.vue'
import GeneratedFields from './components/GeneratedFields.vue'

export default {
  data () {
    return {
      numFields: 0,
      result: '',
      show: false,
      disBtn: true,
      operations: [],
      numbers: []
    }
  },
  components: {
    initialInput: Input,
    genFields: GeneratedFields
  },
  methods: {
    showInputsFields () {
      this.show = true
    },
    inputChanged (value) {
      this.numFields = parseInt(value);
      this.result = '';
      this.show = false
      this.disBtn = (this.numFields === undefined || this.numFields < 2) ? true : false
    },
    operationSelected (oper) {
      this.operations[oper[0]] = oper[1]
    },
    inputsToNumbers (input) {
        if (input[1] == 0) {this.result = 'You left at least one input empty'}
        this.numbers[input[0]] = input[1]
      
    },
    makeCalculations () {
      const self = this
      const operationsFunctions = {
      '+': (a,b) => Number(a) + Number(b),
      '-': (a,b) => Number(a) - Number(b),
      '*': (a,b) => Number(a) * Number(b),
      '/': (a,b) => Number(a) / Number(b)
      }
      if ((this.operations && this.numbers !== null) && this.operations.length + 1 && this.numbers.length === this.numFields) {
        this.result = this.numbers.reduce ( function (a,b,c) {
        return operationsFunctions[self.operations[c-1]] (a,b)
      }).toFixed(2)
      } else {
     this.result = 'Please inpul all numbers and select all operations' }
    }
    }
}
  
</script>

<style>
button:disabled {
  cursor: not-allowed;
}
</style>
