<script setup>
    // import {reactive} from 'vue'
    import { onMounted, ref } from "vue";
    import ClienteService from "../services/ClienteService";
    import { FormKit } from '@formkit/vue'
    import {useRouter, useRoute} from 'vue-router'
    import RouterLink from "../components/UI/RouterLink.vue"
    import Heading from "../components/UI/Heading.vue"

    const route = useRoute()
    const router = useRouter()

    const { id } = route.params

    const formData = ref({})

    onMounted(() => {
        ClienteService.obtenerCliente(id)
            .then(({data}) => formData.value = data)
            .catch((error) => console.log('Sucedio un error: ', error))
    })

    defineProps({
        titulo:{
            type: String,
        }
    })

    const handleSubmit = (data) => {

    }
</script>

<template>
    <div>
        <div class="flex justify-end">
            <RouterLink to="listado-clientes">
                regresar
            </RouterLink>
        </div>
        <Heading>{{titulo}}</Heading>

        <div class="mx-auto mt-10 bg-white shadow">
            <div class="mx-auto md:w-4/5 py-20 px-6">
                <FormKit
                    type="form"
                    submit-label="Agregar Cliente"
                    :incomplete-message=false
                    @submit="handleSubmit"
                    :value="formData"
                > 
                    <FormKit
                        type="text"
                        label="Nombre"
                        name="nombre"
                        placeholder="Nombre del cliente"
                        validation="required"
                        :validation-messages="{required: 'El Nombre del Cliente es Obligatorio'}"
                        v-model="formData.nombre"
                    />

                    <FormKit
                        type="text"
                        label="Apellido"
                        name="apellido"
                        placeholder="Apellido del cliente"
                        validation="required"
                        :validation-messages="{required: 'El Apellido del Cliente es Obligatorio'}"
                        v-model="formData.apellido"
                    />

                    <FormKit
                        type="email"
                        label="Email"
                        name="email"
                        placeholder="Email del cliente"
                        validation="required|email"
                        :validation-messages="{required: 'El Email del Cliente es Obligatorio', email: 'Coloca un email valido'}"
                        v-model="formData.email"
                    />    

                    <FormKit
                        type="text"
                        label="Teléfono"
                        name="telefono"
                        placeholder="Teléfono: XXX-XXX-XXX"
                        validation="?matches:/^[0-9]{3}-[0-9]{3}-[0-9]{4}$/"
                        :validation-messages="{matches: 'El Formato no es valido'}"
                        v-model="formData.telefono"
                    />  
                    
                    <FormKit
                        type="text"
                        label="Empresa"
                        name="empresa"
                        placeholder="Empresa del cliente"
                        v-model="formData.empresa"
                    />

                    <FormKit
                        type="text"
                        label="Puesto"
                        name="puesto"
                        placeholder="Puesto del cliente"
                        v-model="formData.puesto"
                    />
                </FormKit>
            </div>
        </div>
    </div>
</template>

<style>
    .formkit-wrapper{
        max-width: 100%;
    }
</style>