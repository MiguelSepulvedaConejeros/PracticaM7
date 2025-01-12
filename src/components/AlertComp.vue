<template>
    <v-container>
        <v-row class="container">
            <div>
                <p class="mb-3 ml-5">Seguro de eliminar el curso</p>
                <v-btn class="mr-5" @click="elimCurso" color="green">ACEPTAR</v-btn>
                <v-btn @click="closeAlert" color="red">CANCELAR</v-btn>
            </div>
        </v-row>
    </v-container>
</template>

<script>
export default{
    props: {
        cursoId: {
            type: Number,
            required: true
        }
    },
    name: 'AlertComp',
    methods: {
        elimCurso(){
            this.$emit('elimCurso', this.cursoId)
            this.closeAlert();
        },
        closeAlert() {
            this.$emit('closeAlert');
        }
    }
}
</script>

<style scoped>
.container{
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #e0e8ec;
    width: 330px;
    height: 100px;
    border-radius: 5px;
}
</style>