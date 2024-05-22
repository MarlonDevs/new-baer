<template>
  <div class="grid grid-cols-2 gap-6">
    <Card class="col-span-1 mt-2 dark:bg-darkmode-600 shadow-md">
      <CardHeader>
        <h2
          class="text-lg font-semibold text-gray-800 dark:text-gray-200 text-center"
        >
          Control de Movimiento de Bienes Administrativos
        </h2>
      </CardHeader>
      <CardContent>
        <Input
          type="text"
          placeholder="Nombre del Equipo"
          v-model="formNotes"
        />
        <div class="grid grid-cols-2 gap-3">
          <Input
            type="text"
            placeholder="Marca del Equipo"
          />
          <Input
            type="text"
            placeholder="Modelo del Equipo"
          />
        </div>
        <Input type="text" placeholder="Color del Equipo" />
        <div class="grid grid-cols-2 gap-3">
          <Input
            type="text"
            placeholder="Serial del Equipo"
          />
          <Input
            type="text"
            placeholder="Numero de bien del Equipo"
          />
        </div>
        <div class="grid grid-cols-2 gap-3">
          <Input
            type="text"
            placeholder="Ubicacion del Equipo"
          />
          <Input
            type="text"
            placeholder="Aquien pertenece del Equipo"
          />
        </div>

        <!-- Campo para insertar texto para ser guardado en la base de datos -->
        <Button @click="addNewNotes()">add note</Button>
        <!-- Agregar la informacion del campo en la base de datos -->

        <!--
        <div class="col-span-1 mt-2" >
            <span v-for="note in notes">
                <p>{{ note.description }}</p>&nbsp;
            </span>
        </div>



        Card con la info

        <span class="text text-center">Nombre del Equipo</span>
        <div class="grid grid-cols-2 gap-3">
            <span>Nombre</span>
            <span>modelo</span>
        </div>
        <Input type="text" placeholder="Color del Equipo" v-model="formNotes" />
        <div class="grid grid-cols-2 gap-3">
            <span>Serial</span>
            <span>Numero de bien</span>
        </div>
        <div class="grid grid-cols-2 gap-3">
            <span>Ubicacion</span>
            <span>Propietario</span>
        </div>
        -->
      </CardContent>
      <CardFooter> </CardFooter>
    </Card>
  </div>
</template>
<script setup lang="ts">
import axios from "axios";
import {
  Card,
  CardContent,
  CardHeader,
  CardFooter,
  Input,
  Button,
} from "sigae-components";
import { onMounted, ref } from "vue";

const formNotes = ref("");
const notes = ref([]);

const API_URL = "http://localhost:3000/";

//funcion para agregar nuevas notas
const addNewNotes = async () => {
  axios
    .post(API_URL + "api/baer-db/AddNotes", {
      //se define los campos del formulario
      description: formNotes.value,
    })
    .then((response) => {
      //si todo sale bien actualizar la listra y mostar alerta
      refreshData();
      alert(response.data);
    });
};
//funcion para eliminar las notas
const deleteNotes = async (id: string) => {
  //se pasa el id por la ruta
  axios.delete(API_URL + "api/baer-db/DeleteNotes/" + id).then((response) => {
    //si todo sale bien actualizar la listra y mostar alerta
    refreshData();
    alert(response.data);
  });
};

//funcion para obtener las lista de notas
const refreshData = async () => {
  axios.get(API_URL + "api/baer-db/GetNotes").then((response) => {
    //actualizar la variable con la respuesta del servidor
    notes.value = response.data;
  });
};
//al cargar la pagina obtener el listado de notas
onMounted(() => {
  refreshData();
});
</script>
