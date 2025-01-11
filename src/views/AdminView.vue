<template>
    <h1 class="titulo mt-7">Administración</h1>
    <v-btn @click="openForm" class="btn-agregar" color="primary">Agregar Curso</v-btn>
    <v-container class="text-left">
        <v-data-table hide-default-footer>
            <template v-slot:default>
                <thead>
                    <tr>
                        <th>Curso</th>
                        <th>Cupos</th>
                        <th>Inscritos</th>
                        <th>Duracion</th>
                        <th>Costos</th>
                        <th>Terminado</th>
                        <th>Fecha</th>
                        <th>Acciones</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="curso in cursos" :key="curso.id">
                        <td>{{ curso.nombre }}</td>
                        <td>{{ curso.cupos }}</td>
                        <td>{{ curso.inscritos }}</td>
                        <td>{{ curso.duracion }}</td>
                        <td><span class="cost-css">$ {{ curso.costo }}</span></td>
                        <td><span :class="curso.completado ? 'Si' : 'No'">{{ curso.completado ? 'Sí' : 'No' }}</span></td>
                        <td><span class="date-css">{{ curso.fecha_registro }}</span></td>
                        <td>
                            <v-icon @click="openEdit(curso)" color="yellow-darken-3" class="cursor-pointer mr-7">mdi-pencil</v-icon>
                            <v-icon @click="openElim(curso)" color="red darken-2" class="cursor-pointer ml-2">mdi-delete</v-icon>
                        </td>
                    </tr>
                </tbody>
            </template>
        </v-data-table>
        <v-alert class="alert-text" color="purple" variant="outlined"><span class="mdi mdi-account-multiple"></span> Cantidad total de alumnos permitidos: <strong>{{ alumnPermitidos }}</strong> alumnos.</v-alert>
        <v-alert class="alert-text" color="blue" variant="outlined"><span class="mdi mdi-account-check"></span> Cantidad total de alumnos inscritos: <strong>{{ alumnInscritos }}</strong> alumnos.</v-alert>
        <v-alert class="alert-text" color="red" variant="outlined"><span class="mdi mdi-account-multiple"></span> Cantidad total de cupos restantes: <strong>{{ alumnRestantes }}</strong> alumnos.</v-alert>
        <v-alert class="alert-text" color="pink" variant="outlined"><span class="mdi mdi-cancel"></span> Cantidad total de cursos terminados: <strong>{{alumnTerminados}}</strong> cursos.</v-alert>
        <v-alert class="alert-text" color="amber-accent-4" variant="outlined"><span class="mdi mdi-bell-ring"></span> Cantidad total de cursos activos: <strong>{{ cursosActivos }}</strong> cursos.</v-alert>
        <v-alert class="alert-text" color="orange-accent-4" variant="outlined"><span class="mdi mdi-bell-ring"></span> Cantidad total de cursos: <strong>{{ cursosTotales }}</strong> cursos.</v-alert>

        <div v-if="showForm" class="form-overlay">
            <div>
                <FormComp @close="closeForm"/>
            </div>
        </div>
        <div v-if="showEdit" class="form-overlay">
            <div>
                <EditarCurso :cursoId="selectedCursoId" @edit="closeEdit"/>
            </div>
        </div>
        <div v-if="showElim" class="form-overlay">
            <div>
                <AlertComp :cursoId="selectedCursoId" @closeAlert="closeElim" @elimCurso="elimCurso"/>
            </div>
        </div>
    </v-container>
</template>

<script>
import {mapState} from 'vuex'
import {mapGetters} from 'vuex'
import FormComp from '@/components/FormComp.vue'
import EditarCurso from '@/components/EditarCurso.vue'
import AlertComp from '@/components/AlertComp.vue'

export default{
    name: 'AdminView',
    components: {
        FormComp,
        EditarCurso,
        AlertComp,
    },
    data() {
        return {
            showForm: false,
            showEdit: false,
            showElim: false,
            selectedCursoId: null,
        };
    },
    methods: {
        elimCurso(id){
            this.$store.dispatch('elimCurso', id)
        },
        openForm() {
            this.showForm = true;
        },
        closeForm() {
            this.showForm = false;
        },
        openEdit(curso) {
            this.selectedCursoId = curso.id;
            this.showEdit = true;
        },
        closeEdit() {
            this.showEdit = false;
            this.selectedCursoId = null;
        },
        openElim(curso) {
            this.selectedCursoId = curso.id;
            this.showElim = true;
        },
        closeElim(){
            this.showElim = false;
            this.selectedCursoId = null;
        }
    },
    computed:{
        ...mapState(['cursos']),
        ...mapGetters(['alumnInscritos', 'alumnPermitidos', 'alumnRestantes','alumnTerminados', 'cursosActivos', 'cursosTotales']),
    }
}
</script>

<style scoped>
.Titulo{
  display: flex;
  justify-content: center;
  font-size: 60px;
  font-weight: 300;
}
.btn-agregar{
    display: flex;
    justify-self: center;
    margin-top: 40px;
    margin-bottom: 40px;
}
.alert-text{
    height: 40px;
    margin-top: 20px;
}
.cost-css{
    color: white;
    background-color: rgb(20, 160, 20);
    border-radius: 15px;
    padding: 5px;
}
.Si {
    color: white;
    background-color: rgb(20, 116, 160);
    border-radius: 15px;
    padding: 5px;
  }
.No {
    color: white;
    background-color: rgba(131, 128, 128, 0.596);
    border-radius: 15px;
    padding: 5px;
}
.date-css{
    color: white;
    background-color: rgb(20, 160, 20);
    border-radius: 15px;
    padding: 5px;
}
.form-overlay {
  position: fixed; 
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}
</style>