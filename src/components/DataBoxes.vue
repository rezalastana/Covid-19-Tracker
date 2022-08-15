<template>
  <div class="grid md:grid-cols-2 gap-4">
    <!-- Box 1 -->
    <div class="shadow-md bg-blue-200 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-800 font-bold mb-4">Kasus</h3>

      <div class="text-2xl mb-4">
        <span class="font-bold">Baru:</span>
        {{ numberWithComma(stats.NewConfirmed) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{ numberWithComma(stats.TotalConfirmed) }}
      </div>
    </div>

    <!-- Box 2 -->
    <div class="shadow-md bg-blue-400 p-10 text-center rounded">
      <h3 class="text-3xl text-white font-bold mb-4">Kematian</h3>

      <div class="text-2xl mb-4">
        <span class="font-bold">Baru:</span>
        {{ numberWithComma(stats.NewDeaths) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{ numberWithComma(stats.TotalDeaths) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DataBoxes",
  props: ["stats"],
  methods: {
    numberWithComma(x) {
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
  },
};
</script>
