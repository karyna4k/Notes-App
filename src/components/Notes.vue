<template>
  <!-- note list -->
  <ul class="notes">
    <li class="note" v-for="(note, index) in notes" :key="index">
      <div class="note-header">
        <p>{{ note.title }}</p>
      </div>
      <div class="note-body">
        <p>{{ note.descr }}</p>
        <span>{{ note.date }}</span>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style lang="scss">
.notes {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  padding: 40px 0;
}

.note {
  width: calc((100% - 40px) / 2);
  padding: 20px;
  background-color: #fff;
}

.note:nth-child(n + 2) + .note {
  margin-top: 40px;
}

.note-header {
  p {
    color: #494ce8;
    font-size: 22px;
    font-weight: 700;
  }
}

.note-body {
  p {
    margin: 20px 0;
  }

  span {
    font-size: 14px;
    color: #999;
  }
}
</style>