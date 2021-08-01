<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <h1>{{ title }}</h1>

          <Message v-if="message" :message="message" />

          <NewNote :note="note" @addNote="addNote" />
          <!-- note list -->
          <ul class="notes">
            <li class="note" v-for="(note, index) in notes" :key="index">
              <h2 class="note-header">{{ note.title }}</h2>
              <p class="note-description">{{ note.descr }}</p>
              <span class="note-date">{{ note.date }}</span>
            </li>
          </ul>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import Message from "@/components/Message.vue";
import NewNote from "./components/NewNote.vue";

export default {
  components: {
    Message,
    NewNote,
  },
  data() {
    return {
      title: "Notes App",
      note: {
        title: "",
        descr: "",
      },
      message: null,
      notes: [
        {
          title: "First note",
          descr: "Description for the first note",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Second note",
          descr: "Description for the second note",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Third note",
          descr: "Description for the third note",
          date: new Date(Date.now()).toLocaleString(),
        },
      ],
    };
  },
  methods: {
    addNote() {
      let { title, descr } = this.note;

      if (title === "") {
        this.message = "Title can not be blank!";
        return false;
      }

      this.notes.push({
        title,
        descr,
        date: new Date(Date.now()).toLocaleString(),
      });

      this.message = null;
      this.note.title = "";
      this.note.descr = "";
    },
  },
};
</script>

<style>
</style>
