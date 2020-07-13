<template>
  <q-page padding class="row justify-evenly">
    <div class="full-height full-width">
      Detected barcodes:
      <div v-for="(id, i) in detecteds" :key="i">
        {{ id }}
      </div>
      <v-quagga :onDetected="logIt" :readerSize="readerSize"></v-quagga>
    </div>
  </q-page>
</template>

<script lang="ts">
import Vue from 'vue';
import VueQuagga from 'vue-quaggajs';

Vue.use(VueQuagga);

interface quaggaRes {
  codeResult: {
    code: string;
  };
}

export default Vue.extend({
  name: 'PageIndex',
  data() {
    return {
      readerSize: {
        width: 1280,
        height: 700,
      },
      detecteds: [''],
    };
  },
  methods: {
    logIt(data: quaggaRes) {
      this.detecteds.push(data.codeResult.code);
    },
  },
});
</script>

<style>
video,
canvas {
  max-width: 100% !important;
  width: 100% !important;
}
</style>
