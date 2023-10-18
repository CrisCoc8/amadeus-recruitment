<script setup>
import MobileGuestLayout from '@/Layouts/Mobile/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import ButtonGeneric from '@/Components/ButtonGeneric.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

const props = defineProps({
    enrollmentStatus: {
        type: Boolean,
        default: false,
    },
});

const form = useForm({
    email: '',
    password: '',
    remember: false,
});

/* Cristian Chavez
* El proyecto me dio errores al inicializarlo, realice estos pasos adicionales y anteriores al punto 4b
*    1: composer update
*    2: composer install
*    3: php artisan key:generate
*
* Aqui agregaria más feedback al usuario, un loader mientras se comprueban las credenciales, con: onProgress: progress => {}
*
* Agregaria validaciones extras a los inputs, antes de hacer la petición, es posible ingresar datos 'erroneos' al input, por ejemplo, un email no valido, no lo acepta pero el usuario no obtiene feedback, ser mas especifico.
*
* Agregar el icono de mostrar contraseña dentro del mismo input.
*
* Usaria snackbars para mejor feedback a los usuarios
*
* Dependiendo mi porcentaje de usuarios, usaria un breakpoint para dispositivos muy pequeños (iphone SE, 5, etc. max-height: 650px )
*
* No cambie (*) por (•) por temas de seguridad al manipular este input de password
*/

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script>

<template>
    <MobileGuestLayout>
        <Head title="Iniciar Sesión" />

        <form @submit.prevent="submit" class="flex flex-col h-full">

            <div class="welcome-container">
				<h3 class="welcome-title py-0 mb-1">¡Hola!</h3>
                <h5 class="welcome-subtitle pt-0 mt-0">Te damos la bienvenida.</h5>
			</div>

            <div class="flex flex-col items-center input-container">

                <TextInput
                    id="email"
                    type="email"
                    class="mt-1 block w-full form-control"
                    v-model="form.email"
                    required
                    placeholder="Ingrese correo"
                    autofocus
                    autocomplete="username"
                />

                <InputError class="mt-2 form-text" :message="form.errors.email" />
            </div>

            <div class="flex flex-col items-center mt-3">

                <TextInput
                    id="password"
                    type="password"
                    class="mt-1 block w-full form-control"
                    v-model="form.password"
                    placeholder="Ingrese contraseña"
                    required
                    autocomplete="current-password"
                />

                <InputError class="mt-2 form-text" :message="form.errors.password" />
            </div>

            <div class="mt-4">
                <Link
                    :href="route('password.request')"
                    class="restart-account"
                >
                    ¿Olvidaste contraseña?
                </Link>
            </div>

            <div class="button-container items-center">
                <ButtonGeneric class="btn submit-button w-full " :class="{ 'opacity-25,': form.processing }" :disabled="form.processing">
                    Acceder
                </ButtonGeneric>
            </div>
        </form>
    </MobileGuestLayout>
</template>

<style scoped>

/**
    Crearia variables globales para ciertos estilos/colores/tamaños

    color: $primary-color; (#3C7FF8)

    font-sizes:
        $text-xss --> 0.5rem
        $text-xs --> 0.75rem
        $text-sm --> 1rem
        $text-md --> 1.25rem
        $text-lg --> 1.5rem
        $text-xl --> 2.5rem
        $text-xll --> 4rem


*/

/* Estilos para móviles */
@media only screen and (max-width: 599px) {
    /* Estilos específicos para móviles aquí */

    .welcome-container {
        margin-top: 16.5vh;
    }
    .welcome-title {
        color: #3C7FF8;
        font-weight: 700;
        font-size: 1.6rem;
        margin-bottom: 1vh;

    }
    .welcome-subtitle {
        color: #3C7FF8;
        font-family: Poppins;
        font-size: 1.125rem;
        font-style: normal;
        font-weight: 400;
        line-height: 1.85rem;

    }
    .input-container{
        margin-top: 6.5vh;
    }
    .restart-account{
        color: #3C7FF8;
        text-align: center;
        font-family: Poppins;
        font-size: 14px;
        font-style: normal;
        font-weight: 600;
        line-height: 1.56rem;
        letter-spacing: 0.28px;
        text-underline-position: below;
        text-underline-offset: 5px;
        text-decoration: underline;
    }

    .button-container > .btn {
        height: 2.6rem;
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

    .button-container{
        margin-top: 20vh;
    }
    .submit-button {
        font-size: 1rem;
        width: 50%;
        font-weight: 500;
    }
}

/* Estilos para tablets y escritorios */
@media only screen and (min-width: 600px) {
    /* Estilos específicos para tablets y escritorios aquí */
    .welcome-container {
        margin-top: 19.5vh;
    }
    .welcome-title {
        color: #3C7FF8;
        font-weight: 700;
        font-size: 1.85rem;
        margin-bottom: 1vh;

    }
    .welcome-subtitle {
        color: #3C7FF8;
        font-family: Poppins;
        font-size: 1.35rem;
        font-style: normal;
        font-weight: 400;
        line-height: 1.85rem;

    }
    .input-container{
        margin-top: 6.5vh;
    }
    .restart-account{
        color: #3C7FF8;
        text-align: center;
        font-family: Poppins;
        font-size: 16px;
        font-style: normal;
        font-weight: 600;
        line-height: 1.6rem;
        letter-spacing: 0.28px;
        text-underline-position: below;
        text-underline-offset: 5px;
        text-decoration: underline;
    }

    .button-container > .btn {
        height: 2.8rem;
    }

    .form-control {
        width: 100%;
        height: 2.5rem;
        border-radius: 2rem;
        border: 1px solid #2b5db6;
        background: #fff;
        font-size: 1.25rem;
        text-align: center;
        color: #2B5DB6;
    }
    .form-control::placeholder {
    color: #9E9E9E;
    }
    .button-container{
        margin-top: 22vh;
    }
    .submit-button {
        font-size: 1.2rem;
        width: 50%;
        font-weight: 500;
    }
}


</style>
