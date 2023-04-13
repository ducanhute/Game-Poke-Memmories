<template lang="">
  <div class="screen">
    <div class="screen__inner">
      <card-flip
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index: index, value: card }"
        :cardsContext="cardsContext"
        @onFlip="checkRule($event)"
      />
    </div>
    <div @click="onStartAgain" class="back-btn">
      <img src="@/assets/icon/back.png" alt="" />
    </div>
  </div>
</template>
<script>
import CardFlip from "@/components/CardItems.vue";
export default {
  components: {
    CardFlip,
  },
  data() {
    return {
      rules: [],
      cardDisable: [],
    };
  },
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },

  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    },
    checkRule(data) {
      this.rules.push(data);
      if (this.rules.length === 2) {
        for (let i = 0; i < this.cardsContext.length; i++) {
          this.$refs[`card-${i}`][0].onActiveDisabled();
        }
      }
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        // console.log("right");
        //Add class disabled to componets card
        this.cardDisable.push(this.rules[0].index);
        this.cardDisable.push(this.rules[1].index);
        this.$refs[`card-${this.rules[0].index}`][0].onActiveDisabled();
        this.$refs[`card-${this.rules[1].index}`][0].onActiveDisabled();
        // Active card after right
        setTimeout(() => {
          for (let i = 0; i < this.cardsContext.length; i++) {
            this.$refs[`card-${i}`][0].onUnActiveDisabled();
          }
        }, 500);
        // Reset the rules
        this.rules = [];
        // check end game
        const disabledElements = document.querySelectorAll(
          ".screen .card.disabled"
        );
        if (disabledElements.length === this.cardsContext.length - 2) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 1000);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        // console.log("Wrong");

        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          this.rules = [];
          // Active card after wrong
          setTimeout(() => {
            for (let i = 0; i < this.cardsContext.length; i++) {
              this.$refs[`card-${i}`][0].onUnActiveDisabled();
            }
          }, 200);
        }, 800);
      }
      //unactive click on list cardDisabled
      this.cardDisable.forEach((item) => {
        this.$refs[`card-${item}`][0].onActiveDisabled();
      });
    },
  },
};
</script>
<style lang="css" scoped>
.back-btn {
  position: absolute;
  top: 10px;
  left: 10px;
  width: 32px;
  cursor: pointer;
}
@media (min-width: 992px) {
  .back-btn {
    top: 15px;
    left: 15px;
    width: 50px;
  }
}
.back-btn img {
  width: 100%;
}
.screen {
  width: 100%;
  height: 100vh;
  top: 0;
  left: 0;
  z-index: 0;
  background-color: rgba(0, 0, 0, 0.7);
  color: var(--light);
  padding-left: 10px;
  padding-right: 10px;
  display: flex;
  align-items: center;
  position: relative;
}
@media (min-width: 678px) {
  .screen {
    padding-left: 30px;
    padding-right: 30px;
  }
}
@media (min-width: 991px) {
  .screen {
    padding-left: 100px;
    padding-right: 100px;
  }
}
.screen__inner {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  margin: auto;
}
</style>
