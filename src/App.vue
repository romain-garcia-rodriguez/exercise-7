<script setup lang="ts"></script>

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
          <form>
            <!-- Email input -->
            <div class="mb-6">
              <input
                type="text"
                class="form-control block w-full px-4 py-2 text-xl font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                placeholder="Email address"
              />
            </div>

            <!-- Password input -->
            <div class="mb-6">
              <input
                type="password"
                class="form-control block w-full px-4 py-2 text-xl font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                placeholder="Password"
              />
            </div>

            <!-- Confirm password input -->
            <div class="mb-6">
              <input
                type="password"
                class="form-control block w-full px-4 py-2 text-xl font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                placeholder="Confirm password"
              />
            </div>

            <div
              class="flex items-center my-4 before:flex-1 before:border-t before:border-gray-300 before:mt-0.5 after:flex-1 after:border-t after:border-gray-300 after:mt-0.5"
            ></div>

            <div class="mb-4">
              <p class="text-gray-500">You're password must contain :</p>
              <ul class="mx-8 text-gray-400 list-disc">
                <li>At least 8 characters</li>
                <li>At least one special character</li>
                <li>At least one uppercase</li>
                <li>At least one lowercase</li>
                <li>A least one number</li>
              </ul>
            </div>

            <!-- Submit button -->
            <button
              type="submit"
              class="inline-block px-7 py-3 bg-blue-600 text-white font-medium text-sm leading-snug uppercase rounded shadow-md hover:bg-blue-700 hover:shadow-lg focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-800 active:shadow-lg transition duration-150 ease-in-out w-full"
              data-mdb-ripple="true"
              data-mdb-ripple-color="light"
            >
              Sign in
            </button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped></style>
