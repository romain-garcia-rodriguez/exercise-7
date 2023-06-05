<script setup>
const props = defineProps({
  title: {
    type: String,
    required: true,
  },
  validators: {
    type: Array,
    required: true,
  },
});
</script>

<template>
  <p class="text-gray-500">{{ props.title }} :</p>
  <ul class="mx-8 text-gray-400 list-disc">
    <li
      v-for="(validator, index) of validators"
      :key="index"
      :class="validator.validated ? 'text-green-400' : ''"
    >
      {{ validator.content }}
    </li>
  </ul>
</template>

<style scoped></style>
