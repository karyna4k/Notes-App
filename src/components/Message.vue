<template>
  <div class="message">
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.message {
  padding: 20px;
  text-align: center;
}

p {
  color: #ba3838;
}
</style>