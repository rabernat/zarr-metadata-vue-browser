<template>
  <div class="box">
    <h2 class="title is-2">{{ name }}</h2>
    <div class="tags has-addons">
      <span class="tag">dtype</span>
      <span class="tag is-primary">{{ dtype }}</span>
    </div>
    <div v-if="shape.length > 0">
      <table class="table">
        <thead>
          <tr>
            <td>axis</td><th v-for="n in shape.length" :key="n">{{ n }}</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <th>shape</th><td v-for="s in shape">{{ s }}</td>
          </tr>
          <tr>
            <th>chunks</th><td v-for="c in chunks">{{ c }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div v-else>
      <span class="tag is-primary">singleton</span>
    </div>
    <zarr-attrs v-bind:attrs="attrs"></zarr-attrs>
  </div>
</template>

<script>
import ZarrAttrs from './ZarrAttrs.vue'

export default {
  name: 'ZarrAttrs',
  props: ['name', 'shape', 'chunks', 'dtype', 'attrs'],
  components: {'zarr-attrs': ZarrAttrs}
}
</script>
