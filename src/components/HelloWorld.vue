<template>
  <div id="wheel-container">
    <div id="wheel" :class="{ spin: spinning }">
      <div
        v-for="(piece, index) in wheelPieces"
        :key="index"
        :class="`piece piece-${piece}`"
      >
        <div class="value">
          <span>{{ piece }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      wheelPieces: ["A", "B", "C", "D"],
      usedWheelPieces: [],
      spinning: false,
    };
  },
  methods: {
    shuffle(array) {
      let currentIndex = array.length;
      let temporaryValue, randomIndex;

      while (0 !== currentIndex) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        temporaryValue = array[currentIndex];
        array[currentIndex] = array[randomIndex];
        array[randomIndex] = temporaryValue;
      }

      const firstValue = array[0];

      if (this.usedWheelPieces.includes(firstValue)) {
        return this.shuffle(array);
      } else {
        this.usedWheelPieces.push(firstValue);
        return array;
      }
    },
    spinWheel() {
      if (this.spinning) return;

      this.spinning = true;
      const pieces = this.shuffle([...this.wheelPieces]);
      this.wheelPieces = pieces;
      console.log(this.wheelPieces);

      console.log(this.usedWheelPieces);
      setTimeout(() => {
        this.spinning = false;
      }, 5000);
    },
  },
  mounted() {
    document.addEventListener("click", this.spinWheel);
  },
  beforeUnmount() {
    document.removeEventListener("click", this.spinWheel);
  },
};
</script>

<style lang="scss" scoped>
$size: 500;
$pieceCount: 22;
$pieceWidth: $size / $pieceCount;

#wheel-container {
  padding: 10px;
  position: relative;
  width: #{$size}px;
  height: #{$size}px;
  background: #ddd;

  &:before {
    content: "";
    position: absolute;
    z-index: 10;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    border: 15px solid transparent;
    border-top: 30px solid #222;
    border-bottom: none;
  }
}

@keyframes spin {
  0% {
    transform: rotate(-630deg);
  }
  100% {
    transform: rotate(90deg);
  }
}

#wheel {
  width: 100%;
  height: 100%;
  background: green;
  border-radius: 50%;
  position: relative;
  overflow: hidden;
  transform: rotate(-630deg);

  &.spin {
    animation: spin 5s ease-out;
  }

  .piece {
    position: absolute;
    border: #{$pieceWidth}px solid transparent;
    border-right: none;
    border-left: #{$size / 2}px solid yellowgreen;
    transform-origin: 100% 50%;
    top: 50%;
    left: 50%;
    transform: translate(-100%, -50%) rotate(0deg);

    &.piece-0x {
      color: red;
    }
    &.piece-2x {
      color: green;
    }
    &.piece-4x {
      color: gold;
    }

    .value {
      position: absolute;
      height: #{$size / 2}px;
      transform-origin: 100% 0;
      // I don't even...
      transform: rotate(-90deg) translate(50%, -100%);

      span {
        background: #222;
        padding: 5px;
        border-radius: 50%;
      }
    }
  }

  @for $i from 1 through $pieceCount {
    .piece:nth-child(#{$i}) {
      $deg: 360 / $pieceCount * $i - (360 / $pieceCount);
      transform: translate(-100%, -50%) rotate(#{$deg}deg);
    }
  }
}
</style>
