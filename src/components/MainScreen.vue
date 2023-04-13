<template>
  <div class="screen">
    <div>
      <h1 style="font-size: 80px; color: #f3f3f3; text-align: center">
        POKE MEMORIES
      </h1>
      <h3 style="text-align: center; font-size: 30px; color: #ff8383">
        Select mode to start game
      </h3>
      <div class="actions" style="padding-top: 30px; text-align: center">
        <button @click="onStart(4)">
          <p>2x2</p>
          <p>Easy</p>
        </button>
        <button @click="onStart(16)">
          <p>4x4</p>
          <p>Easy</p>
        </button>
        <button @click="onStart(36)">
          <p>6x6</p>
          <p>Normal</p>
        </button>
        <button @click="onStart(64)">
          <p>8x8</p>
          <p>Hard</p>
        </button>
        <button @click="onStart(100)">
          <p>10x10</p>
          <p>Supper Hard</p>
        </button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", { totalOfBlocks });
    },
  },
};
</script>
<style lang="css" scoped>
.screen {
  background: #212121;
  height: 100vh;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
}
.actions button {
  width: 110px;
  height: 130px;
  background: #212121;
  border: 3px solid #fff;
  border-radius: 10px;
  margin: 10px 10px;
  color: #fff;
  font-size: 1rem;
  cursor: pointer;
  font-weight: 600;
}
@media (max-width: 500px) {
  .actions button {
    width: 80px;
    height: 100px;
    background: #212121;
    border: 1px solid #fff;
    border-radius: 10px;
    margin: 10px 10px;
    color: #fff;
    font-size: 0.8rem;
    cursor: pointer;
    font-weight: 600;
  }
}
.actions button:hover {
  background: #ebebeb;
  color: #000;
  font-weight: 600;
}
</style>
