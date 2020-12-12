<template>  
  <div>
    <v-container>
      <!-- +-------------------------------------------------------------------+
          |                     TABLA ENFERMERAS                               |
          +-------------------------------------------------------------------+ -->    
      <v-row>
        <v-data-table      
          color="primary"
          :headers="headers"
          :items="enfermeras"
          :page.sync="page"
          :items-per-page="itemsPerPage"                
          item-key="matricula"
          show-expand
          :disable-sort="true"        
          hide-default-footer        
          class="elevation-1"
          @page-count="pageCount = $event"
        >
          <template v-slot:expanded-item="{ headers, item }">
          <td :colspan="headers.length">More info about {{ item.nombres + headers[0].text }}</td>
          </template>
          <template v-slot:item.actions="{ item }">       
          <div class="d-flex">   
            <v-icon small class="mr-4" @click="editar_enfermera(item.matricula, item, false)">mdi-pencil</v-icon>
            <v-icon small @click="delete_enfermera(item, false)">mdi-delete</v-icon>
          </div>
          </template>
        </v-data-table>
      </v-row>
      <!-- +-------------------------------------------------------------------+
          |                        PAGINACION                                 |
          +-------------------------------------------------------------------+ -->
      <v-row class="mt-2 justify-center">
        <v-pagination v-model="page" :length="pageCount"></v-pagination>
      </v-row> 
    </v-container>
        <!-- +-------------------------------------------------------------------+
        |                     MODAL CONFIRMAR ELIMINAR                      |
        +-------------------------------------------------------------------+ -->
    <v-dialog v-model="dialogDelete" persistent max-width="290">    
      <v-card>
        <v-card-title primary>Advertencia</v-card-title>
        <v-card-text>
          Seguro que quieres eliminar a la enfermera
          <p class="mt-5 font-weight-black">{{ `${enfemeraDelete.nombres}  ${enfemeraDelete.apellido_m} ${enfemeraDelete.apellido_p}` }}</p>          
          <p class="font-weight-black">{{`Matricula: ${enfemeraDelete.matricula}`}}</p>        
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="red" text @click="dialogDelete = false">No</v-btn>
          <v-btn color="green" text @click="delete_enfermera({},true)">Si</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <!-- +-------------------------------------------------------------------+
        |                     MODAL EDITAR ENFERMERA                         |
        +-------------------------------------------------------------------+ -->
    <v-dialog v-model="dialogEdit" persistent width="550">    
      <v-card>
        <v-card-title>Edicion Enfermera</v-card-title>
        <v-divider></v-divider>
        <v-card-text class="mt-2 mb-2">
            <v-row>
              <v-col>
                <v-text-field v-model="enfermeraEdit.matricula" label="Matricula"></v-text-field>
              </v-col>
              <v-col>
                <v-text-field v-model="enfermeraEdit.nombres" label="Nombre(s)"></v-text-field>
              </v-col>              
            </v-row>            
            <v-row>
              <v-col>
                <v-text-field v-model="enfermeraEdit.apellido_m" label="Apellido Materno"></v-text-field>
              </v-col>
              <v-col>
                <v-text-field v-model="enfermeraEdit.apellido_p" label="Apelldio Paterno"></v-text-field>
              </v-col>                                 
            </v-row>   
            <v-row>
              <v-col>                                
                  <v-checkbox v-model="enfermeraEdit.sexo" class="ma-0" value="F" label="Femenino" color="primary"></v-checkbox>                                                                                      
              </v-col>
              <v-col>                                                  
                  <v-checkbox v-model="enfermeraEdit.sexo" class="ma-0" value="M" label="Masculino" color="primary"></v-checkbox>                                                                     
              </v-col>     
            </v-row>          
            <v-row>
              <v-col>
                <v-text-field v-model="enfermeraEdit.lugar_nacimiento" label="Lugar de Nacimiento"></v-text-field>
              </v-col>
              <v-col>
                <v-menu :close-on-content-click="false"
                  transition="scale-transition"
                  offset-y
                  max-width="290px"
                  min-width="290px"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-text-field
                      v-model="enfermeraEdit.fecha_nacimiento"
                      label="Fecha de Nacimiento"                      
                      persistent-hint
                      prepend-icon="mdi-calendar"
                      v-bind="attrs"                      
                      v-on="on"
                    ></v-text-field>
                  </template>
                  <v-date-picker v-model="enfermeraEdit.fecha_nacimiento" no-title></v-date-picker>
                </v-menu>        
              </v-col>
            </v-row>             
            <v-row>
              <v-col>
                <v-text-field v-model="enfermeraEdit.tipo_enfermera" label="Tipo de Enfermera"></v-text-field>
              </v-col>
              <v-col>
                <v-text-field v-model="enfermeraEdit.jornada" label="Jornada"></v-text-field>
              </v-col>
              <v-col>
                <v-text-field v-model="enfermeraEdit.horario_labores" label="Horario Laboral"></v-text-field>
              </v-col>
              <v-col>
                <v-text-field v-model="enfermeraEdit.descanso" label="Descando"></v-text-field>
              </v-col>
            </v-row>
            <v-divider></v-divider>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="red" text @click="dialogEdit = false">Cancelar</v-btn>
          <v-btn color="green" text @click="editar_enfermera(matriculaEdit, enfermeraEdit, true)">Actualizar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>     
