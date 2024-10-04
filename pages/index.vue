<script setup lang="ts">

import { object, string, type InferType } from 'yup'
  import type { FormSubmitEvent } from '#ui/types'

  const schema = object({
    email: string().email('Email invalide').required('Champ obligatoire'),
    password: string()
      .min(8, 'Doit comporter au moins 8 caractères')
      .required('Champ obligatoire')
  })

  type Schema = InferType<typeof schema>

  const state = reactive({
    email: undefined,
    password: undefined
  })
  
    async function onSubmit (event: FormSubmitEvent<Schema>) {
        // Do something with event.data
        console.log(event.data)
        await navigateTo({
            path: '/',
            query: {
                email: state.email,
                password: state.password
            }
        })
    }

    function onClick () {
        console.log(schema)
    }
</script>

<template>

    <UForm :schema="schema" :state="state" class="flex justify-center items-center w-full h-full" @submit="onSubmit">
        <div class="flex justify-center items-center w-full h-full">
            <div id="login__form" class="auth__form flex flex-col max-sm:px-4">
                <h1 class="mb-8">Connexion</h1>
                
                <div class="flex flex-col gap-y-4">
                    <!-- <UFormGroup label="Email" name="email">
                        <UInput v-model="state.email" placeholder="Adresse mail" />
                    </UFormGroup> -->
                    <UFormGroup name="email">
                        <!-- <input v-model="state.email" placeholder="Adresse mail"/> -->
                        <UInput v-model="state.email" placeholder="Adresse mail" size="md" />
                    </UFormGroup>

                    
                    <UFormGroup name="password">
                        <UInput v-model="state.password" placeholder="Mot de passe" size="md"/>
                        <!-- <input v-model="state.password" placeholder="Mot de passe" type="password" /> -->
                    </UFormGroup>

                    <!-- <input type="text" name="" id="" placeholder="Nom d'utilisateur">
                    <input type="text" name="" id="" placeholder="Mot de passe"> -->
                </div>

                <button class="btn btn-primary w-full mt-4" @click="onClick">Se connecter</button>

                <nuxt-link to="/auth/inscription/client" class="mt-2 inline-block ml-auto link">
                    Pas de compte ? Inscrivez-vous
                </nuxt-link>
            </div>
        </div>
    </UForm>
</template>

<style scoped>

    .auth__form {
        width: 440px;
        max-width: 100%;
    }

    input {
        width: 100%;
        margin-top: 1.5rem;
    }

    button {
        border-radius: 1.5rem;
    }

</style>