<template>
  <div class="custom-content-card content-card card">
    <div class="card-body pb-0">
    <div class="content-header h4 text-center pt-2 pb-3">Highlights</div>
      <div class="row">
        <wind-status :highlights="highlights"></wind-status>
      </div>
    </div>
  </div>
</template>

<script>

import WindStatus from "./WindStatus.vue"
export default {
  props: ["highlights"],
  components: {
    "wind-status": WindStatus,
  },
};
</script>