<script setup>
import { computed } from "vue";

const props = defineProps({
  type: {
    type: String,
    required: false,
    default: "submit",
  },
  content: {
    type: String,
    required: true,
  },
  disabled: {
    type: Boolean,
    required: false,
    default: true,
  },
});

const isDisabled = computed(() => {
  return props.disabled
    ? "bg-gray-200"
    : "bg-blue-600 hover:bg-blue-700 shadow-md hover:shadow-lg active:bg-blue-800 active:shadow-lg";
});
</script>

<template>
  <button
    :type="props.type"
    :class="[
      'inline-block px-7 py-3 text-white font-medium text-sm leading-snug uppercase rounded focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0 transition duration-150 ease-in-out w-full',
      isDisabled,
    ]"
    data-mdb-ripple="true"
    data-mdb-ripple-color="light"
    :disabled="props.disabled"
  >
    {{ props.content }}
  </button>
</template>

<style scoped></style>
