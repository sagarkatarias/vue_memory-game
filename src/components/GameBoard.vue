<template>
  <div>
    <div class="container">
      <DashBoard
        v-bind="{
          turns: turns,
          finishGame: finishGame,
          createBoard: createBoard
        }"
      />
      <div class="game-board">
        <div
          class="card"
          :class="{ flipped: item.matched }"
          v-for="(item, index) in cards"
          :key="`${item.id + index}`"
          v-on:click="handleClick(item)"
        >
          <img
            :src="item.image"
            alt=""
            v-if="clickedOrDiscoverd(item)"
            v-on:click.stop
          />
          <img src="../assets/back.jpg" alt="" v-else />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { unsplashApplication } from '../config/unsplash';
import DashBoard from './DashBoard';
import _ from 'lodash';

export default {
  components: {
    DashBoard
  },
  data() {
    return {
      cards: [],
      found1: null,
      found2: null,
      turns: 0
    };
  },
  props: {
    columns: {
      type: Number,
      default: 4
    }
  },
  computed: {
    count() {
      return this.columns ** 2 / 2;
    },
    finishGame() {
      return this.cards.reduce((acc, act) => acc && act.matched, true);
    }
  },
  methods: {
    async createBoard() {
      const res = await axios.get(
        `https://api.unsplash.com/photos/random?count=${this.count}&orientation=squarish&client_id=${unsplashApplication}`
      );
      this.cards = [];
      this.turns = 0;
      res.data.forEach((image) => {
        this.cards.push({
          image: image.urls.thumb,
          matched: false,
          id: image.id
        });
        this.cards.push({
          image: image.urls.thumb,
          matched: false,
          id: image.id
        });
      });
      this.cards = _.shuffle(this.cards);
    },
    clickedOrDiscoverd(item) {
      return item.matched || item === this.found1 || item === this.found2;
    },
    handleClick(item) {
      if (!item.matched) {
        this.turns++;
      }
      if (!this.found1) {
        this.found1 = item;
      } else {
        if (!this.found2) {
          this.found2 = item;
          if (this.found1.image === this.found2.image) {
            this.found1.matched = true;
            this.found2.matched = true;
          }
        } else {
          this.found1 = item;
          this.found2 = null;
        }
      }
    }
  },
  mounted() {
    this.createBoard();
  }
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
}

.game-board {
  display: grid;
  grid-template-columns: 150px 150px 150px 150px;
  gap: 20px;
  perspective: 800px;
  cursor: pointer;
}

.card {
  width: 150px;
  height: 150px;
  transition: transform 1s;
  transform-style: preserve-3d;
}

.card.flipped {
  transform: rotateY(360deg);
}

.card:hover {
  cursor: pointer;
}

.card img {
  width: 100%;
  height: 100%;
}
</style>
