<template>
  <div v-if="url">
    <div v-if="loading">Loading...</div>
    <div v-else>
      <p>Url: {{ url }}</p>
      <div v-for="array in group.arrays" v-bind:key="array.name">
        <zarr-array v-bind="array"></zarr-array>
      </div>
      <h3 class="title is-3">Group Level Metadata</h3>
      <zarr-attrs v-bind:attrs="group.attrs"></zarr-attrs>
    </div>
  </div>
  <div v-else>Please enter a URL</div>
</template>


<script>
import ZarrArray from './ZarrArray.vue'
import ZarrAttrs from './ZarrAttrs.vue'

const axios = require('axios').default;

function parseMeta(meta) {
  if (!('.zgroup' in meta)) {
    throw "Group doesn't contain the '.zgroup' key."
  }

  let group = {}
  group['zarr_format'] = meta['.zgroup'].zarr_format
  group['attrs'] = meta['.zattrs']

  let arrays = {}
  for (const prop in meta) {
    if (prop.endsWith('/.zarray')) {
      let attrs = meta[prop.replace('.zarray', '.zattrs')]
      let name = prop.split('/.zarray')[0]
      let array = {
        name: name,
        shape: meta[prop].shape,
        chunks: meta[prop].chunks,
        dtype: meta[prop].dtype,
        attrs: attrs
      }
      arrays[name] = array
    }
  }
  group['arrays'] = arrays
  return group
}

export default {
  name: 'ZarrGroup',
  data () {
    return {
      info: null,
      loading: true,
      errored: false,
      group: {}
    }
  },
  props: {
    url: String,
  },
  components: {
    'zarr-array': ZarrArray,
    'zarr-attrs': ZarrAttrs,
  },
  mounted () {
    axios
      .get(this.url)
      .then(response => (this.group = parseMeta(response.data.metadata)))
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
  }
}
</script>
