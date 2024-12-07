<template lang="pug">
q-page.row.items-center.justify-evenly
  // q-img(src="../assets/ja_roman.jpg")

  table
    tr
      th.flex.flex-rwd
        div 平
        div 假
        div 名
      th(v-for="p in phonics_a", :key="p") {{ p }}
    tr
      td a
      td(v-for="(p, idx) in phonics_as" :key="p")
        q-btn(round, size="lg", @click="play(p, phonics_a, '', idx)",
         :label="getLabel(phonics_a, p, '', idx)")
    tr
      td ka
      td(v-for="(p, idx) in phonics_ks" :key="p")
        q-btn(round, size="lg", @click="play(p, phonics_a, 'k', idx)",
         :label="getLabel(phonics_a, p, 'k', idx)")
    tr
      td sa
      td(v-for="(p, idx) in phonics_ss" :key="p")
        q-btn(round, size="lg", @click="play(p, phonics_a, 's', idx)",
         :label="getLabel(phonics_a, p, 's', idx)")
    tr
      td ta
      td(v-for="(p, idx) in phonics_ts" :key="p")
        q-btn(round, size="lg", @click="play(p, phonics_a, 't', idx)",
         :label="getLabel(phonics_a, p, 't', idx)")
    tr
      td na
      td(v-for="(p, idx) in phonics_ns" :key="p")
        q-btn(round, size="lg", @click="play(p, phonics_a, 'n', idx)",
         :label="getLabel(phonics_a, p, 'n', idx)")
    tr
      td ha
      td(v-for="(p, idx) in phonics_hs" :key="p")
        q-btn(round, size="lg", @click="play(p, phonics_a, 'h', idx)",
         :label="getLabel(phonics_a, p, 'h', idx)")
    tr
      td ma
      td(v-for="(p, idx) in phonics_ms" :key="p")
        q-btn(round, size="lg", @click="play(p, phonics_a, 'm', idx)",
         :label="getLabel(phonics_a, p, 'm', idx)")
    tr
      td ya
      td(v-for="(p, idx) in phonics_ys" :key="idx")
        q-btn(v-if="p", round, size="lg", @click="play(p, phonics_a, 'y', idx)",
         :label="getLabel(phonics_a, p, 'y', idx)")
      td
      td
    tr
      td ra
      td(v-for="(p, idx) in phonics_ls" :key="p")
        q-btn(round, size="lg", @click="play(p, phonics_a, 'l', idx)",
         :label="getLabel(phonics_a, p, 'l', idx)")
    tr
      td wa
      td(v-for="(p, idx) in phonics_ws" :key="idx")
        q-btn(v-if="p", round, size="lg", @click="play(p, phonics_a, 'w', idx)",
         :label="getLabel(phonics_a, p, 'w', idx)")
      td
      td
      td



</template>

<script lang="ts">
import ExampleComponent from 'components/ExampleComponent.vue';
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'IndexPage',
  props: [
    'phonics_a',
    'phonics_song',
    'phonics_as',
    'phonics_ks',
    'phonics_ss',
    'phonics_ts',
    'phonics_ns',
    'phonics_hs',
    'phonics_ms',
    'phonics_ys',
    'phonics_ls',
    'phonics_ws',
  ],
  components: { ExampleComponent },
  setup() {
    return {
      count: ref(1),
      currentRoman: ref(null),
      currentPhonics: ref(null),
      useRoman: ref(new Array(5).fill(false)),
    };
  },
  methods: {
    getPhonics(hiragana: string) {
      return hiragana;
    },
    getLabel(phonics_a: [string], hiragana: string, head: string, idx: number) {
      if (this.currentPhonics !== hiragana) {
        return this.getPhonics(hiragana);
      } else {
        let tail = phonics_a[idx];
        if (head === 's' && tail === 'i') {
          head = 'sh';
        } else if (head === 't' && tail === 'i') {
          head = 'ch';
        } else if (head === 't' && tail === 'u') {
          head = 'ts';
        }
        return head + tail;
      }
    },
    play(hiragana: string, phonics: string, p: string, idx: number) {
      this.currentPhonics = hiragana;

      const utterance = new SpeechSynthesisUtterance(hiragana);
      utterance.lang = 'ja-JP';
      utterance.rate = 0.8;

      window.speechSynthesis.speak(utterance);
    },
  },
});
</script>
