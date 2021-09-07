<template>
  <v-container>
    <v-row class="mt-3 mt-md-6">

      <v-col cols="12" sm="6">
        <v-card class="mb-3" v-for="(tarea, index ) in listaTareas" :key="index">
          <v-card-text>
            <v-chip class="ma-2 ml-0" color="indigo darken-3" label text-color="white">
              <v-icon left>mdi-label</v-icon>
              {{tarea.titulo}} #{{tarea.id}}
            </v-chip>
            <p>{{tarea.descripcion}}</p>
              <v-btn color="warning" class="mr-3" @click="editar(index)">Editar</v-btn>
              <v-btn color="error" @click="eliminarTarea(index)">Eliminar</v-btn>
          </v-card-text>
        </v-card>
      </v-col>

      <v-col cols="12" sm="6" v-if="formAgregar">
        <v-card class="mb-3 px-5 py-4">
          <v-form @submit.prevent="agregarTarea">
            <v-text-field label="Título de la tarea" v-model="titulo"></v-text-field>
            <v-textarea label="Descripción de la tarea" v-model="descripcion"></v-textarea>
            <v-btn color="primary" type="submit" block>Agregar tarea</v-btn>
          </v-form>
        </v-card>
      </v-col>

      <v-col cols="12" sm="6" v-if="!formAgregar">
        <v-card class="mb-3 px-5 py-4">
          <v-form @submit.prevent="editarTarea">
            <v-text-field label="Título de la tarea" v-model="titulo"></v-text-field>
            <v-textarea label="Descripción de la tarea" v-model="descripcion"></v-textarea>
            <v-btn color="warning" type="submit" block>Editar tarea</v-btn>
          </v-form>
        </v-card>
      </v-col>

    </v-row>

    <v-snackbar
      v-model="snackbar"
    >
      {{ aviso }}

        <v-btn
          color="pink"
          text
          @click="snackbar = false"
        >
          Cerrar
        </v-btn>
    </v-snackbar>
  </v-container>
</template>

<script>

export default {
    name: 'Tareas-Crud',
    components: {  
    },
    data: () => ({
      listaTareas: [
        {  
          id: 1, 
          titulo: 'Ir al supermercado', 
          descripcion: 'Debo comprar: hamburguesas de soya, té verde, 3paltas, queso de cabra, ramitas de queso, 1 champaña brut, pétalos de algodón, pasta de dientes, desodorante, limpia vidrios.'
        }
      ],
      titulo: '',
      descripcion: '',
      snackbar: false,
      aviso: '',
      id: 2,
      formAgregar: true,
      indexTarea: ''
    }),
    methods: {
      agregarTarea() {
        if(this.titulo === '' || this.descripcion === '') {
          this.snackbar = true
          this.aviso = 'Debes rellenar todos los campos'
        } else {
          this.listaTareas.push({
            id: this.id ++,
            titulo: this.titulo,
            descripcion: this.descripcion
          })
          this.titulo = ''
          this.descripcion = ''
          this.snackbar = true
          this.aviso = 'Tarea agregada! '
        }
      },
      eliminarTarea(index) {
        this.listaTareas.splice(index, 1);
      },
      editar(index) {
        this.formAgregar = false
        this.titulo = this.listaTareas[index].titulo
        this.descripcion = this.listaTareas[index].descripcion
        this.indexTarea = index
      },
      editarTarea() {
        this.listaTareas[this.indexTarea].titulo = this.titulo
        this.listaTareas[this.indexTarea].descripcion = this.descripcion
        this.formAgregar = true

        this.titulo = ''
        this.descripcion = ''
        this.snackbar = true
        this.aviso = 'Tarea editada! '
      }
    }
  }
</script>

<style scoped>

</style>