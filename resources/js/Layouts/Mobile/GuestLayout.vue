<script setup>
import ApplicationLogo from '@/Components/Amadeus/ApplicationLogo.vue';
import GridLayout from '@/Components/Custom/GridLayout.vue';
import { Link } from '@inertiajs/vue3';
</script>

<template>

    <GridLayout />

    <div class="min-h-screen flex flex-column justify-between items-center">
        <div class="flex flex-colum justify-center text-center px-6 py-4 shadow-md rounded-lg form-container-custom">
            <slot />
        </div>

        <div class="logo-container">
            <Link href="/">
                <ApplicationLogo class="logo"/>
            </Link>
        </div>
    </div>

</template>

<style>

.logo {
    max-width: 12rem;
    height: 2rem;
}

.logo-container {
    max-width: 12rem;
    height: 5rem;
}

/*Nuevos estilos y medidas para el layout de Guest*/
.form-container-custom {
    border-radius: 3.125rem;
    min-width: 100vw;
    height: 64vh;
    border: 0px solid #3C7FF8;
    border-radius: 0px 0px 40px 40px;
    background: linear-gradient(180deg, #B5CFFD -3.47%, rgba(181, 207, 253, 0.20) 34.78%, #B5CFFD 126.26%);
    box-shadow:0rem 0rem 0rem 0rem #00000015;
    overflow: visible;
}
</style>
