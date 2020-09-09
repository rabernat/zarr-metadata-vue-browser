<template>
  <section class="section">
    <div class="container">
      <b-field>
          <b-input placeholder="Zarr Group URL" type="url" v-model="inputUrl"></b-input>
      </b-field>
      <b-button @click="loadGroup">Go</b-button>
      <div v-if="clicked">
        <zarr-group v-bind:url="targetUrl"></zarr-group>
      </div>
    </div>
  </section>
</template>

<script>
import ZarrGroup from './ZarrGroup.vue'

export default {
  name: 'ZarrViewer',
  data () {
    return {
      inputUrl: null,
      clicked: false
    }
  },
  computed: {
    targetUrl: function() {
      return this.inputUrl
    }
  },
  components: {'zarr-group': ZarrGroup},
  methods: {
    loadGroup() {
      this.clicked = true
    }
  }
}
</script>
