<template>
    <v-sheet class="mt-10" >
        <div class="form-wrapper">
            <span type="button" class="close-btn" icon @click="closeForm"><v-icon>mdi-close</v-icon></span>
        </div>
        <v-form @submit.prevent>
            <v-text-field :rules="rules" label="Nombre" v-model="curso.nombre"></v-text-field>
            <v-text-field :rules="rules" label="URL de la imagen" v-model="curso.img" ></v-text-field>
            <v-text-field :rules="rules" label="Cupos del curso" v-model="curso.cupos"></v-text-field>
            <v-text-field :rules="rules" label="Inscritos en el curso" v-model="curso.inscritos"></v-text-field>
            <v-text-field :rules="rules" label="Duración del curso" v-model="curso.duracion"></v-text-field>
            <v-text-field :rules="rules" label="Fecha de registro" v-model="curso.fecha_registro"></v-text-field>
            <v-text-field :rules="rules" label="Costo del curso" v-model="curso.costo"></v-text-field>
            <v-textarea  :rules="rules" label="Descripción del curso" v-model="curso.descripcion"></v-textarea>
            <v-btn class="btn-form" color="green" @click="addCurso()">AGREGAR</v-btn>
            <v-btn class="btn-form" color="orange">LIMPIAR FORMULARIO</v-btn>
            <v-btn class="btn-form" color="red" @click="closeForm">CANCELAR</v-btn>
            
        </v-form>
    </v-sheet>
</template>


<script>
import store from '../store/index.js';
export default {
    data: () => {
        store;
        const today = new Date();
        const day = String(today.getDate()).padStart(2, '0');
        const month = String(today.getMonth() + 1).padStart(2, '0');
        const year = today.getFullYear();
        const formattedDate = `${day}-${month}-${year}`;
        return {
            rules: [
                value => !!value || 'Required',
            ],
            curso: {
                id:0,
                nombre: '',
                img: '',
                cupos: '',
                inscritos: '',
                duracion: '',
                fecha_registro: formattedDate,
                completado: false,
                costo: '',
                descripcion: '',
            }
        }
    },
   
    methods: {
        closeForm() {
            this.$emit('close'); 
        },
        addCurso() {
            if(parseInt(this.curso.inscritos) > parseInt(this.curso.cupos)) {
                alert('No se puede agregar el curso. La cantidad de inscritos en mayor que los cupos disponibles')
            } else {
                const cursos = this.$store.state.cursos;
                const newCurso = {
                id: cursos.length + 1,
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
                this.$store.dispatch('addCurso', newCurso);
                this.closeForm();
            }
        },
    },
}

</script>

<style scoped>
.v-sheet {
    width: 500px;
    border-radius: 10px;
    padding-top: 8px;
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