</template>

<script>
import axios from "axios";
const API = "http://localhost:8089";
export default {
  name: "TablaEnfermeras",
  data: () => ({
    page: 1,
    pageCount: 0,    
    itemsPerPage: 10,
    headers: [
      { text: "Matricula", value: "matricula" },
      { text: "Nombre(s)", value: "nombres" },
      { text: "Apellido Materno", value: "apellido_m" },
      { text: "Apellido Paterno", value: "apellido_p" },
      { text: "Sexo", value: "sexo" },
      { text: "Tipo de Enfermera", value: "tipo_enfermera" },
      { text: "Jornada", value: "jornada" },
      { text: "Horario de Labores", value: "horario_labores" },
      { text: "Descanso", value: "descanso" },
      { text: "Fecha de Nacimiento", value: "fecha_nacimiento" },
      { text: "Lugar de Nacimiento", value: "lugar_nacimiento" },
      { text: "", value: "actions" },
      { text: "", value: "data-table-expand" },
    ],
    enfermeras: [],
    enfemeraDelete: {},
    dialogDelete: false,
    enfermeraEdit: {},
    dialogEdit: false,
    nuevaEnfermera: {},
    matriculaEdit: '',        
    
  }),
// +----------------------------------------------------------+
// |                    CICLOS DE VIDA                        |
// +----------------------------------------------------------+
  beforeMount() {
    this.actualizar_tabla_enfermeras()
  },
// +----------------------------------------------------------+
// |                        METODOS                           |
// +----------------------------------------------------------+
  methods: {
    actualizar_tabla_enfermeras() {
      axios
      .get(`${API}/mariadb`)
      .then((response) => {
        if (response.status === 200) {          
          this.enfermeras = response.data;
        }
      }).catch((err) => console.error(err)); 
    },     
    delete_enfermera(_enfermera, _delete) {
      if(_delete){        
        axios
        .delete(`${API}/mariadb/${_enfermera.matricula}`)
        .then((response) => {
          if(response.status === 200) {  
            this.actualizar_tabla_enfermeras()
            this.dialogDelete = false
          }
        }).catch((err) => console.error(err))
      } else{
        this.dialogDelete = true
        this.enfemeraDelete = { ..._enfermera }
      }
    },
    editar_enfermera(_matriculaEdit, _enfermera, _edit) {
      if(_edit) {
        console.log('editar')
        axios
        .put(`${API}/mariadb/${_matriculaEdit}`,_enfermera)
        .then((response) => {
          if(response.status === 200) {  
            this.actualizar_tabla_enfermeras()
            this.dialogEdit = false
          }
        }).catch((err) => console.error(err))
      } else{        
        this.dialogEdit = true        
        this.enfermeraEdit =  { ..._enfermera }         
        this.matriculaEdit = _matriculaEdit       
      }
    },    
  }
};
</script>
