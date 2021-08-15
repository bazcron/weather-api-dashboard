<template>
  <div class="custom-card header-card card">
    <div class="card-body pt-0">
      <div class="content-header h4 text-center pt-2 pb-3">Map</div>
      <div class="row">
        <div class="mapouter"><div class="gmap_canvas"><iframe width="1360" height="430" id="gmap_canvas" :src="embedFrame.src" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" style="margin-left: 1em"></iframe></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['embedFrame']
}
</script>