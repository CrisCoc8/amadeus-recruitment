<script setup>
import MobileGuestLayout from '@/Layouts/Mobile/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import ButtonGeneric from '@/Components/ButtonGeneric.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

const form = useForm({
    email: '',
});


/** Cristian Chavez
 * En esta vista elimine el texto descriptivo original que tenia pero considero que es muy valido para mejor entendimiento al usuario.
 *
 * Un botón/texto para seria util
 *
 * El titulo es un area de oportunidad ("¿Quieres recuperar tu contraseña?"),
 *
 * Igual que el Login, agregar más feedback especifico al usuario y validaciones antes de hacer la petición y loading al boton.
 *
 * Dependiendo mi porcentaje de usuarios, usaria un breakpoint para dispositivos muy pequeños (iphone SE, 5, etc. max-height: 650px )
 */

const submit = () => {
    form.post(route('password.email'));
};
</script>

<template>
    <MobileGuestLayout>
        <Head title="Restablecer Contraseña" />

        <form @submit.prevent="submit" class="flex flex-col h-full">

            <div class="password-container flex justify-center">
                <h3 class="password-title">¿Quieres recuperar tu contraseña?</h3>
            </div>

            <div class="flex flex-col items-center input-container">

                <TextInput
                    id="email"
                    type="email"
                    class="mt-0 block w-full form-control"
                    v-model="form.email"
                    required
                    autofocus
                    placeholder="Ingrese usuario o correo"
                    autocomplete="username"
                />

                <InputError class="mt-2 form-text" :message="form.errors.email" />
            </div>

            <div class="button-container items-center">
                <ButtonGeneric class="btn submit-button w-full" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Restablecer
                </ButtonGeneric>
            </div>
        </form>

    </MobileGuestLayout>
</template>

<style scoped>

/* Estilos para móviles */
@media only screen and (max-width: 599px) {
    /* Estilos específicos para móviles aquí */

    .password-container{
        margin-top: 32.5vh;
    }
    .password-title {
        color: #3C7FF8;
        text-align: center;
        font-family: Poppins;
        font-size: 1.5rem;
        font-style: normal;
        font-weight: 600;
        line-height: 1.85rem;
        width: 76%;
    }
    .input-container{
        margin-top: 9vh;
    }
    .form-label {
        font-weight: 600;
        font-size: 1.2rem;
        color: #222038;
        text-align: start;
        width: 75%;
        margin-left: 1rem;
    }

    .form-control {
        width: 100%;
        height: 2.5rem;
        border-radius: 2rem;
        border: 1px solid #2b5db6;
        background: #fff;
        font-size: 1rem;
        text-align: center;
        color: #2B5DB6;

    }

    .form-control::placeholder {
    color: #9E9E9E;
    }

    .button-container > .btn {
        height: 2.6rem;
    }
    .button-container{
        margin-top: 14.75vh;
    }
    .submit-button {
        font-size: 1rem;
        width: 48%;
        font-weight: 500;
    }
}

/* Estilos para tablets y escritorios */
@media only screen and (min-width: 600px) {
    /* Estilos específicos para tablets y escritorios aquí */

    .password-container{
        margin-top: 30.5vh;
    }
    .password-title {
        color: #3C7FF8;
        text-align: center;
        font-family: Poppins;
        font-size: 1.85rem;
        font-style: normal;
        font-weight: 600;
        line-height: 2rem;
        width: 60%;
    }
    .input-container{
        margin-top: 15vh;
    }
    .form-control {
        width: 75%;
        height: 2.5rem;
        border-radius: 2rem;
        border: 1px solid #2b5db6;
        background: #fff;
        font-size: 1rem;
        text-align: center;
        color: #2B5DB6;

    }

    .form-control::placeholder {
    color: #9E9E9E;
    }

    .button-container > .btn {
        height: 2.8rem;
    }
    .button-container{
        margin-top: 14vh;
    }
    .submit-button {
        font-size: 1.2rem;
        width: 35%;
        font-weight: 500;
    }

}


</style>
