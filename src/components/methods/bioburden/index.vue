<template>
  <div class="bioburden">
    <label for="methodUsed">Method Used
        <input id="methodUsed"
               type="text"
               v-model="methodUsed" />
    </label>

    <div class="star">
      <div>Define TNTC and TFTC Limits?</div>
      <label for="yes">
          <input id="yes"
                value="yes"
                name="tntcTftcLimit"
                type="radio"
                v-model="tntcTftcLimit" />Yes
      </label>
      <label for="no">
          <input id="no"
                value="no"
                name="tntcTftcLimit"
                type="radio"
                v-model="tntcTftcLimit" />No
      </label>
    </div>
    <div class="tntcTftc"
         v-if="tntcTftcLimit === 'yes'">
      <label for="tntcLimit">TNTC Limit (in CFU)
          <input id="tntcLimit"
                type="number"
                v-model="tntcLimit" />
      </label>
      <label for="tftcLimit">TFTC Limit (in CFU)
          <input id="tftcLimit"
                type="number"
                v-model="tftcLimit" />
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
