<template>
  <div class="addQuestion-wrapper">
    <button>Dodaj pitanje</button>
  </div>
</template>

<script>
export default {
  name: "AddQuestion",
  components: {},
  data() {
    return {};
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
  color: #2c3e50;
  font-size: 60px;
  line-height: 60px;
}

.addQuestion-wrapper {
  position: absolute;
  top: 0;
  right: 20px;
  button {
    padding: 16px;
    border-radius: 8px;
    background: green;
  }
}
</style>
