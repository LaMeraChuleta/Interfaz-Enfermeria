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
                                        <v-select v-model="datosPersonales.tipo_enfermera" item-text="descripcion" item-value="id" :items="tipoEnfermera" label="Tipo de Enfermera"></v-select>
                                    </v-col>
                                    <v-col>                                        
                                        <v-select v-model="datosPersonales.jornada" :items="tipoJornada" label="Jornada"></v-select>
                                    </v-col>
                                    <v-col>                                        
                                        <v-select @change="formato_descansos" v-model="datosPersonales.horario_labores" :items="tipoHorario" label="Horario Laboral"></v-select>
                                    </v-col>
                                    <v-col>                                        
                                        <v-select v-model="datosPersonales.descanso" :items="tipoDescanso" label="Descanso"></v-select>                                        
                                    </v-col>
                                </v-row>
                                <v-row>
                                    <v-col>
                                        <v-text-field v-model="datosPersonales.curp" label="CURP"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model="datosPersonales.telefono" label="Telefono"></v-text-field>
                                    </v-col>                                  
                                </v-row>
                            <v-divider></v-divider>
                            </v-card-text>
                            <v-card-actions class="d-flex justify-end">
                                <v-btn text>Cancel</v-btn>
                                <v-btn color="primary" @click="agregar_enfermera(datosPersonales, 1)">Continue</v-btn>
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
                                                <v-text-field v-model="datosAcademicos.nivel" label="Nivel de Estudio"></v-text-field>
                                            </v-col>
                                            <v-col>                                                
                                                <v-select v-model="datosAcademicos.titulo" :items="tipoTitulo" label="Titulo"></v-select>
                                            </v-col>                                           
                                        </v-row>
                                        <v-row>
                                            <v-col cols="8">
                                                <v-text-field v-model="datosAcademicos.institucion" label="Institucion"></v-text-field>
                                            </v-col>
                                            <v-col>
                                                <v-select v-model="datosAcademicos.tipo_escuela" :items="tipoEscuela" label="Tipo Escuela"></v-select>
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
                                                    <td>{{ item.nivel }}</td>
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
                                <v-btn color="primary" @click="agregar_enfermera(listaAcademica, 2)">Continue</v-btn>
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
                                        <v-text-field v-model.number="datosVivienda.num_ext" label="Numero Ext"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field v-model.number="datosVivienda.num_int" label="Numero Int"></v-text-field>
                                    </v-col>
                                </v-row>
                            <v-divider></v-divider>
                            </v-card-text>
                            <v-card-actions class="d-flex justify-end">
                                <v-btn @click="e1 = 2" text>Cancel</v-btn>
                                <v-btn color="primary" @click="agregar_enfermera(datosVivienda, 3)">Continue</v-btn>
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
                                                <v-text-field v-model="datosFamiliares.nombres" label="Nombre(s)"></v-text-field>
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
                                                <v-text-field v-model.number="datosFamiliares.edad" label="Edad"></v-text-field>                                                
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
                                                    <td>{{ `${item.nombres} ${item.apellido_m} ${item.apellido_p}` }}</td>
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
                                <v-btn color="primary" @click="agregar_enfermera(listaFamiliares, 4)">Continue</v-btn>
                            </v-card-actions>
                        </v-card>
                        
                    </v-stepper-content>
                </v-stepper-items>
            </v-stepper>
            <div class="text-center">
                <v-snackbar color="red darken-2" v-model="errorModal" timeout="2000" :vertical="true">
                    {{ error  }}
                    <template v-slot:action="{ attrs }">
                        <v-btn color="grey lighten-2" text v-bind="attrs" @click="errorModal = false">Cerrar</v-btn>
                    </template>
                </v-snackbar>
            </div>
        </v-container>
    </div>
