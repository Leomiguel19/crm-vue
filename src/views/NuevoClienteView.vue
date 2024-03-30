<script setup>
    // import {reactive} from 'vue'
    import axios from "axios"
    import { FormKit } from '@formkit/vue'
    import {useRouter, useRoute} from 'vue-router'
    import RouterLink from "../components/UI/RouterLink.vue"
    import Heading from "../components/UI/Heading.vue"

    const route = useRoute()
    const router = useRouter()

    defineProps({
        titulo:{
            type: String,
        }
    })

    // const formData = reactive({
    //     nombre: "Leonardo",
    //     apellido: "Guilarte",
    //     email: "leomiguel1907@gmail.com",
    //     telefono: "+58 412-095-0165",
    //     empresa: "MaiaHR",
    //     puesto: "Desarrollador Full Stack",
    // })

    const handleSubmit = (data) => {
        axios.post('http://localhost:4000/clientes', data)
            .then(response => {
                // Redireccionar
                router.push({name: 'inicio'})
            })
            .catch(error => console.log(error))
    }
</script>

<template>
    <div>
        <div class="flex justify-end">
            <RouterLink to="inicio">
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
                > 
                    <!-- :value="formData" -->
                    <FormKit
                        type="text"
                        label="Nombre"
                        name="nombre"
                        placeholder="Nombre del cliente"
                        validation="required"
                        :validation-messages="{required: 'El Nombre del Cliente es Obligatorio'}"
                    />

                    <FormKit
                        type="text"
                        label="Apellido"
                        name="apellido"
                        placeholder="Apellido del cliente"
                        validation="required"
                        :validation-messages="{required: 'El Apellido del Cliente es Obligatorio'}"
                    />

                    <FormKit
                        type="email"
                        label="Email"
                        name="email"
                        placeholder="Email del cliente"
                        validation="required|email"
                        :validation-messages="{required: 'El Email del Cliente es Obligatorio', email: 'Coloca un email valido'}"
                    />    

                    <FormKit
                        type="text"
                        label="Teléfono"
                        name="telefono"
                        placeholder="Teléfono: +XX XXX-XXX-XXX"
                        validation="?matches:/^[+][0-9]{2} [0-9]{3}-[0-9]{3}-[0-9]{4}$/"
                        :validation-messages="{matches: 'El Formato no es valido'}"
                    />  
                    
                    <FormKit
                        type="text"
                        label="Empresa"
                        name="empresa"
                        placeholder="Empresa del cliente"
                    />

                    <FormKit
                        type="text"
                        label="Puesto"
                        name="puesto"
                        placeholder="Puesto del cliente"
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