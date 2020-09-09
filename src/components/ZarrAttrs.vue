
<template>
    <section>
        <b-collapse class="card" animation="slide" aria-id="contentIdForA11y3" :open="false">
            <div
                slot="trigger"
                slot-scope="props"
                class="card-header"
                role="button"
                aria-controls="contentIdForA11y3">
                <p class="card-header-title">
                    Attributes
                </p>
                <a class="card-header-icon">
                    <b-icon
                        :icon="props.open ? 'menu-down' : 'menu-up'">
                    </b-icon>
                </a>
            </div>
            <div class="card-content">
                <div class="content">
                  <dl class="zarr-attrs">
                    <template v-for="(value, name) in attrs">
                      <span v-bind:key="name">
                        <dt >{{ name }}</dt><dd>{{ value }}</dd>
                      </span>
                    </template>
                  </dl>
                </div>
            </div>
        </b-collapse>

    </section>
</template>

<script>
export default {
  name: 'ZarrAttrs',
  props: {
    attrs: Object
  }
}
</script>


<style scoped>

dl {
  width: 100%;
  overflow: hidden;
  padding: 0;
  margin: 0
}
dt {
  float: left;
  width: 50%;
  /* adjust the width; make sure the total of both is 100% */
  padding: 0;
  margin: 0
}
dd {
  float: left;
  width: 50%;
  /* adjust the width; make sure the total of both is 100% */
  padding: 0;
  margin: 0
}

</style>