</template>
<script>
import axios from "axios";
const STEP_NUEVA_ENFERMERA = Object.freeze({
    datosPresonales: 1,
    datosAcademicos: 2,
    datosVivienda: 3,
    datosFamiliares: 4
})
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
        listaFamiliares: [],
        //Catalogos
        tipoEscuela: ['Publica', 'Privada'],
        tipoTitulo: ['Diploma', 'Constancia'],
        tipoJornada: ['8hrs', '12hrs'],
        tipoHorario: [
            {value: 'Matutino', text: 'Matutino 07:00 - 15:00'},
            {value: 'Vespertino', text: 'Vespertino 14:00 - 21:30'},
            {value: 'Nocturno', text: 'Nocturno 20:30 - 08:10'},
        ],
        tipoDescanso: [],
        tipoEnfermera: [], 
        errorModal: false,
        error: ''
        
        
    }),
// +----------------------------------------------------------+
// |                     CICLOS DE VIDA                       |
// +----------------------------------------------------------+
    beforeMount(){
        axios
            .get(`${API}/catalogo/tipoEnfermera`)
            .then((response) => {
                if (response.status === 200) {
                    this.tipoEnfermera = response.data
                }
            })
        .catch((err) => console.error(err));
    },
// +----------------------------------------------------------+
// |                        METODOS                           |
// +----------------------------------------------------------+
    methods: {       
        agregar_enfermera(_new_info, _step) {
            
            let url = ''
            switch(_step){
                case STEP_NUEVA_ENFERMERA.datosPresonales:
                    url = 'enfermera'
                    break;
                case STEP_NUEVA_ENFERMERA.datosAcademicos:
                    url = 'estudios'                                        
                    break
                case STEP_NUEVA_ENFERMERA.datosVivienda:
                    _new_info["id_enfermera"] = this.datosPersonales.matricula
                    url = 'vivienda'
                    break;
                case STEP_NUEVA_ENFERMERA.datosFamiliares:                    
                    url = 'familia'
                    break;
                default:
                    alert('error')
                    break;
            }            
            //Si es true Itera las Lista de Estudios o de Familia
            if(_step % 2 === 0){
                for(let item of _new_info){
                    //Se agregar los id´s de la enfermera
                    item["id_enfermera"] = this.datosPersonales.matricula
                    if(_step === 2)
                        item["id_estudio"] = 0
                    if(_step === 4)
                        item["id_familia"] = 0                                     
                    axios
                        .post(`${API}/${url}`, item)
                        .then((response) => {                
                            if (response.status === 200) {
                                console.log(response)
                                this.e1 = _step + 1
                                if(_step === 4){
                                    this.$router.push('/TablaEnfermeras')
                                }
                            }
                        })
                    .catch((err) => console.error(err)); 
                } 
            //Manda el objeto directo sin iterar
            } else {                
                axios
                    .post(`${API}/${url}`, _new_info)
                    .then((response) => {                
                        if (response.status === 200) {
                            console.log(response)
                            this.e1 = _step + 1
                            if(_step === 4){
                                this.$router.push('/TablaEnfermeras')
                            }
                        }
                    })
                .catch((err) => {
                    this.errorModal = true
                    this.error = err
                });  
            }                   
        },  
        agregar_dato_academico(_nuevo_estudio){
            this.listaAcademica.push({ ..._nuevo_estudio });
            this.datosAcademicos = {}
        },
        agregar_dato_familia(_nuevo_familiar){
            this.listaFamiliares.push({ ..._nuevo_familiar });
            this.datosFamiliares = {}
        },
        formato_descansos(){
            if(this.datosPersonales.horario_labores === 'Nocturno'){
                this.tipoDescanso = ['Domingo', 'Lunes', 'Martes', 'Miercoles', 'Jueves', 'Viernes', 'Sabado'] 
            } else{
                this.tipoDescanso = ['Domingo-Lunes', 'Lunes-Martes', 'Martes-Miercoles', 'Miercoles-Jueves', 'Jueves-Viernes', 'Viernes-Sabado']
            }
        }

    },
};
</script>
