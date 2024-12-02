<script>
import CitaCard from './components/CitaCard.vue';

export default {
    data() {
        return {
            form: {
                paciente: '',
                fecha: '',
                hora: '',
                gravedad: '',
                motivo: '',
            },
            citas: [],
        };
    },
    computed: {
        esFormularioValido() {
            const { paciente, fecha, hora, gravedad, motivo } = this.form;
            return paciente && fecha && hora && gravedad && motivo;
        },
    },
    methods: {
        agregarCita() {
            this.citas.push({ ...this.form });
            this.limpiarFormulario();
        },
        limpiarFormulario() {
            this.form = {
                paciente: '',
                fecha: '',
                hora: '',
                gravedad: '',
                motivo: '',
            };
        },
        eliminarCita(index) {
            this.citas.splice(index, 1);
        },
    },
    components: {
        CitaCard,
    },
};
</script>

<template>
    <div class="container">
        <h1>Administrador de Citas Médicas</h1>

        <form @submit.prevent="agregarCita">
            <div class="container__form">
                <div>
                    <label :class="{ 'label-error': !form.paciente }">Paciente</label>
                    <input v-model="form.paciente" type="text" />
                </div>

                <div>
                    <label :class="{ 'label-error': !form.fecha }">Fecha</label>
                    <input v-model="form.fecha" type="date" />
                </div>

                <div>
                    <label :class="{ 'label-error': !form.hora }">Hora</label>
                    <input v-model="form.hora" type="time" />
                </div>

                <div>
                    <label :class="{ 'label-error': !form.gravedad }">Gravedad</label>
                    <select v-model="form.gravedad">
                        <option disabled value="">Selecciona una gravedad</option>
                        <option>Baja</option>
                        <option>Media</option>
                        <option>Alta</option>
                    </select>
                </div>

                <div>
                    <label :class="{ 'label-error': !form.motivo }">Motivo</label>
                    <input v-model="form.motivo" type="text" />
                </div>
            </div>

            <button :disabled="!esFormularioValido">Agregar</button>
        </form>

        <p v-if="citas.length === 0" class="no-consultas">Aún no hay consultas registradas</p>

        <div class="container__citas">
            <div v-for="(cita, index) in citas" :key="index">
                <CitaCard :cita="cita" @eliminar-cita="eliminarCita(index)" />
            </div>
        </div>
    </div>
</template>

<style>
form {
    display: flex;
    flex-direction: column;
    gap: 10px;
    padding: 10px 15px;
    border-radius: 10px;
    border: 1px solid gray;
}
.container__form {
    display: flex;
    flex-direction: row;
    gap: 5px;
}
.container__form div {
    display: flex;
    flex-direction: column;
    gap: 5px;
}
input,
select {
    height: 30px;
    border: 1px solid gray;
    border-radius: 4px;
}
select {
    height: 32px;
}
.label-error {
    color: red;
}
.no-consultas {
    color: red;
}
button,
button:disabled {
    margin: 25px auto;
    width: 100px;
    background-color: grey;
    cursor: not-allowed;
}
.container__citas {
    display: flex;
    max-width: 700px;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 10px;
}
</style>
