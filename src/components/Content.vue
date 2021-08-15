<template>
  <div style="position: relative;">
      <today-highlights :highlights="highlights"></today-highlights>
      <embed-frame :embedFrame="embedFrame"></embed-frame>
  </div>
</template>

<script>
import Highlights from './Highlights.vue';
import EmbedFrame from './EmbedFrame.vue';
export default {
  props: ['highlights', 'embedFrame'],
  components: {
    'embed-frame': EmbedFrame,
    'today-highlights': Highlights
  },
}
</script>