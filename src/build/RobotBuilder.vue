<template>
  <div>
    <div class="top-row">
      <div class="top part">
        <div class="robot-name">{{selectedRobot.head.title}}</div>
        <img :src="selectedRobot.head.src" title="head"/>
        <button @click ="selectPreviousHead()" class="prev-selector">&#9668;</button>
        <button @click ="selectNextHead()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img :src="availableParts.arms[selectLeftArmIndex].src" title="left arm"/>
        <button class="prev-selector">&#9650;</button>
        <button class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img :src="availableParts.torsos[selectTorsorIndex].src" title="left arm"/>
        <button class="prev-selector">&#9668;</button>
        <button class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img :src="availableParts.arms[selectRightArmIndex].src" title="left arm"/>
        <button class="prev-selector">&#9650;</button>
        <button class="next-selector">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img :src="availableParts.bases[selectBaseIndex].src" title="left arm"/>
        <button class="prev-selector">&#9668;</button>
        <button class="next-selector">&#9658;</button>
      </div>
    </div>
  </div>
</template>

<script>
import availableParts from '../data/parts';

function NextIndex(index, length) {
  const increase = index + 1;
  return increase > length - 1 ? 0 : increase;
}
function PreviousIndex(index, length) {
  const previous = index - 1;
  return previous < 0 ? length - 1 : previous;
}

export default {
  name: 'RobotBuilder',
  data() {
    return {
      availableParts,
      selectHeadIndex: 0,
      selectLeftArmIndex: 0,
      selectTorsorIndex: 0,
      selectRightArmIndex: 0,
      selectBaseIndex: 0,
    };
  },
  computed: {
    selectedRobot() {
      return {
        head: availableParts.heads[this.selectHeadIndex],
        leftArm: availableParts.arms[this.selectLeftArmIndex],
        torso: availableParts.torsos[this.selectTorsorIndex],
        rightArm: availableParts.arms[this.selectRightArmIndex],
        base: availableParts.bases[this.selectBaseIndex],

      };
    },
  },
  methods: {
    selectNextHead() {
      this.selectHeadIndex = NextIndex(this.selectHeadIndex, availableParts.heads.length);
    },

    selectPreviousHead() {
      this.selectHeadIndex = PreviousIndex(this.selectHeadIndex, availableParts.heads.length);
    },
  },
};

</script>

<style>
.part {
  position: relative;
  width:165px;
  height:165px;
  border: 3px solid #aaa;
}
.part img {
  width:165px;
}
.top-row {
  display:flex;
  justify-content: space-around;
}
.middle-row {
  display:flex;
  justify-content: center;
}
.bottom-row {
  display:flex;
  justify-content: space-around;
  border-top: none;
}
.head {
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
  z-index:1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector, .center .next-selector {
  opacity:0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  right: -3px;
}
.robot-name{
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}
</style>
