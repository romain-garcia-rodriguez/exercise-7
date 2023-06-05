<script setup>
import { computed } from "vue";

const props = defineProps({
  modelValue: String,
  placeholder: {
    value: String,
    required: true,
  },
  inputType: {
    type: String,
    required: false,
    default: "text",
  },
  error: {
    type: Object,
    required: true,
  },
});
defineEmits(["valueUpdated", "focusBlur"]);

const hasError = computed(() => {
  return !props.error.isValidated
    ? "focus:border-blue-600"
    : "focus:border-red-600 border-red-600";
});
</script>

<template>
  <input
    :class="[
      'form-control block w-full px-4 py-2 text-xl font-normal text-gray-700 bg-white bg-clip-padding border border-solid rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:outline-none',
      hasError,
    ]"
    :value="props.modelValue"
    :placeholder="props.placeholder"
    :type="props.inputType"
    @blur="$emit('focusBlur')"
    @input="$emit('valueUpdated', $event.target.value)"
  />
  <span v-if="props.error.isValidated" class="text-red-600 text-sm">{{
    props.error.message
  }}</span>
</template>

<style scoped></style>
