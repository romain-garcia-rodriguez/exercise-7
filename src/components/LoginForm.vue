<script setup>
import useVuelidate from "@vuelidate/core";
import { watch } from "vue";
import ButtonForm from "./ButtonForm.vue";
import FormValidators from "./FormValidators.vue";
import InputForm from "./InputForm.vue";

const props = defineProps({
  state: {
    type: Object,
    required: true,
  },
  rules: {
    type: Object,
    required: true,
  },
});
defineEmits([
  "focusBlur",
  "updateEmailValue",
  "updatePasswordValue",
  "updateConfirmPasswordValue",
]);

const v$ = useVuelidate(props.rules, props.state);

const onFocusBlur = (validator) => {
  if (validator.$invalid) {
    validator.$touch();
  } else {
    validator.$reset();
  }
};

watch(
  (v$.value.$invalid,
  (invalid) => {
    if (!invalid) {
      console.log("ici");
      v$.value.$reset();
    }
  })
);
</script>

<template>
  <form>
    <!-- Email input -->
    <div class="mb-6">
      <InputForm
        :modelValue="props.state.email"
        @valueUpdated="$emit('updateEmailValue', $event)"
        placeholder="Email address"
        input-type="text"
        :error="{
          isValidated: v$.email.$dirty,
          message: v$.email.required.$invalid ? 'Email is required' : '',
        }"
        @focus-blur="onFocusBlur(v$.email)"
      />
    </div>

    <!-- Password input -->
    <div class="mb-6">
      <InputForm
        :modelValue="props.state.password"
        @valueUpdated="$emit('updatePasswordValue', $event)"
        placeholder="Password"
        input-type="password"
        :error="{
          isValidated: v$.password.$dirty,
          message: v$.password.required.$invalid ? 'Password is required' : '',
        }"
        @focus-blur="onFocusBlur(v$.password)"
      />
    </div>

    <!-- Confirm password input -->
    <div class="mb-6">
      <InputForm
        :modelValue="props.state.confirmPassword"
        @valueUpdated="$emit('updateConfirmPasswordValue', $event)"
        placeholder="Confirm assword"
        input-type="password"
        :error="{
          isValidated: v$.confirmPassword.$dirty,
          message: v$.confirmPassword.required.$invalid
            ? 'Confirm password is required'
            : '',
        }"
        @focus-blur="onFocusBlur(v$.confirmPassword)"
      />
    </div>

    <div
      class="flex items-center my-4 before:flex-1 before:border-t before:border-gray-300 before:mt-0.5 after:flex-1 after:border-t after:border-gray-300 after:mt-0.5"
    ></div>

    <div class="mb-4">
      <FormValidators
        title="You're password must contain"
        :validators="[
          {
            content: 'At least 8 characters',
            validated: !v$.password.minLengthPassword.$invalid,
          },
          {
            content: 'At least one special character',
            validated: !v$.password.atLeastOneSpecial.$invalid,
          },
          {
            content: 'At least one uppercase',
            validated: !v$.password.atLeastOneUpper.$invalid,
          },
          {
            content: 'At least one lowercase',
            validated: !v$.password.atLeastOneLower.$invalid,
          },
          {
            content: 'A least one number',
            validated: !v$.password.atLeastOneNumber.$invalid,
          },
        ]"
      />
    </div>
    <!-- Submit button -->
    <ButtonForm content="Sign in" :disabled="v$.$invalid" />
  </form>
</template>

<style scoped></style>
