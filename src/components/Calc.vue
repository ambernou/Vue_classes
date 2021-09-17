<template>
  <div class='calc'>
    <div class='display'>
        <input v-model.number='operand1' type='number' />
        <input v-model.number='operand2' type='number' />
        = {{ result }}
    </div>
    <div class='keyboard'>
        <button @click='result = operand1 + operand2'>+</button>
        <button @click='subtraction(operand1, operand2)'>-</button>
        <button @click='multiply'>*</button>
        <button @click='div'>/</button>
        <button @click='exp'>a<sup>b</sup></button>
        <button @click='intDiv'>div</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data () {
    return {
      operand1: 0,
      operand2: 0,
      result: 0
    }
  },
  methods: {
    subtraction (operand1, operand2) {
      this.result = operand1 - operand2
    },
    multiply () {
      const { operand1, operand2 } = this
      this.result = operand1 * operand2
    },
    div () {
      const { operand1, operand2 } = this
      this.result = operand1 / operand2
    },
    exp () {
      const { operand1, operand2 } = this
      if (operand2 === 0) {
        this.result = 1
      } else if (operand2 === 1) {
        this.result = operand1
      } else if (operand2 >= 2) {
        this.result = operand1
        for (let i = 2; i <= operand2; i++) {
          this.result = this.result * operand1
        }
      } else if (operand2 === -1) {
        this.result = (1 / operand1).toFixed(4)
      } else if (operand2 < -1) {
        this.result = operand1
        for (let i = -2; i >= operand2; i--) {
          this.result = this.result * operand1
        }
        this.result = (1 / this.result).toFixed(4)
      }
    },
    intDiv () {
      const { operand1, operand2 } = this
      this.result = parseInt(operand1 / operand2)
    }
  }
}
</script>
