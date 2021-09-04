<template>
  <div class="player">
    <h1 id="player">Player - {{ player }}</h1>
    <h1 id="total-score">
      Total Score <span class="score">{{ tScore }}</span>
    </h1>
    <div class="score-card">
      <h3>Current Score</h3>
      <h1 id="current-score">
        <span class="score">{{ ctScore }}</span>
      </h1>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    player: Number,
    tScore: Number,
    ctScore: Number,
  },
};
</script>

<style scoped>
.player {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 50px;
  height: 500px;
  width: 500px;
  box-shadow: 5px 10px 18px #888888;
}
.score-card {
  height: 120px;
  width: 180px;
  text-align: center;
  background-color: aquamarine;
  border-radius: 4px;
  margin-top: 180px;
}
.score {
  font-size: 50px;
  font-weight: 100;
}
</style>
