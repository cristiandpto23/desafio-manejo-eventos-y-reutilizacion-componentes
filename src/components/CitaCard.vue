<script>
export default {
    props: {
        cita: Object,
    },
    computed: {
        gravedadClass() {
            switch (this.cita.gravedad) {
                case 'Baja':
                    return 'gravedad-baja';
                case 'Media':
                    return 'gravedad-media';
                case 'Alta':
                    return 'gravedad-alta';
                default:
                    return '';
            }
        },
    },
    methods: {
        eliminarCita() {
            this.$emit('eliminar-cita');
        },
    },
};
</script>

<template>
    <div :class="['cita-card', gravedadClass]">
        <p><strong>Paciente:</strong> {{ cita.paciente }}</p>
        <p><strong>Fecha:</strong> {{ cita.fecha }}</p>
        <p><strong>Hora:</strong> {{ cita.hora }}</p>
        <p><strong>Motivo:</strong> {{ cita.motivo }}</p>
        <button @click="eliminarCita">Eliminar</button>
    </div>
</template>

<style>
.cita-card {

    border: 1px solid black;
    padding: 10px;
    margin: 10px 0;
    width: 175px;
}
.gravedad-baja {
    background-color: lightgreen;
}
.gravedad-media {
    background-color: yellow;
}
.gravedad-alta {
    background-color: red;
}
</style>
