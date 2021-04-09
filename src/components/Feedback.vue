<template>
  <div>
    <div class="notification is-success" v-if="questionIsCorrect">
      Das war richtig!
    </div>
    <div class="notification is-danger" v-else>Das war leider falsch.</div>
  </div>
</template>

<script>
export default {
  name: "Feedback",
  props: {
    questionIsCorrect: Boolean
  }
};
</script>

<style scoped>
.notification.is-success {
  margin-bottom: 1rem;
}

.notification.is-danger {
  margin-top: 1.5rem;
  margin-bottom: 1rem;
}
</style>
