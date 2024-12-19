<template>
  <div>
    <div class="inline-flex flex-col align-center border-solid rounded-lg divide-y-2 overflow-hidden">
      <PlateRow :size="7" v-for="i in 7" :key="i" />
    </div>
    <div class="flex flex-row mt-4 items-center space-x-1">
      <span>花瓶已使用: 
        <span class="text-red-500">{{ flowerUsedNum }}</span>
      </span>
      <button
        type="button"
        class="rounded-full bg-blue-500 text-white px-4 py-2 hover:bg-blue-600 text-sm"
        @click="applyFlowerBottle"
      >
        使用
      </button>
    </div>
    <div class="flex flex-row mt-4 items-center space-x-1">
      <ul>
        玻璃: 
        <li v-for="item in blindBoxNums">
          <span class="text-red-500">
            {{ item.level }}级: <b>{{ item.number }}</b> 
          </span>
          <button 
            v-if="item.level === 5"
            type="button" 
            class="rounded-full bg-blue-500 text-white px-4 py-2 hover:bg-blue-600 text-sm"
            @click="applyGlass"
          >
            使用
          </button>
        </li>
      </ul>
    </div>
    <div class="flex flex-row mt-4 items-center space-x-1">
      <ul>
        玩具: 
        <li v-for="item in toyNumbers">
          <span class="text-red-500">
            {{ item.level }}级: <b>{{ item.number }}</b> 
          </span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue';
import PlateRow from './components/PlateRow.vue';

const flowerUsedNum = ref(0);

const glassNum = ref(12);
const glassMaxLevel = 5;

const toyNum = ref(128 + 32);
const toyMaxLevel = 12;

const transformNumByNum = (num: number, maxLevel: number) => {
  const arr: Array<{
    level: number,
    number: number,
  }> = [];
  const numsStr = num.toString(2);

  for (let i = numsStr.length - 1; i >= Math.max(0, numsStr.length - maxLevel + 1); i--) {
    arr.push({
      level: numsStr.length - i,
      number: numsStr[i] === '0' ? 0 : 1,
    });
  }
  const maxLevelNum = glassNum.value >> (maxLevel - 1);

  if (maxLevelNum > 0) {
    arr.push({
      level: maxLevel,
      number: maxLevelNum,
    });
  }
  return arr.filter(item => item.number > 0);
  
}

const blindBoxNums = computed(() => {
  return transformNumByNum(glassNum.value, glassMaxLevel);
})

const toyNumbers = computed(() => {
  return transformNumByNum(toyNum.value, toyMaxLevel);
})

const applyGlass = () => {
  if (glassNum.value >= 16) {
    glassNum.value -= 16;
    toyNum.value += 8;
  }
}

const applyFlowerBottle = () => {
  flowerUsedNum.value += 1;
  glassNum.value += 7;
}
</script>