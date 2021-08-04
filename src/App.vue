<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <!-- message -->
          <Message v-if="message" :message="message" />

          <!-- new note -->
          <NewNote :note="note" @addNote="addNote" />

          <!-- title -->
          <div class="note-header">
            <h1>{{ title }}</h1>

            <Search
              :value="search"
              placeholder="Find your note"
              @search="search = $event"
            />

            <!-- icons control -->
            <div class="icons">
              <svg
                :class="{ active: grid }"
                @click="grid = true"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <rect x="3" y="3" width="7" height="7"></rect>
                <rect x="14" y="3" width="7" height="7"></rect>
                <rect x="14" y="14" width="7" height="7"></rect>
                <rect x="3" y="14" width="7" height="7"></rect>
              </svg>
              <svg
                :class="{ active: !grid }"
                @click="grid = false"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <line x1="8" y1="6" x2="21" y2="6"></line>
                <line x1="8" y1="12" x2="21" y2="12"></line>
                <line x1="8" y1="18" x2="21" y2="18"></line>
                <line x1="3" y1="6" x2="3" y2="6"></line>
                <line x1="3" y1="12" x2="3" y2="12"></line>
                <line x1="3" y1="18" x2="3" y2="18"></line>
              </svg>
            </div>
          </div>

          <!-- note list -->
          <Notes :notes="notesFilter" :grid="grid" @remove="removeNote" />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import Message from "@/components/Message.vue";
import NewNote from "./components/NewNote.vue";
import Notes from "./components/Notes.vue";
import Search from "./components/Search.vue";

export default {
  components: {
    Message,
    NewNote,
    Notes,
    Search,
  },
  data() {
    return {
      title: "Notes App",
      search: "",
      message: null,
      grid: true,
      note: {
        title: "",
        descr: "",
        priority: "normal"
      },
      notes: [
        {
          title: "First note",
          descr: "Description for the first note",
          priority: "normal",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Second note",
          descr: "Description for the second note",
          priority: "low",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Third note",
          descr: "Description for the third note",
          priority: "high",
          date: new Date(Date.now()).toLocaleString(),
        },
      ],
    };
  },
  computed: {
    notesFilter() {
      let array = this.notes;
      let search = this.search;

      if (!search) return array;
      // small
      search = search.trim().toLowerCase();
      // filter
      array = array.filter((item) => {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item;
        }
      });
      // error
      return array;
    },
  },
  methods: {
    addNote() {
      let { title, descr, priority } = this.note;

      if (title === "") {
        this.message = "Title can not be blank!";
        return false;
      }

      this.notes.push({
        title,
        descr,
        priority,
        date: new Date(Date.now()).toLocaleString(),
      });

      this.message = null;
      this.note.title = "";
      this.priority = "normal";
      this.note.descr = "";
    },
    removeNote(index) {
      this.notes.splice(index, 1);
    },
  },
};
</script>

<style>
</style>
