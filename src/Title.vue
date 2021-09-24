<template>
  <h1 class="title">{{ titolo }}</h1>
</template>

<script>
export default {
  props: {
    titolo: {
      type: String,
      required: true,
    },
  },
};
</script>

<style>
.title {
  color: white;
}
</style>
