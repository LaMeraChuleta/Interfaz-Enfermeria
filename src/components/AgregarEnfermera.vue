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
                    <v-stepper-step :complete="e1 > 2" step="2">Datos Academicos</v-stepper-step>
                    <v-divider></v-divider>
                    <v-stepper-step :complete="e1 > 3" step="3">Datos Vivienda</v-stepper-step>
                    <v-divider></v-divider>
                    <v-stepper-step :complete="e1 > 4" step="4">Datos Familiares</v-stepper-step>
                </v-stepper-header>
                <v-stepper-items>
                <!-- +-------------------------------------------------------------------+
                    |                         PASO NUMERO 1                              |
                    +-------------------------------------------------------------------+ -->
                    <v-stepper-content step="1">
                        <v-card>
                            <v-card-title>Nueva Enfermera</v-card-title>
                            <v-divider></v-divider>
                            <v-card-text class="mt-2">
                                <v-row>
                                    <v-col>
                                        <v-text-field v-model="datosPersonales.matricula" label="Matricula"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="datosPersonales.nombres" label="Nombre(s)"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="datosPersonales.apellido_m" label="Apellido Materno"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="datosPersonales.apellido_p" label="Apelldio Paterno"></v-text-field>
                                    </v-col>
                                </v-row>
                                <v-row>
                                    <v-col>
                                        <v-text-field v-model="datosPersonales.lugar_nacimiento" label="Lugar de Nacimiento"></v-text-field>
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
                                                v-model="datosPersonales.fecha_nacimiento"
                                                label="Fecha de Nacimiento"
                                                persistent-hint
                                                prepend-icon="mdi-calendar"
                                                v-bind="attrs"
                                                v-on="on"
                                            ></v-text-field>
                                        </template>
                                        <v-date-picker v-model="datosPersonales.fecha_nacimiento" no-title></v-date-picker>
                                        </v-menu>
                                    </v-col>
                                    <v-col>
                                        <v-checkbox v-model="datosPersonales.sexo" class="ma-0" value="F" label="Femenino" color="primary"></v-checkbox>
                                    </v-col>
                                    <v-col>
                                        <v-checkbox v-model="datosPersonales.sexo" class="ma-0" value="M" label="Masculino" color="primary"></v-checkbox>
                                    </v-col>
                                </v-row>
                                <v-row>
                                    <v-col>
                                        <v-text-field v-model="datosPersonales.tipo_enfermera" label="Tipo de Enfermera"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="datosPersonales.jornada" label="Jornada"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="datosPersonales.horario_labores" label="Horario Laboral"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="datosPersonales.descanso" label="Descanso"></v-text-field>
                                    </v-col>
                                </v-row>
                            <v-divider></v-divider>
                            </v-card-text>
                            <v-card-actions class="d-flex justify-end">
                                <v-btn text>Cancel</v-btn>
                                <v-btn color="primary" @click="e1 = 2">Continue</v-btn>
                            </v-card-actions>
                        </v-card>
                    </v-stepper-content>
                <!-- +-------------------------------------------------------------------+
                    |                           PASO NUMERO 2                            |
                    +-------------------------------------------------------------------+ -->
                    <v-stepper-content step="2">
                        <v-card>
                            <v-card-title>Estudios</v-card-title>
                            <v-divider></v-divider>
                            <v-card-text class="mt-2">
                                <v-row class="pa-0" >
                                    <v-col>                                        
                                        <v-row class="">
                                            <v-col cols="5">
                                                <v-text-field v-model="datosAcademicos.nivel_estudios" label="Nivel de Estudio"></v-text-field>
                                            </v-col>
                                            <v-col>
                                                <v-text-field v-model="datosAcademicos.titulo" label="Titulo"></v-text-field>
                                            </v-col>
                                        </v-row>
                                        <v-row>
                                            <v-col>
                                                <v-text-field v-model="datosAcademicos.institucion" label="Institucion"></v-text-field>
                                            </v-col>
                                        </v-row>
                                        <v-row>   
                                            <v-col cols="2">                                                
                                                <h3 class="mt-6 ml-5">De:</h3>  
                                            </v-col>
                                            <v-col cols="4">                  
                                                <v-text-field v-model="datosAcademicos.año_inicio" label="Año"></v-text-field>                                                
                                            </v-col>
                                            <v-col cols="2">                                                
                                                <h3 class="mt-6 ml-4">Hasta:</h3>   
                                            </v-col>
                                            <v-col cols="4">   
                                                <v-text-field v-model="datosAcademicos.año_fin" label="Año"></v-text-field>                                                
                                            </v-col>                                                                                                                                             
                                        </v-row>
                                        <v-row class="d-flex justify-end ">
                                            <v-btn text>Cancel</v-btn>
                                            <v-btn color="primary" @click="agregar_dato_academico(datosAcademicos)">Continue</v-btn>
                                        
                                        </v-row>
                                    </v-col>
                                    <v-col cols="6">
                                        <v-simple-table fixed-header height="255">
                                            <template v-slot:default>
                                                <thead>
                                                    <tr>
                                                        <th class="text-left">Nivel</th>
                                                        <th class="text-left">Titulo</th>
                                                        <th class="text-left"></th>
                                                    </tr>
                                                </thead>
                                                <tbody>
                                                <tr v-for="item in listaAcademica" :key="item.name">
                                                    <td>{{ item.nivel_estudios }}</td>
                                                    <td>{{ item.titulo }}</td>
                                                    <td>                                                        
                                                        <v-icon small class="mr-4">mdi-pencil</v-icon>                                                        
                                                        <v-icon small class="mr-4">mdi-delete</v-icon>
                                                    </td>
                                                </tr>
                                                </tbody>
                                            </template>
                                        </v-simple-table>
                                    </v-col>                                    
                                </v-row>
                            <v-divider></v-divider>
                            </v-card-text>
                            <v-card-actions class="d-flex justify-end">
                                <v-btn @click="e1 = 1" text>Cancel</v-btn>
                                <v-btn color="primary" @click="e1 = 3">Continue</v-btn>
                            </v-card-actions>
                        </v-card>                        
                    </v-stepper-content>
                <!-- +-------------------------------------------------------------------+
                    |                           PASO NUMERO 3                            |
                    +-------------------------------------------------------------------+ -->
                    <v-stepper-content step="3">
                        <v-card>
                            <v-card-title>Direccion</v-card-title>
                            <v-divider></v-divider>
                            <v-card-text class="mt-2 mb-10">
                                <v-row>
                                    <v-col>
                                        <v-text-field v-model="datosVivienda.estado" label="Estado"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="datosVivienda.delegacion" label="Delegacion"></v-text-field>
                                    </v-col>                               
                                    <v-col cols="5">
                                        <v-text-field v-model="datosVivienda.colonia" label="Colonia"></v-text-field>
                                    </v-col>                                 
                                </v-row>                            
                                <v-row>
                                    <v-col>
                                        <v-text-field v-model="datosVivienda.calle" label="Calle(s)"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="datosVivienda.cp" label="C.P"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="datosVivienda.num_ext" label="Numero Ext"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="datosVivienda.num_int" label="Numero Int"></v-text-field>
                                    </v-col>
                                </v-row>
                            <v-divider></v-divider>
                            </v-card-text>
                            <v-card-actions class="d-flex justify-end">
                                <v-btn @click="e1 = 2" text>Cancel</v-btn>
                                <v-btn color="primary" @click="e1 = 4">Continue</v-btn>
                            </v-card-actions>
                        </v-card>        
                    </v-stepper-content>
                <!-- +-------------------------------------------------------------------+
                    |                           PASO NUMERO 5                            |
                    +-------------------------------------------------------------------+ -->
                    <v-stepper-content step="4">
                        <v-card>
                            <v-card-title>Estudios</v-card-title>
                            <v-divider></v-divider>
                            <v-card-text class="mt-2">
                                <v-row>
                                    <v-col>                                        
                                        <v-row>
                                            <v-col>
                                                <v-text-field v-model="datosFamiliares.nombre" label="Nombre(s)"></v-text-field>
                                            </v-col>
                                            <v-col>
                                                <v-text-field v-model="datosFamiliares.apellido_m" label="Apellido Materno"></v-text-field>
                                            </v-col>
                                            <v-col>
                                                <v-text-field v-model="datosFamiliares.apellido_p" label="Apellido Paterno"></v-text-field>
                                            </v-col>
                                        </v-row>
                                        <v-row>   
                                            <v-col>                                                                                                               
                                                <v-text-field v-model="datosFamiliares.parentesco" label="Parentesco"></v-text-field>                                                
                                            </v-col>                                            
                                            <v-col>                                                                                                    
                                                <v-text-field v-model="datosFamiliares.edad" label="Edad"></v-text-field>                                                
                                            </v-col>                                                                                                                                             
                                        </v-row>
                                        <v-row class="d-flex justify-end mt-10">
                                            <v-btn @click="e1 = 1" text>Cancel</v-btn>
                                            <v-btn color="primary" @click="agregar_dato_familia(datosFamiliares)">Continue</v-btn>
                                        
                                        </v-row>
                                    </v-col>
                                    <v-col cols="6">
                                        <v-simple-table fixed-header height="255">
                                            <template v-slot:default>
                                                <thead>
                                                    <tr>
                                                        <th class="text-left">Nombre</th>
                                                        <th class="text-left">Parentesco</th>
                                                        <th class="text-left">Acciones</th>
                                                    </tr>
                                                </thead>
                                                <tbody>
                                                <tr v-for="(item, key) in listaFamiliares" :key="key">
                                                    <td>{{ `${item.nombre} ${item.apellido_m} ${item.apellido_p}` }}</td>
                                                    <td>{{ item.parentesco }}</td>
                                                    <td>
                                                        <v-icon small class="mr-4">mdi-pencil</v-icon>
                                                        <v-icon small class="mr-4">mdi-delete</v-icon>
                                                    </td>
                                                </tr>
                                                </tbody>
                                            </template>
                                        </v-simple-table>
                                    </v-col>                                    
                                </v-row>
                            <v-divider></v-divider>
                            </v-card-text>
                            <v-card-actions class="d-flex justify-end">
                                <v-btn @click="e1 = 3" text>Cancel</v-btn>
                                <v-btn color="primary">Continue</v-btn>
                            </v-card-actions>
                        </v-card>
                        
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
        datosPersonales: {},
        datosAcademicos: {},
        datosVivienda: {},
        datosFamiliares: {},
        listaAcademica: [],
        listaFamiliares: []       
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
        agregar_dato_academico(_nuevo_estudio){
            this.listaAcademica.push({ ..._nuevo_estudio });
            this.datosAcademicos = {}
        },
        agregar_dato_familia(_nuevo_familiar){
            this.listaFamiliares.push({ ..._nuevo_familiar });
            this.datosFamiliares = {}
        }

    },
};
</script>
