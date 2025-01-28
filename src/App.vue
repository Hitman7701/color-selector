<script setup>
import { ref } from 'vue'

const colorsList = ref([
  [
    'rgb(245, 245, 245)',
    'rgb(238, 238, 238)',
    'rgb(189, 189, 189)',
    'rgb(158, 158, 158)',
    'rgb(97, 97, 97)',
    'rgb(66, 66, 66)',
    'rgb(0, 0, 0)',
  ],
  [
    'rgb(255, 205, 210)',
    'rgb(239, 154, 154)',
    'rgb(239, 83, 80)',
    'rgb(244, 67, 54)',
    'rgb(211, 47, 47)',
    'rgb(198, 40, 40)',
    'rgb(183, 28, 28)',
  ],
  [
    'rgb(225, 190, 231)',
    'rgb(206, 147, 216)',
    'rgb(171, 71, 188)',
    'rgb(156, 39, 176)',
    'rgb(123, 31, 162)',
    'rgb(106, 27, 154)',
    'rgb(74, 20, 140)',
  ],
  [
    'rgb(187, 222, 251)',
    'rgb(144, 202, 249)',
    'rgb(66, 165, 245)',
    'rgb(33, 150, 243)',
    'rgb(25, 118, 210)',
    'rgb(21, 101, 192)',
    'rgb(13, 71, 161)',
  ],
  [
    'rgb(200, 230, 201)',
    'rgb(197, 225, 165)',
    'rgb(102, 187, 106)',
    'rgb(76, 175, 80)',
    'rgb(56, 142, 60)',
    'rgb(46, 125, 50)',
    'rgb(27, 94, 32)',
  ],
  [
    'rgb(255, 236, 179)',
    'rgb(255, 213, 79)',
    'rgb(255, 202, 40)',
    'rgb(255, 193, 7)',
    'rgb(255, 160, 0)',
    'rgb(255, 143, 0)',
    'rgb(255, 111, 0)',
  ],
  [
    'rgb(215, 204, 200)',
    'rgb(188, 170, 164)',
    'rgb(141, 110, 99)',
    'rgb(121, 85, 72)',
    'rgb(109, 76, 65)',
    'rgb(78, 52, 46)',
    'rgb(62, 39, 35)',
  ],
])

const selectedColor = ref('rgb(245, 245, 245)')
const selectColor = (color) => {
  selectedColor.value = color
}
</script>

<template>
  <h1>Sélectionnez une couleur</h1>
  <main>
    <div>
      <div class="gradient" v-for="colors in colorsList" :key="colors[0]">
        <div
          class="sample"
          v-for="color in colors"
          :key="color"
          :style="{ backgroundColor: color }"
          @click="selectColor(color)"
          :class="{
            selected: color === selectedColor,
          }"
        ></div>
      </div>
    </div>
    <div>
      <p>{{ selectedColor }}</p>

      <div class="big-color" :style="{ backgroundColor: selectedColor }"></div>
    </div>
  </main>
</template>

<style scoped>
h1 {
  font-size: 40px;
  text-align: center;
  color: black;
  margin-bottom: 200px;
  margin-top: 100px;
}

main {
  /* border: 1px green solid; */
  display: flex;
  justify-content: center;
  gap: 150px;
}

.gradient {
  /* border: 1px red solid; */
  display: flex;
  /* gap: 10px; */
}

.sample {
  display: flex;
  margin: 5px;
  height: 25px;
  width: 25px;
  border-radius: 5px;
  cursor: pointer;
  /* border: 1px solid black; */
}
p {
  text-align: center;
  margin-bottom: 30px;
}
.big-color {
  border: 1px solid black;
  height: 180px;
  width: 180px;
  justify-self: center;
  align-self: center;
}

.gradient .selected {
  box-shadow: Opx Opx 10px black;
}
</style>
