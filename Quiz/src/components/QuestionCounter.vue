<template>
  <div>
    <p>{{currentQuestion}} / {{questionLength}}</p>
  </div>
</template>

<script>
export default {
  name: "QuestionCounter",
  props: {
    currentQuestion: Number,
    questionLength: Number
  },
  components: {},

  data() {
    return {
     
    };
  },
  mounted() {
  },
  methods: {
    
  }
};
</script>

<style lang="scss">
h1 {
  color: #2c3e50;
  font-size: 60px;
  line-height: 60px;
}

</style>
