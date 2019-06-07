<template>
  <div class="bioburden">
    <label for="methodUsed">Method Used
        <input id="methodUsed"
               type="text"
               v-model="methodUsed"
               @input="updateData('Bioburden.methodUsed', methodUsed)" />
    </label>

    <div class="star">
      <div>Define TNTC and TFTC Limits?</div>
      <label for="yes">
          <input id="yes"
                value="yes"
                name="tntcTftcLimit"
                type="radio"
                v-model="tntcTftcLimit"
                @change="toggleTntcTftc" />Yes
      </label>
      <label for="no">
          <input id="no"
                value="no"
                name="tntcTftcLimit"
                type="radio"
                v-model="tntcTftcLimit"
                @change="toggleTntcTftc" />No
      </label>
    </div>
    <div class="tntcTftc"
         v-if="tntcTftcLimit === 'yes'">
      <label for="tntcLimit">TNTC Limit (in CFU)
          <input id="tntcLimit"
                type="number"
                v-model="tntcLimit"
                @input="updateData('Bioburden.tntcLimit', tntcLimit)" />
      </label>
      <label for="tftcLimit">TFTC Limit (in CFU)
          <input id="tftcLimit"
                type="number"
                v-model="tftcLimit"
                @input="updateData('Bioburden.tftcLimit', tftcLimit)" />
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Api',
  data () {
    return {
      methodUsed: '',
      tntcTftcLimit: 'yes',
      tntcLimit: null,
      tftcLimit: null
    }
  },
  props: {
    updateData: {
      type: Function
    }
  },
  methods: {
    toggleTntcTftc () {
      this.updateData('Bioburden.tntcTftcLimit', this.tntcTftcLimit)
      this.tntcLimit = null
      this.tftcLimit = null
    }
  }
}
</script>
<style scoped>
.star > div::before {
  content: '*';
  color: red;
}
.bioburden > div > label {
  display: inline-block;
  margin: 0.5rem 0;
}
.star > label::before {
  content: '';
  color: red;
}
.star input {
  display: inline-block;
  width: 1.3rem;
}
.tntcTftc {
  display: flex;
  justify-content: space-between;
}
.tntcTftc > label {
  width: 47%;
}
</style>
