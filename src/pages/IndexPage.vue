<template lang="pug">
q-page.row.items-center.justify-evenly
  q-img(src="../assets/ja_roman.jpg")
</template>

<script lang="ts">
import ExampleComponent from 'components/ExampleComponent.vue';
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'IndexPage',
  components: { ExampleComponent },
  setup () {
    return {
      count: ref(1)
    };
  }
});
</script>
