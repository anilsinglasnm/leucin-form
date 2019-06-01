<template>
  <div class="swabRinse">
    <template v-if="residueType === 'Api' || residueType === 'CleaningAgent'">
      <label for="methodUsed">Method Used
          <input id="methodUsed"
                type="text"
                v-model="methodUsed" />
      </label>
      <div v-if="name === 'swab'"
           class="flexbox">
        <label for="solventName"
               class="halfWidth">Solvent Name
            <input id="solventName"
                  type="text"
                  v-model="solventName" />
        </label>
        <label for="solventQuantity"
               class="halfWidth">Solvent Quantity (ml)
            <input id="solventQuantity"
                  type="number"
                  v-model="solventQuantity" />
        </label>
      </div>
    </template>
    <div :class="{'flexbox': bioburdenOrEndotoxin}">
      <div class="star halfWidth"
           v-if="bioburdenOrEndotoxin">
        <div>Use recovery for Swab?</div>
        <label :for="`${name}yes`">
            <input :id="`${name}yes`"
                  :value="`${name}yes`"
                  :name="`${name}useRecovery`"
                  type="radio"
                  v-model="useRecovery" />Yes
        </label>
        <label :for="`${name}no`">
            <input :id="`${name}no`"
                  :value="`${name}no`"
                  :name="`${name}useRecovery`"
                  type="radio"
                  v-model="useRecovery" />No
        </label>
      </div>
      <label v-if="!hideDefaultRecovery"
            :class="{'halfWidth': bioburdenOrEndotoxin}"
            for="defaultRecovery">
        Default Recovery(%)
        <input id="defaultRecovery"
              type="number"
              v-model="defaultRecovery" />
      </label>
    </div>

    <button v-if="!addMoc"
            class="blue"
            @click="addMoc=true">
      Add MOC
    </button>
    <MocList v-else
             @showAddMocButton="addMoc=false" />

  </div>
</template>
<script>
export default {
  name: 'SwabRinse',
  data () {
    return {
      moc: false,
      methodUsed: '',
      solventName: '',
      solventQuantity: null,
      defaultRecovery: null,
      useRecovery: `${this.name}yes`,
      addMoc: false
    }
  },
  props: {
    name: {
      type: String
    },
    residueType: {
      type: String
    }
  },
  computed: {
    hideDefaultRecovery () {
      return this.bioburdenOrEndotoxin && this.useRecovery === 'no'
    },
    bioburdenOrEndotoxin () {
      return this.residueType === 'Bioburden' || this.residueType === 'Endotoxin'
    }
  },
  components: {
    MocList: () => import('../mocList/index.vue')
  }
}
</script>
<style scoped>
.swabRinse {
  border: 0.1rem solid black;
  padding: 0.5rem 1rem;
}
.star > div::before {
  content: '*';
  color: red;
}
.star > label {
  display: inline-block;
  margin: 0;
}
.star > label::before {
  content: '';
  color: red;
}
.star input {
  display: inline-block;
  width: 1.3rem;
}
.halfWidth {
  width: 48%;
  display: inline-block;
  margin: 0;
}
.flexbox {
  display: flex;
  justify-content: space-between;
}
.blue {
  color:skyblue;
  border-color:skyblue;
}
</style>
