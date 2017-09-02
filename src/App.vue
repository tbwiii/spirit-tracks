<template>
  <div>
      <header>
        <h1 class="app-title">Ticket Counter</h1>
        <nav class="menu">
          <button class="menu-button" @click="playerCount++">Add Player</button>
        </nav>
      </header>

      <div class="player-cards">
        <score-card v-for="index in playerCount"></score-card>
      </div>
  </div>
</template>

<script>
import scoreCard from './ScoreCard.vue'
export default {
  name: 'app',
  components: {
    scoreCard: scoreCard
  },
  data () {
    return {
      playerCount: 2
    }
  }
}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

html,
body {
  margin: 0;
  padding: 0
}

body {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

header {
  overflow: auto;
  padding: 1em 2em;
}

h1, h2 {
  font-weight: normal;
}

a {
  color: #42b983;
}

.app-title {
  float: left;
}

.menu {
  float: right
}

.menu-button {
  background: #eee;
  border: 0;
  padding: 1em;
  font-size: 1em;
  margin-top: 1.5em;
  outline: 0;

  &:hover {
    cursor: pointer;
  }
}

.player-cards {
  display: flex;
  flex-wrap: wrap;
}
</style>
