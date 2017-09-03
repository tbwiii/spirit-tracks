<template>
  <div class="player-card">
    <h2 class="player-name">
      <div @click="toggleEdit" v-if="editing === false">{{ name }}</div>
      <input ref="nameInput" v-if="editing === true" @blur="toggleEdit" @keyup.enter="toggleEdit" type="text" v-model="name">
    </h2>
    <ul class="track-cards">
      <li class="track-card" v-for="(line, key) in lines">
        <h3 class="track-title">{{ key }}</h3>
        <span class="track-amount">{{ line.amount }}</span>
        <div class="amount-buttons">
          <button class="amount-button" @click="remove(key)">-</button>
          <button class="amount-button" @click="add(key)">+</button>
        </div>
      </li>
    </ul>
    <p class="trains">{{ remainingTrains }} trains remaining</p>
    <h3 class="score">{{ score }}</h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "Player Name",
      editing: false,
      trains: 40,
      lines: {
        'One': {
          trains: 1,
          amount: 0,
          value: 1
        },
        'Two': {
          trains: 2,
          amount: 0,
          value: 2
        },
        'Three': {
          trains: 3,
          amount: 0,
          value: 4
        },
        'Four': {
          trains: 4,
          amount: 0,
          value: 7
        },
        'Five': {
          trains: 5,
          amount: 0,
          value: 10
        },
        'Six': {
          trains: 6,
          amount: 0,
          value: 15
        }
      } // lines
    }
  }, // data
  computed: {
    score() {
      let val = 0;
      for (var line in this.lines) {
        val = val + (this.lines[line].value * this.lines[line].amount);
      }

      return val;
    },
    remainingTrains() {
      let val = 40;
      for (var line in this.lines) {
        val = val - (this.lines[line].trains * this.lines[line].amount);
      }

      return val;
    }
  },
  methods: {
    toggleEdit() {
      this.editing = !this.editing;

      if (this.editing) {
        let self = this;
        this.name = '';
        this.$nextTick(function (){
          this.$refs.nameInput.focus();
        });
      } else {
        this.name = this.name ? this.name : 'Player Name'
      }
    },
    add(key) {
      this.lines[key].amount++;
    },
    remove(key) {
      if (this.lines[key].amount > 0) {
        this.lines[key].amount--;
      }
    }
  }
}
</script>

<style lang="scss">
.player-card {
  border: solid 1px #eee;
  flex-basis: calc(50% - 2em);
  justify-content: center;
  flex-direction: column;
  margin: 1em;
  padding: 1em;
}

.player-name {
  float: left;
}

.track-cards {
  clear: both;
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
}

.track-card {
  border: solid 1px #ddd;
  flex: 1;
  margin: 0 .2em;
  text-align: center;
}

.track-title {
  margin: .3em 0 0;
}

.track-amount {
  display: block;
  margin: 1em;
}

.amount-buttons {
  display: flex;
}

.amount-button {
  background: #eee;
  border: solid 1px #fff;
  color: #555;
  flex: 1;
  font-size: 1.2em;
  font-weight: bold;
  outline: 0;

  &:hover {
    cursor: pointer;
  }
}

.score {
  float: right;
  font-size: 2em;
  margin: 1em 0 0;
  padding: 0;
}

.trains {
  float: left;
}

input {
  border: 0;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  font-size: 1em;
  padding: 0;
}
</style>
