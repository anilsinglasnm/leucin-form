<template>
  <div class="apiMethod">
    <label for="lod">LOD (in ppm)
        <input id="lod"
               type="number"
               v-model="lod"
               @input="updateData('Api.lod', lod)" />
    </label>
    <label for="loq">LOQ (in ppm)
        <input id="loq"
               type="number"
               v-model="loq"
               @input="updateData('Api.loq', loq)" />
    </label>
  </div>
</template>

<script>
export default {
  name: 'Api',
  data () {
    return {
      lod: null,
      loq: null
    }
  },
  props: {
    updateData: {
      type: Function
    }
  }
}
</script>
<style scoped>
.apiMethod {
  display: flex;
  justify-content: space-between;
}
.apiMethod > label {
  width: 47%;
}
</style>
