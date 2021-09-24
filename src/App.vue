<template>
  <div class="globalContainer d-flex align-items-center justify-content-center">
    <div v-if="alert" class="alert alert-primary" role="alert">
      This is a primary alert—check it out!
    </div>

    <form>
      <Title :titolo="titolo"></Title>
      <Clock></Clock>
      <hr />
      <Main></Main>
    </form>
  </div>
</template>

<script>
import Title from "./Title.vue";
import Clock from "./Clock.vue";
import Main from "./Main.vue";
export default {
  components: {
    Title,
    Clock,
    Main,
  },
  data() {
    return {
      titolo: "🖥️ To do Application 🖥️",
    };
  },
};
</script>

<style>
.globalContainer {
  height: 100vh;
  background-image: url(https://static.vecteezy.com/ti/foto-gratuito/p1/1854615-bolle-su-sfondo-nero-gratuito-foto.jpg);
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
}

form {
  width: 70%;
  padding: 2rem;
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(5px);
  -webkit-backdrop-filter: blur(5px);
  border-radius: 10px;
  border: 1px solid rgba(255, 255, 255, 0.18);
}
</style>
