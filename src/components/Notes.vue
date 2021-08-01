<template>
  <!-- note list -->
  <ul class="notes">
    <li class="note" v-for="(note, index) in notes" :key="index">
      <div class="note-header">
        <p>{{ note.title }}</p>
        <p @click="removeNote(index)">x</p>
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
  methods: {
    removeNote(index) {
      console.log(`Note id ${index} removed`);
      this.$emit("remove", index);
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

  @media screen and (max-width: 768px) {
    width: 100%;
  }
}

.note + .note {
  @media screen and (max-width: 768px) {
    margin-top: 40px;
  }
}

.note:nth-child(n + 2) + .note {
  margin-top: 40px;
}

.note-header {
  display: flex;
  justify-content: space-between;
  align-items: center;

  p {
    color: #494ce8;
    font-size: 22px;
    font-weight: 700;

    &:last-of-type {
      cursor: pointer;
    }
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