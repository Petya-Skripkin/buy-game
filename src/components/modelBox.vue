<template>
  <div v-if="game.win || game.lose" class="model">
    <div class="model__content">
      <h1 v-if="game.win">You win!</h1>
      <h1 v-if="game.lose">You lose</h1>
      <my-button class="return" @click="Return">{{game.lose ? 'Try again' : 'Play again'}}</my-button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    game: {
      win: Boolean,
      lose: Boolean,
    },
  },
  methods: {
    Return() {
      this.$emit('click')
    }
  }
};
</script>

<style scoped>
.model {
  position: absolute;
  width: 100vw;
  height: 100vh;
  background-color: rgba(61, 60, 60, 0.466);
}

.model__content{
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  width: 40vw;
  height: 40vh;
  margin-left: auto;
  margin-right: auto;
  margin-top: 10%;
  border-radius: 10px;
  background: wheat;
  opacity: 0.8;
}

.return {
  font-size: 24px;
  padding: 5px 10px;
  background: burlywood;
}
</style>