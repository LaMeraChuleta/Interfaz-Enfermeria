<template>
    <div>
        <!-- +-------------------------------------------------------------------+ 
        |                           PASOS PARA AGREGAR ENFERMERA            |
        +-------------------------------------------------------------------+ -->
        <v-container>
            <v-stepper v-model="e1">
                <v-stepper-header>
                    <v-stepper-step :complete="e1 > 1" step="1">Datos Personales</v-stepper-step>
                    <v-divider></v-divider>
                    <v-stepper-step :complete="e1 > 2" step="2">Name of step 2</v-stepper-step>
                    <v-divider></v-divider>
                    <v-stepper-step step="3">Name of step 3</v-stepper-step>
                </v-stepper-header>
                <v-stepper-items>
                <!-- +-------------------------------------------------------------------+
                            |                         PASO NUMERO 1                              |
                            +-------------------------------------------------------------------+ -->
                    <v-stepper-content step="1">
                        <v-card>
                            <v-card-title>Nueva Enfermera</v-card-title>
                            <v-divider></v-divider>
                            <v-card-text class="mt-2 mb-10">
                                <v-row>
                                    <v-col>
                                        <v-text-field v-model="nuevaEnfermera.matricula" label="Matricula"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="nuevaEnfermera.nombres" label="Nombre(s)"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="nuevaEnfermera.apellido_m" label="Apellido Materno"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="nuevaEnfermera.apellido_p" label="Apelldio Paterno"></v-text-field>
                                    </v-col>
                                </v-row>
                                <v-row>
                                    <v-col>
                                        <v-text-field v-model="nuevaEnfermera.lugar_nacimiento" label="Lugar de Nacimiento"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-menu
                                            :close-on-content-click="false"
                                            transition="scale-transition"
                                            offset-y
                                            max-width="290px"
                                            min-width="290px"
                                        >
                                        <template v-slot:activator="{ on, attrs }">
                                            <v-text-field
                                                v-model="nuevaEnfermera.fecha_nacimiento"
                                                label="Fecha de Nacimiento"
                                                persistent-hint
                                                prepend-icon="mdi-calendar"
                                                v-bind="attrs"
                                                v-on="on"
                                            ></v-text-field>
                                        </template>
                                        <v-date-picker v-model="nuevaEnfermera.fecha_nacimiento" no-title></v-date-picker>
                                        </v-menu>
                                    </v-col>
                                    <v-col>
                                        <v-checkbox v-model="nuevaEnfermera.sexo" class="ma-0" value="F" label="Femenino" color="primary"></v-checkbox>
                                    </v-col>
                                    <v-col>
                                        <v-checkbox v-model="nuevaEnfermera.sexo" class="ma-0" value="M" label="Masculino" color="primary"></v-checkbox>
                                    </v-col>
                                </v-row>
                                <v-row>
                                    <v-col>
                                        <v-text-field v-model="nuevaEnfermera.tipo_enfermera" label="Tipo de Enfermera"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="nuevaEnfermera.jornada" label="Jornada"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="nuevaEnfermera.horario_labores" label="Horario Laboral"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="nuevaEnfermera.descanso" label="Descando"></v-text-field>
                                    </v-col>
                                </v-row>
                            <v-divider></v-divider>
                            </v-card-text>
                            <v-card-actions class="d-flex justify-end">
                                <v-btn text>Cancel</v-btn>
                                <v-btn color="primary" @click="agregar_enfermera(nuevaEnfermera)">Continue</v-btn>
                            </v-card-actions>
                        </v-card>
                    </v-stepper-content>
                <!-- +-------------------------------------------------------------------+
                            |                           PASO NUMERO 2                            |
                            +-------------------------------------------------------------------+ -->
                    <v-stepper-content step="2">
                        <v-card class="mb-12" color="grey lighten-1" height="200px"></v-card>
                        <v-btn color="primary" @click="e1 = 3">Continue</v-btn>
                        <v-btn text>Cancel</v-btn>
                    </v-stepper-content>
                <!-- +-------------------------------------------------------------------+
                            |                           PASO NUMERO 3                            |
                            +-------------------------------------------------------------------+ -->
                    <v-stepper-content step="3">
                        <v-card class="mb-12" color="grey lighten-1" height="200px"></v-card>
                        <v-btn color="primary" @click="e1 = 1">Continue</v-btn>
                        <v-btn text>Cancel</v-btn>
                    </v-stepper-content>
                </v-stepper-items>
            </v-stepper>
        </v-container>
    </div>
</template>
<script>
import axios from "axios";
const API = "http://localhost:8089";
export default {
    name: "AgregarEnfermera",
    data: () => ({
        e1: 1,
        nuevaEnfermera: {}
    }),
// +----------------------------------------------------------+
// |                        METODOS                           |
// +----------------------------------------------------------+
    methods: {       
        agregar_enfermera(_enfermera) {
            axios
            .post(`${API}/mariadb`, _enfermera)
            .then((response) => {
                if (response.status === 200) {
                    this.$router.push('/TablaEnfermeras')
                }
            })
            .catch((err) => console.error(err));
        },        
    },
};
</script>
