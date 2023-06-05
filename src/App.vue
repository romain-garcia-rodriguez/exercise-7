<script setup lang="ts">
import { ref } from "vue";
import { required, email } from "@vuelidate/validators";
import LoginForm from "./components/LoginForm.vue";
// import useVuelidate from "@vuelidate/core";

const state = ref({
  email: "",
  password: "",
  confirmPassword: "",
});

const rules = {
  email: {
    required,
    email: email,
  },
  password: {
    required,
    minLengthPassword: () => {
      return state.value.password.length >= 8;
    },
    atLeastOneUpper: () => {
      const regex = /[A-Z]+/g;
      return regex.test(state.value.password);
    },
    atLeastOneLower: () => {
      const regex = /[a-z]+/g;
      return regex.test(state.value.password);
    },
    atLeastOneSpecial: () => {
      const regex = /[@&!*$()<>]+/g;
      return regex.test(state.value.password);
    },
    atLeastOneNumber: () => {
      const regex = /[0-9]+/g;
      return regex.test(state.value.password);
    },
  },
  confirmPassword: {
    required,
    sameAsPassword: () => {
      return state.value.password === state.value.confirmPassword;
    },
  },
};
// const v$ = useVuelidate(rules, state);

// const onFocusBlur = (validator) => {
//   if (validator.$invalid) {
//     validator.$touch();
//   } else {
//     validator.$reset();
//   }
// };
</script>

<template>
  <!-- 
    Pour cet exercice, il faut:
      - Décoposer le template en composants réutilisable
      - Rendre le formulaire interctif, c'est à dire:
      - Si une des conditions suivantes n'est pas respectées, mettre le bouton login en disable
      - Valider le champ email pour être sur que l'utilateur a bien écrit un email. Lorsque l'utilsateur qui le champ input email, le mettre en rouge si ce n'est pas bon
      - Lorsque l'utilisateur écrit son mot de passe, valider les requirements (les passer en vert). Si il supprime un des requierment, le mettre en rouge
      - Quand l'utilisateur tape son mot de passe pour confirmer le premier qu'il a ecrit, après un certain délai, valider si il est semblable ou non (mettre l'input en rouge s'il ne l'est pas)
      - Une fois que l'utilateur à rentré un email et un mot de passe valide et confirmé son mot de passe, rendre le bouton cliquable
    Pour cet exercice, il faut utiliser la librairie Vuelidate (pour Vue 3)
    - En bonus, rajouter un petit oeil dans les inputs passwords pour pouvoir voir les mots de passe, et qui après un certain délais se désactive
  -->
  <section class="h-screen">
    <div class="container px-6 py-12 h-full">
      <div
        class="flex justify-center items-center flex-wrap h-full g-6 text-gray-800"
      >
        <div class="md:w-8/12 lg:w-6/12 mb-12 md:mb-0">
          <img
            src="https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-login-form/draw2.svg"
            class="w-full"
            alt="Phone image"
          />
        </div>
        <div class="md:w-8/12 lg:w-5/12 lg:ml-20">
          <LoginForm
            :state="state"
            :rules="rules"
            @updateEmailValue="state.email = $event"
            @updatePasswordValue="state.password = $event"
            @updateConfirmPasswordValue="state.confirmPassword = $event"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped></style>
