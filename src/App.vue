<script setup>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { onMounted, ref } from "vue";

gsap.registerPlugin(ScrollTrigger);

const text = [
  "这个常伴你左右的好伙伴，超有能耐。",
  "体温感应功能，帮女性洞察自身的健康;",
  "车祸检测待命，紧急时刻主动呼叫救援;",
  "睡眠阶段跟测，让你更了解自己的睡眠状况;",
  "还有进阶的体能训练 app，为锻炼加分。",
  "就让一个更健康的未来，更漂亮地开始吧。",
];

const textRef = ref([]);
const textSpanActiveIndex = ref(0);

onMounted(() => {
  textRef.value.forEach((ele, index) => {
    ScrollTrigger.create({
      trigger: ele,
      start: "top, 60%",
      end: 'bottom, 60%',
      onEnter() {
        textSpanActiveIndex.value = index
      },
      onEnterBack() {
        textSpanActiveIndex.value = index
      }
    });
  })
});
</script>

<template>
  <main>
    <section></section>
    <section>
      <h1>
        <span
          v-for="(t, i) in text"
          :key="t"
          :ref="el => textRef.push(el)"
          :class="[i === textSpanActiveIndex && 'active']"
        >
          {{ t }}
        </span>
      </h1>
    </section>
    <section></section>
  </main>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  color: #ffffff;
}

body {
  background-color: #1d1d1f;
}

section {
  height: 100vh;
  max-width: 1300px;
  margin: 0 auto;
}

h1 {
  font-size: 56px;
}

span {
  opacity: 0.45;
  transition: opacity 0.2s ease;
}

span.active {
  opacity: 1;
}
</style>
