<template>
  <li>
    <b>Task n°:</b> {{ i + 1 }} <br />
    <b>Titolo:</b> {{ titolo }} <br />
    <b>Descrizione:</b> {{ descrizione }} <br />
    <button
      class="btn btn-outline-danger btn-lg but"
      @click.prevent="$emit('deleteTask', i)"
    >
      Cancella
    </button>
  </li>
</template>

<script>
export default {
  props: {
    i: {
      type: Number,
    },
    titolo: {
      type: Array,
    },
    descrizione: {
      type: Array,
    },
  },
};
</script>

<style></style>
