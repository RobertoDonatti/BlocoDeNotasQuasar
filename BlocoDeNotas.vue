<template>
  <q-page>
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          round
          dense
          icon="save"
          @click="saveNote"
          :disable="!noteContent.trim()"
        />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <q-input
        v-model="noteTitle"
        label="Título"
        dense
        outlined
        class="q-mb-md"
      />

      <q-input
        v-model="noteContent"
        label="Anotações"
        dense
        outlined
        type="textarea"
        rows="8"
      />
    </q-page-container>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      noteTitle: "",
      noteContent: "",
    };
  },
  methods: {
    saveNote() {
      if (this.noteContent.trim()) {
        const note = {
          title: this.noteTitle,
          content: this.noteContent,
        };

        const savedNotes = JSON.parse(localStorage.getItem("notes")) || [];

        savedNotes.push(note);

        localStorage.setItem("notes", JSON.stringify(savedNotes));

        this.noteTitle = "";
        this.noteContent = "";

        console.log("Nota salva!");
      }
    },
  },
};
</script>
