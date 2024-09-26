<template>
  <div>
    <div class="top-row">
      <div class="top part">
        <img
          :src="availableParts.heads[currentHeadIndex].imageUrl"
          alt="head"
        />
        <button
          class="prev-selector"
          @click.prevent="selectNextHead('decrement')"
        >
          &#9668;
        </button>
        <button
          class="next-selector"
          @click.prevent="selectNextHead('increment')"
        >
          &#9658;
        </button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img
          :src="availableParts.arms[currentLeftArmIndex].imageUrl"
          alt="left arm"
        />
        <button class="prev-selector" @click.prevent="selectPreviousLeftArm()">
          &#9650;
        </button>
        <button class="next-selector" @click.prevent="selectNextLeftArm()">
          &#9660;
        </button>
      </div>
      <div class="center part">
        <img
          :src="availableParts.torsos[currentTorsoIndex].imageUrl"
          alt="torso"
        />
        <button class="prev-selector">&#9668;</button>
        <button class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img
          :src="availableParts.arms[currentRightArmIndex].imageUrl"
          alt="right arm"
        />
        <button class="prev-selector">&#9650;</button>
        <button class="next-selector">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img
          :src="availableParts.bases[currentBaseIndex].imageUrl"
          alt="base"
        />
        <button class="prev-selector">&#9668;</button>
        <button class="next-selector">&#9658;</button>
      </div>
    </div>
  </div>
</template>
<script>
import parts from "@/data/parts";

//Chris note:: IMO these should be moved into a utility file if they're used else where.
//For now they're just private functions.
/**
function getNextValidIndex(index, length) {
  const incrementedIndex = index + 1;
  return incrementedIndex > length - 1 ? 0 : incrementedIndex;
}

function getPreviousValidIndex(index, length) {
  const deprecatedIndex = index - 1;
  return deprecatedIndex < 0 ? length - 1 : deprecatedIndex;
}
*/

export default {
  name: "RobotBuilder",
  data() {
    return {
      availableParts: parts,
      currentHeadIndex: 0,
      currentLeftArmIndex: 0,
      currentRightArmIndex: 0,
      currentBaseIndex: 0,
      currentTorsoIndex: 0,
    };
  },
  methods: {
    //Chris Note: One of my key goals when it comes to functions is to ensure the cognitive complexity
    // stays belowe a threshold of 15.
    //In the tutorial the tutor creates a function each section and does a next/previous function.
    selectNextHead(direction = "increment") {
      this.currentHeadIndex =
        direction == "increment"
          ? this.currentHeadIndex + 1
          : this.currentHeadIndex - 1;

      if (this.currentHeadIndex == -1) {
        this.currentHeadIndex = this.availableParts.heads.length - 1;
      }

      if (this.currentHeadIndex > this.availableParts.heads.length - 1) {
        this.currentHeadIndex = 0;
      }
    },
    selectNextLeftArm() {},
    selectPreviousLeftArm() {},
    selectNextRightArm(direction = "increment") {
      this.currentRightArmIndex =
        direction == "increment"
          ? this.currentRightArmIndex + 1
          : this.currentRightArmIndex - 1;

      if (this.currentRightArmIndex == -1) {
        this.currentRightArmIndex = this.availableParts.arms.length - 1;
      }

      if (this.currentRightArmIndex > this.availableParts.arms.length - 1) {
        this.currentRightArmIndex = 0;
      }
    },
    selectNextBase() {},
  },
};
</script>
<style>
.part {
  position: relative;
  width: 200px;
  height: 200px;
  border: 3px solid #aaa;
}

.part img {
  width: 200px;
}

.top-row {
  display: flex;
  justify-content: space-around;
}

.middle-row {
  display: flex;
  justify-content: center;
}

.bottom-row {
  display: flex;
  justify-content: space-around;
  border-top: none;
}

.top {
  border-bottom: none;
}

.left {
  border-right: none;
}

.right {
  border-left: none;
}

.left img {
  transform: rotate(-90deg);
}

.right img {
  transform: rotate(90deg);
}

.bottom {
  border-top: none;
}

.prev-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 206px;
}

.next-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 206px;
}

.center .prev-selector,
.center .next-selector {
  opacity: 0.8;
}

.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 179px;
  height: 25px;
}

.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 179px;
  height: 25px;
}

.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 179px;
  height: 25px;
}

.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 179px;
  height: 25px;
}

.right .next-selector {
  right: -3px;
}
</style>
