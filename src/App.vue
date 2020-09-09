<template>
  <div id="app">
    <section class="hero is-primary">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
            Zarr Viewer
          </h1>
        </div>
      </div>
    </section>
    <section>
      <zarr-viewer />
    </section>
  </div>
</template>

<script>

import ZarrViewer from './components/ZarrViewer.vue'

export default {
  name: 'App',
  components: {
    'zarr-viewer': ZarrViewer
  }
}
</script>

<style>
</style>
