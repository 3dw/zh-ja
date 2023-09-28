<template lang="pug">
q-page.row.items-center.justify-evenly
  q-img(src="../assets/ja_roman.jpg")
  
  table
    tr
      td(v-for="phonics in phonics_a", :key="phonics")
    tr
      td(v-for="(p, idx) in phonics_as" :key="phonics_a")
        q-btn(@click="play(phonics_a, p, idx)", :label="getRoman(p, '')")


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
      count: ref(1)
    };
  },
  methods: {
    getRoman (phonics: string, head: string) {
      return head + phonics
    },
    play (phonics: string, p:string, idx: number) {
      const isOpera = (!!window.opr && !!opr.addons) || !!window.opera || navigator.userAgent.indexOf(' OPR/') >= 0;
      const isSafari = /constructor/i.test(window.HTMLElement) || (function (p) { return p.toString() === "[object SafariRemoteNotification]"; })(!window['safari'] || (typeof safari !== 'undefined' && window['safari'].pushNotification));

      console.log('playing:' + p)
      if (isOpera || isSafari) {
        const audio = new Audio(`/phonics/${phonics[idx]}.ogg`);
      } else {
        const audio = new Audio(`/phonics/${phonics[idx]}.mp3`);
      }
      audio.play();
    }
  }
});
</script>
