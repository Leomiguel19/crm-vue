<script setup>
    import RouterLink from "../components/UI/RouterLink.vue";
    import Heading from "../components/UI/Heading.vue"

    defineProps({
        titulo:{
            type: String,
        }
    })
</script>

<template>
    <div>
        <div class="flex justify-end">
            <RouterLink to="inicio">
                regresar
            </RouterLink>
        </div>
        <Heading>{{titulo}}</Heading>
    </div>
</template>