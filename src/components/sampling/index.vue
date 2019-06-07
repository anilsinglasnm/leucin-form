<template>
  <div>
    <button :class="['blue', {'red': swab}]"
            @click="toggleSamplingForm('swab')">
      {{swab ? BUTTON_LABELS.SWAB.REMOVE : BUTTON_LABELS.SWAB.CONFIGURE}}
    </button>
    <SwabRinse v-if="swab"
               name="swab"
               :residueType="residueType"
               :updateData="updateData" />

    <button :class="['blue', {'red': rinse}]"
            @click="toggleSamplingForm('rinse')">
      {{rinse ? BUTTON_LABELS.RINSE.REMOVE : BUTTON_LABELS.RINSE.CONFIGURE}}
    </button>
    <SwabRinse v-if="rinse"
               name="rinse"
               :residueType="residueType"
               :updateData="updateData" />
  </div>
</template>

<script>
const BUTTON_LABELS = {
  SWAB: {
    CONFIGURE: 'Configure Swab Sampling Parameters',
    REMOVE: 'Remove Swab Sampling Parameters'
  },
  RINSE: {
    CONFIGURE: 'Configure Rinse Sampling Parameters',
    REMOVE: 'Remove Rinse Sampling Parameters'
  }
}
export default {
  name: 'Sampling',
  data () {
    return {
      BUTTON_LABELS,
      swab: false,
      rinse: false
    }
  },
  props: {
    residueType: {
      type: String
    },
    updateData: {
      type: Function
    }
  },
  methods: {
    toggleSamplingForm (type) {
      this[type] = !this[type]
    }
  },
  components: {
    SwabRinse: () => import('../swabRinse/index.vue')
  }
}
</script>
<style scoped>
.blue {
  color:skyblue;
  border-color:skyblue;
}
.red {
  color: red;
  border-color: red;
}
</style>
