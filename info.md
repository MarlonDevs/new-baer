<Card class="col-span-1 mt-2">
    <span>{{ note.description }}</span>&nbsp;
</Card>

<p v-for="note in notes">
    <b>* {{ note.description }}</b> &nbsp;
    <!-- nombre o descripcion del equipo -->
    <Button @click="deleteNotes(note.id)">delete</Button
    ><!-- Borrar de la lista -->
</p>
