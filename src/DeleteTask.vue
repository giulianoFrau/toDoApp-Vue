<template>
  <li>
    <b>Task n°:</b> {{ j + 1 }} <br />
    <b>Titolo:</b> {{ titolo }} <br />
    <b>Descrizione:</b> {{ descrizione }} <br />
    <button
      class="btn btn-outline-success btn-lg but"
      @click.prevent="$emit('resume', j)"
    >
      Ripristina
    </button>
    <button
      class="btn btn-outline-danger btn-lg but"
      @click.prevent="$emit('deleteDefinitely', j)"
    >
      Cancella Definitivamente
    </button>
  </li>
</template>

<script>
export default {
  props: {
    j: {
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
