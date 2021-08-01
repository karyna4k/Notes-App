<template>
  <!-- note list -->
  <ul class="notes">
    <li
      class="note"
      :class="{ full: !grid }"
      v-for="(note, index) in notes"
      :key="index"
    >
      <div class="note-header" :class="{ full: !grid }">
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
    grid: {
      type: Boolean,
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
  box-shadow: 0 30px 30px rgba($color: #000000, $alpha: 0.02);
  transition: all 0.25s cubic-bezier(0.02, 0.01, 0.47, 1);

  &:hover {
    box-shadow: 0 30px 30px rgba($color: #000000, $alpha: 0.04);
    transform: translate(0, -6px);
    transition-delay: 0s !important;
  }

  &.full {
    width: 100%;
    text-align: center;

    &:first-child {
      margin-bottom: 40px;
    }
  }
}

.note:nth-child(n + 2) + .note {
  margin-top: 40px;
}

.note-header {
  display: flex;
  justify-content: space-between;
  align-items: center;

  h1 {
    font-size: 32px;
  }

  p {
    color: #494ce8;
    font-size: 22px;
    font-weight: 700;

    &:last-of-type {
      cursor: pointer;
    }
  }

  svg {
    color: #999;
    cursor: pointer;

    &.active {
      color: #494ce8;
    }
  }

  svg + svg {
    margin-left: 12px;
  }

  &.full {
    justify-content: center;
    align-items: flex-start;

    p {
      &:first-child {
        flex-grow: 1;
        margin: 0 32px;
      }
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