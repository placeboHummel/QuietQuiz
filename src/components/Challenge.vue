<template>
  <div>
    <div class="notification vcentered" v-html="question"></div>
  </div>
</template>

<script>
export default {
  name: "Challenge",
  props: {
    question: String,
    questionIndex: Number
  }
};
</script>

<style scoped>
.tag {
  margin-bottom: 0.4rem;
}

.vcentered {
  display: flex;
  justify-content: center;
  align-items: center;
}

.notification {
  height: 8rem;
}
</style>
