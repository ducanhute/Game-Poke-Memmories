<template lang="">
  <div class="screen">
    <div>
      <h1>✨ Congratulations ✨</h1>
      <p
        style="
          text-align: center;
          font-size: 26px;
          color: #c9b7b7;
          margin-top: 20px;
        "
      >
        You had finished the game in
        <span style="color: red">
          {{ Math.floor(timer / 1000) }}
        </span>
        Seconds
      </p>

      <div class="button1" style="text-align: center; margin: 20px auto">
        <span class="btn1" @click="onStartAgain">Start again</span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    timer: {
      type: Number,
      required: true,
    },
  },
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
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
h1 {
  font-size: 80px;
  color: #f3f3f3;
  text-align: center;
}
@media (max-width: 620px) {
  h1 {
    font-size: 40px;
  }
}
.button1 {
  background-image: linear-gradient(135deg, #008aff, #86d472);
  border-radius: 6px;
  box-sizing: border-box;
  color: #ffffff;
  display: block;
  height: 50px;
  font-size: 1.4em;
  font-weight: 600;
  padding: 4px;
  position: relative;
  text-decoration: none;
  width: 7em;
  z-index: 2;
}
.button1:hover {
  color: #fff;
}
.button1 .btn1 {
  align-items: center;
  cursor: pointer;
  background: #212121;
  border-radius: 6px;
  display: flex;
  justify-content: center;
  height: 100%;
  transition: background 0.5s ease;
  width: 100%;
}
.button1:hover .btn1 {
  background: transparent;
}
</style>
