<template>
  <div class="validate-input-container pb-3">
    <input
      class="form-control"
           :class="{'is-invalid':inputRef.error}"
           :value="inputRef.val"
           @blur="validateInput"
           @input="updateValue"
      v-bind="$attrs"
    >
  </div>
  <span v-if="inputRef.error" class="invalid-feedback">123213</span>
</template>

<script lang="ts">
import { defineComponent, PropType, reactive } from 'vue'
interface RuleProp {
  type: 'required' |'email';
  message: string;
}
export type RulesProp = RuleProp[]
export default defineComponent({
  name: 'ValidateInput',
  props: {
    rules: Array as PropType<RulesProp>,
    modelValue: String
  },
  inheritAttrs: false,
  setup (props, context) {
    const inputRef = reactive({
      val: props.modelValue || '',
      error: false,
      message: ''
    })
    const updateValue = (e: KeyboardEvent) => {
      const targetValue = (e.target as HTMLInputElement).value
      inputRef.val = targetValue
      context.emit('update:modelValue', targetValue)
    }
    const validateInput = () => {
      if (props.rules) {
        const allPassed = props.rules.every(rule => {
          let passed = true
          inputRef.message = rule.message
          switch (rule.type) {
            case 'required':
              passed = (inputRef.val.trim() !== '')
              break
            default:
              break
          }
          return passed
        })
        inputRef.error = !allPassed
      }
    }
    return {
      inputRef,
      validateInput,
      updateValue
    }
  }
})
</script>

<style scoped>

</style>
