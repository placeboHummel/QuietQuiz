<template>
  <div>
    <div class="box" v-if="points === 0">
      Du hast leider
      <div class="failed">keine</div>
      Frage richtig beantwortet.
    </div>

    <div class="box" v-if="points === 1">
      Du hast immerhin
      <div class="points-one">{{ points }}</div>
      Frage richtig beantwortet.
    </div>

    <div class="box" v-if="points > 1">
      Du hast
      <div class="points-green">{{ points }}</div>
      Fragen richtig beantwortet!
    </div>
  </div>
</template>

<script>
export default {
  name: "Challenge",
  props: {
    points: Number
  }
};
</script>

<style scoped>
img {
  padding: 5px;
  width: 200px;
}

.failed {
  color: red;
  font-weight: bold;
  font-size: 80px;
}

.points-green {
  color: green;
  font-weight: bold;
  font-size: 80px;
}

.points-one {
  color: grey;
  font-weight: bold;
  font-size: 80px;
}
</style>
