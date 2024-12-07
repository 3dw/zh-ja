<template lang="pug">
q-layout(view="lHh Lpr lFf")
  q-header(elevated)
    q-toolbar
      q-btn(flat, dense, round, icon="menu", aria-label="Menu", @click="toggleLeftDrawer")
      q-toolbar-title 自主學日文
      div
        a(href="https://github.com/3dw/zh-ja/", target="_blank", rel="noopener noreferrer")
          q-icon(name="palette")
          span.thin-only 開放的教材教法 -
          span 共筆研發中
  q-drawer(v-model="leftDrawerOpen", show-if-above, bordered)
    q-list
      q-item-label(header) 學習資源
  q-page-container
    router-view(:phonics_a="phonics_a", :phonics_song="phonics_song",
      :phonics_as="phonics_as", :phonics_ks="phonics_ks", :phonics_ss="phonics_ss",
      :phonics_ts="phonics_ts", :phonics_ns="phonics_ns", :phonics_hs="phonics_hs",
      :phonics_ms="phonics_ms", :phonics_ys="phonics_ys", :phonics_ls="phonics_ls",
      :phonics_ws="phonics_ws")

</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'MainLayout',

  components: {},

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
      phonics_a: ref(['a', 'i', 'u', 'e', 'o']),
      phonics_song: ref([
        'A',
        'ka',
        'sa',
        'ta',
        'na',
        'ha',
        'ma',
        'ya',
        'ra',
        'wa',
      ]),
      phonics_as: ref(['あ', 'い', 'う', 'え', 'お']),
      phonics_ks: ref(['か', 'き', 'く', 'け', 'こ']),
      phonics_ss: ref(['さ', 'し', 'す', 'せ', 'そ']),
      phonics_ts: ref(['た', 'ち', 'つ', 'て', 'と']),
      phonics_ns: ref(['な', 'に', 'ぬ', 'ね', 'の']),
      phonics_hs: ref(['は', 'ひ', 'ふ', 'へ', 'ほ']),
      phonics_ms: ref(['ま', 'み', 'む', 'め', 'も']),
      phonics_ys: ref(['や', '', 'ゆ', '', 'よ']),
      phonics_ls: ref(['ら', 'り', 'る', 'れ', 'ろ']),
      phonics_ws: ref(['わ', '', 'ん', '', 'を']),
    };
  },
});
</script>
