<template>
  <div class="highlights-item col-md-12 col-sm-12 col-xs-12 border-top">
    <div>
    <div class="card-heading pt-5">Wind Status</div>
    <div class="row pt-4 mt-4">
      <div class="col-sm-4 col-md-4 mt-2">
        <p class="card-sub-heading mt-3">Wind Direction</p>
        <p class="mt-4"><img src="../assets/wind-direction.svg" height="40" width="40"/></p>
        <p class="card-value mt-4">{{ highlights.windStatus.windDegrees }} °</p>
      </div>
      <div class="col-sm-4 col-md-4 mt-2 text-center align-middle">
        <p class="card-sub-heading mt-3">Wind Gust</p>
        <p class="mt-4"><img src="../assets/winddirection.svg" height="40" width="40"></p>
        <p class="card-value mt-4">{{ highlights.windStatus.gust }}</p>
      </div>
      <div class="col-sm-4 col-md-4 mt-2">
        <p class="card-sub-heading mt-3">Wind Speed</p>
        <p class="mt-4"><img src="../assets/windspeed.svg" height="40" width="40"></p>
        <p class="card-value mt-4">{{ highlights.windStatus.windSpeed }} km/h</p>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["highlights"],
  components: {},
  data() {
    return {};
  },
  methods: {},
  computed: {}
};
</script>