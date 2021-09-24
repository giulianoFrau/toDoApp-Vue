<template>
  <span class="data">🗓️ {{ dataOdierna }} </span>
</template>

<script>
export default {
  data() {
    return {
      dataOdierna: "",
    };
  },
  created() {
    setInterval(this.getNow, 1000);
  },
  methods: {
    getNow() {
      const today = new Date();
      const date =
        today.getDate() +
        "/" +
        (today.getMonth() + 1) +
        "/" +
        today.getFullYear();

      const time =
        today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
      const dateTime = date + " " + time;
      this.dataOdierna = dateTime;
    },
  },
};
</script>

<style>
.data {
  color: white;
  font-size: 3rem;
  font-family: "Indie Flower", cursive;
}
</style>
