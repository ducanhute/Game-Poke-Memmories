<template>
  <div
    class="card"
    :class="{
      disabled: isDisabled,
      styleBelow100Box: cardsContext.length < 101,
      styleBelow16Box: cardsContext.length < 17,
    }"
    :style="{
      height: `${90 / Math.sqrt(this.cardsContext.length)}vh`,
      width: `${100 / Math.sqrt(this.cardsContext.length)}% `,
    }"
  >
    <div
      class="card__inner"
      :class="{ 'is-flipped': isFlipped }"
      @click="onToggleFlipCard"
    >
      <div class="card__face card__face--front">
        <div class="card__content"></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + imgBackFaceUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    card: {
      type: [String, Number, Array, Object],
    },
    imgBackFaceUrl: {
      type: String,
      required: true,
    },
    cardsContext: {
      type: [Array],
      default: () => {
        [];
      },
    },
  },
  data() {
    return {
      isFlipped: false,
      isDisabled: false,
    };
  },
  methods: {
    onToggleFlipCard() {
      if (this.isDisabled) return false;
      this.isFlipped = !this.isFlipped;
      // console.log(this.card);
      if (this.isFlipped) this.$emit("onFlip", this.card);
    },
    // Close funtion will be call in interact
    onFlipBackCard() {
      this.isFlipped = false;
    },
    onActiveDisabled() {
      this.isDisabled = true;
    },
    onUnActiveDisabled() {
      this.isDisabled = false;
    },
  },
};
</script>
<style lang="css" scoped>
.styleBelow100Box {
  padding: 2px;
}
.styleBelow16Box {
  padding: 10px;
}
.card {
  display: inline-block;
}
.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.card__inner.is-flipped {
  transform: rotateY(-180deg);
}
.card__face {
  width: 100%;
  height: 100%;
  position: absolute;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 10px;
  padding: 1rem;
  background: rgba(0, 0, 0, 0.7);
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}
.card__face--front .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  background-size: 30px;
  width: 100%;
  height: 100%;
}
.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
.card__face--back .card__content {
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
}
.card.disabled .card__inner {
  cursor: default;
}
</style>
