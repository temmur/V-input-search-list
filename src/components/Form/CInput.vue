<template lang="">
    <div>
        <slot name="prefix"></slot>
    <input
    @change="change"
      class="py-3 px-4 placeholder:text-white/20 bg-sky-600 outline-none text-white"
      v-bind="{ type, placeholder, minLength, maxLength, id,  }"
      :value="modelValue"
      @input="(event) => emit('update:modelValue', event.target?.value)"
      @blur="emit('on-blur')"
      @focus="emit('on-focus')"
      @focusout="emit('focus-out')"
    />
    <slot name="suffix"></slot>
    </div>
</template>
<script setup lang="ts">
import { defineProps, defineEmits } from 'vue'
interface Props {
  type: string
  placeholder: string
  modelValue: string | number
  maxLength?: number
  minLength?: number
  id?: string
  inputClass?: string
  error?: boolean,
  change:Function
  

}
defineProps<Props>(
    
)

const emit = defineEmits<{
  (e: 'update:modelValue', val: Event): void
  (e: 'on-focus'): void
  (e: 'on-blur'): void
  (e: 'focus-out'): void
}>()
</script>
<style scoped>
    
</style>