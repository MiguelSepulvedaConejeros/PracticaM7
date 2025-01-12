<template>
    <v-sheet class="mt-15" >
        <v-form @submit.prevent>
            <v-text-field type="text" v-model="curso.nombre" :rules="rules" label="Nombre"></v-text-field>
            <v-text-field type="url" v-model="curso.img" :rules="rules" label="URL de la imagen"></v-text-field>
            <v-text-field type="number" v-model="curso.cupos" :rules="rules" label="Cupos del curso"></v-text-field>
            <v-text-field type="number" v-model="curso.inscritos" :rules="rules" label="Inscritos en el curso"></v-text-field>
            <v-text-field type="text" v-model="curso.duracion" :rules="rules" label="Duración del curso"></v-text-field>
            <v-text-field v-model="curso.fecha_registro" :rules="rules" label="Fecha de registro"></v-text-field>
            <v-text-field placeholder="Ingrese sí o no" type="" v-model="curso.editCompletado" :rules="[valCompletado]" label="Terminado"></v-text-field>
            <v-text-field type="number" v-model="curso.costo" :rules="rules" label="Costo del curso"></v-text-field>
            <v-textarea type="text" v-model="curso.descripcion" :rules="rules" label="Descripción del curso"></v-textarea>
            <v-btn class="btn-form" color="green" @click="editCurso">EDITAR</v-btn>
            <v-btn class="btn-form" color="red" @click="closeEdit">CANCELAR</v-btn>
        </v-form>
    </v-sheet>
</template>

<script>
import store from '../store/index.js';
export default {
    store,
    props: {
        cursoId: {
            type: Number,
            required: true
    }
},
    data: () => {
        return {
            rules: [
                value => !!value || 'Required'
            ],
            curso: {
                id:0,
                nombre: '',
                img: '',
                cupos: '',
                inscritos: '',
                duracion: '',
                fecha_registro: '',
                editCompletado: '',
                completado: '',
                costo: '',
                descripcion: '',
            }
        }
    },
    mounted() {
        const curso = this.$store.state.cursos.find(curso => curso.id === this.cursoId);
        if (curso) {
            this.curso = { ...curso };
        }
    },
    methods: {
        valCompletado(value) {
        if (value === 'sí' || value === 'si') {
            this.curso.completado = true;
            return true;
        } else if (value === 'no') {
            this.curso.completado = false;
        }
        },
        editCurso() {
            if(parseInt(this.curso.inscritos) > parseInt(this.curso.cupos)) {
                alert('No se puede editar el curso. La cantidad de inscritos en mayor que los cupos disponibles')
            }
            if(this.curso.completado === true){
                this.curso.inscritos = 0;
            }
            this.curso.editCompletado = this.curso.completado

            const updatedData = {
                nombre: this.curso.nombre,
                img: this.curso.img,
                cupos: this.curso.cupos,
                inscritos: this.curso.inscritos,
                duracion: this.curso.duracion,
                fecha_registro: this.curso.fecha_registro,
                completado: this.curso.completado,
                costo: this.curso.costo,
                descripcion: this.curso.descripcion,
            };
        this.actualizarCurso(this.curso.id, updatedData);
        this.closeEdit();
        },
        actualizarCurso(id, updatedData) {
            this.$store.dispatch('editCursos', { id, updatedData });
        },
        closeEdit() {
            this.$emit('edit');
        }
    },
}
</script>

<style scoped>
.v-sheet {
    width: 500px;
    border-radius: 10px;
    padding: 8px;
}
.form-wrapper {
  position: relative;
  padding: 10px;
}
.close-btn{
    position: absolute;
    height: 10px;
    font-size: 12px;
    top: 1px;
    right: 4px; 
    box-shadow: none !important;
}
.btn-form{
    margin: 10px;
    color:white !important;
}
</style>