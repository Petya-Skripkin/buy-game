<template>
  <div class="main">
    <model-box-vue :game="game" @click="nextGame" />
    <div class="central">
      <my-counter-vue :name="'score'" :count="count" />
      <my-counter-vue :name="'product'" :count="product" />
    </div>
    <div class="level">
      <my-button
        v-for="level in levels"
        :key="level"
        class="getLevel"
        :class="nowLevel === level && 'getLevelActive'"
        @click="disLevel"
      >
        {{ level }}
      </my-button>
    </div>
    <div class="game">
      <my-button
        class="button"
        v-if="start.length < 2 && randomNumberPositive === 0 && !game.lose"
        style="background: rgb(229, 255, 0)"
        @click="Start"
        >Start</my-button
      >
      <div v-else class="bargain">
        <my-button
          class="button"
          :disabled="count < this.randomNumberPositive"
          style="background: chartreuse"
          @click="buy"
          >{{ this.randomNumberPositive }}</my-button
        >
        <my-button
          class="button"
          :disabled="product === 0"
          style="background: rgb(224, 7, 0)"
          @click="sale"
          >{{ this.randomNumberNegative }}</my-button
        >
      </div>
    </div>
    {{ err }}
    <p class="regulations">You win when you get 1000000 points or 100 products</p>
  </div>
</template>

<script>
import myCounterVue from "@/components/my-counter.vue";
import modelBoxVue from "./components/modelBox.vue";

export default {
  components: {
    myCounterVue,
    modelBoxVue,
  },
  data() {
    return {
      err: "",
      start: "",
      count: 5000,
      product: 0,
      randomNumberPositive: 0,
      randomNumberNegative: 0,
      nowLevel: "From 1000 to 5000",
      levels: [
        "From 1000 to 5000",
        "From 5000 to 10000",
        "From 10000 to 20000",
      ],
      game: {
        win: false,
        lose: false,
      },
    };
  },
  methods: {
    Start() {
      switch (this.nowLevel) {
        case "From 1000 to 5000":
          this.randomNumberPositive = Math.ceil(Math.random() * 4000 + 1000);
          this.randomNumberNegative = Math.floor(Math.random() * 4000 + 1000);
          break;
        case "From 5000 to 10000":
          this.randomNumberPositive = Math.ceil(Math.random() * 4000 + 5000);
          this.randomNumberNegative = Math.floor(Math.random() * 4000 + 5000);
          break;
        case "From 10000 to 20000":
          this.randomNumberPositive = Math.ceil(Math.random() * 9000 + 10000);
          this.randomNumberNegative = Math.floor(Math.random() * 9000 + 10000);
          break;
        default:
          this.start = "Not that level";
      }
    },
    disLevel(event) {
      this.nowLevel = event.target.innerText;
      event.target.disabled = true;
    },
    buy() {
      this.product++;
      this.count -= this.randomNumberPositive;
      this.Start();
    },
    sale() {
      this.product--;
      this.count += this.randomNumberNegative;
      this.Start();
    },
    nextGame() {
      window.location.reload()
    },
  },
  watch: {
    count(count) {
      if (count > 999999 || this.product > 99) {
        this.game.win = true;
      }
      if (count < this.randomNumberPositive && this.product < 1) {
        this.game.lose = true;
      }
    },
  },
};
</script>

<style>
* {
  margin: 0;
  border: 0;
}

.main {
  position: relative;
  height: 100vh;
  background-color: wheat;
}

.central {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5px 10px;
}

.level {
  position: fixed;
  top: 10%;
  right: 5%;
  display: flex;
  flex-direction: column;
}

.game {
  display: flex;
  justify-content: center;
}

.getLevel {
  margin: 2px 0;
  border-radius: 10px;
  background-color: rgb(105, 211, 0);
  text-align: center;
  cursor: pointer;
}

.getLevelActive {
  background-color: rgb(224, 7, 0);
  background-color: rgb(88, 175, 1);
}

.button {
  font-size: 40px;
  padding: 10px 20px;
  margin: 0 20px;
  margin-top: 100px;
}

.regulations {
  margin-top: 100px;
  text-align: center;
  color: lightslategray;
}
</style>
