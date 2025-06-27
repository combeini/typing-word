<script setup lang="ts">
import { computed, ref, watch } from 'vue';

interface Props {
  currentKey?: string;
}

const props = withDefaults(defineProps<Props>(), {
  currentKey: ''
});

const keyboardLayout = [
  ['q', 'w', 'e', 'r', 't', 'y', 'u', 'i', 'o', 'p'],
  ['a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l'],
  ['z', 'x', 'c', 'v', 'b', 'n', 'm']
];

const currentKeyLower = computed(() => props.currentKey.toLowerCase());

// 判断当前键是否需要高亮
const isKeyHighlighted = (key: string) => {
  return key === currentKeyLower.value;
};
</script>

<template>
  <div class="keyboard-hint">
    <div class="keyboard">
      <div v-for="(row, rowIndex) in keyboardLayout" :key="rowIndex" class="keyboard-row">
        <div 
          v-for="(key, keyIndex) in row" 
          :key="keyIndex" 
          class="key" 
          :class="{ 'key-highlight': isKeyHighlighted(key) }"
        >
          {{ key }}
        </div>
      </div>
      <div class="keyboard-row">
        <div class="key key-space" :class="{ 'key-highlight': currentKeyLower.value === ' ' }">空格</div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.keyboard-hint {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 10rem;
  
  .keyboard {
    display: flex;
    flex-direction: column;
    gap: 6rem;
    
    .keyboard-row {
      display: flex;
      justify-content: center;
      gap: 6rem;
      
      .key {
        width: 40rem;
        height: 40rem;
        display: flex;
        align-items: center;
        justify-content: center;
        background-color: rgba(30, 100, 200, 0.2); // 蓝色背景，增加对比度
        border-radius: 6rem;
        font-size: 16rem;
        color: #ffffff; // 白色文字，增加对比度
        text-transform: uppercase;
        user-select: none;
        transition: all 0.2s;
        border: 1px solid rgba(100, 150, 255, 0.3); // 蓝色边框
        
        &.key-highlight {
          background-color: rgba(50, 120, 255, 0.8); // 高亮时更亮的蓝色
          color: white;
          transform: translateY(-3rem);
          box-shadow: 0 3rem 6rem rgba(0, 100, 255, 0.4);
          border-color: rgba(100, 150, 255, 0.8);
          font-weight: bold;
        }
        
        &.key-space {
          width: 200rem;
        }
      }
    }
  }
}
</style>