<template>
  <!-- new note -->
  <div class="new-note">
    <label>Title</label>
    <input v-model="note.title" type="text" />
    <label>Priority</label>
    <select v-model="note.priority">
      <option value="" disabled>Choose a priority</option>
      <option value="low">Low</option>
      <option value="normal">Normal</option>
      <option value="high">High</option>
    </select>
    <label >Description</label>
    <textarea v-model="note.descr"></textarea>
    <button @click="addNote" class="btn btnPrimary">New note</button>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      required: true,
    },
  },
  methods: {
    addNote() {
      this.$emit("addNote", this.note);
    },
  },
};
</script>

<style lang="scss" scoped>
.new-note {
  text-align: center;
}

select {
  display: block;
  width: 100%;
  margin-bottom: 30px;
  border-radius: 20px;
  padding: 16px 26px;
  appearance: none;
}

button {
  margin: 20px 0;
}
</style>