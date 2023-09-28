<template lang="pug">
q-page.row.items-center.justify-evenly
  // q-img(src="../assets/ja_roman.jpg")
  
  table
    tr
      th 平假名
      th(v-for="p in phonics_a", :key="p") {{ p }}
    tr
      td a
      td(v-for="(p, idx) in phonics_as" :key="p")
        q-btn(@click="play(p, phonics_a, '', idx)", :label="getLabel(phonics_a, p, '', idx)")
    tr
      td ka
      td(v-for="(p, idx) in phonics_ks" :key="p")
        q-btn(@click="play(p, phonics_a, 'k', idx)", :label="getLabel(phonics_a, p, 'k', idx)")

</template>

<script lang="ts">
import ExampleComponent from 'components/ExampleComponent.vue';
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'IndexPage',
  props: ['phonics_a', 'phonics_song', 'phonics_as', 'phonics_ks'],
  components: { ExampleComponent },
  setup () {
    return {
      count: ref(1),
      currentRoman: ref(null),
      currentPhonics: ref(null),
      useRoman: ref(new Array(5).fill(false))
    };
  },
  methods: {
    getPhonics (hiragana: string) {
      return hiragana
    },
    getLabel (phonics_a:[string], hiragana: string, head: string, idx: number) {
      console.log(hiragana)
      if (this.currentPhonics !== hiragana) {
        return this.getPhonics(hiragana)
      } else {
        let tail = phonics_a[idx]
        console.log(tail)
        return head + tail
      }
    },
    play (hiragana:string,  phonics: string, p:string, idx: number) {
      const isOpera = (!!window.opr && !!opr.addons) || !!window.opera || navigator.userAgent.indexOf(' OPR/') >= 0;
      const isSafari = /constructor/i.test(window.HTMLElement) || (function (p) { return p.toString() === '[object SafariRemoteNotification]'; })(!window['safari'] || (typeof safari !== 'undefined' && window['safari'].pushNotification));

      this.currentPhonics = hiragana

      console.log(`playing: ${p}${phonics[idx]}`)
      if (isOpera || isSafari) {
        const audio = new Audio(`/phonics/${p}${phonics[idx]}.ogg`);
        audio.play();
      } else {
        const audio = new Audio(`/phonics/${p}${phonics[idx]}.mp3`);
        audio.play();
      }
    }
  }
});
</script>
