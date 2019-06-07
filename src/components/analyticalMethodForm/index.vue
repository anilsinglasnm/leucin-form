<template>
  <div>
    <label for="methodId">Analytical Method Id
        <input id="methodId"
               type="text"
               v-model="sampleData.methodId" />
    </label>
    <label for="residueType">Target Residue Type
      <select id="residueType"
              v-model="sampleData.selectedResidueType"
              @change="clear(sampleData.selectedResidueType)">
        <option v-for="item in residueTypes"
                :key="item.id"
                :value="item.id">
          {{item.label}}
        </option>
      </select>
    </label>
    <component :is="sampleData.selectedResidueType"
               :updateData="updateData" />
    <Sampling v-if="sampleData.selectedResidueType"
              :residueType="sampleData.selectedResidueType" />
    <label for="reason">Reason
        <input id="reason"
               type="text"
               v-model="sampleData.reason" />
    </label>

    <div class="flexbox">
      <button @click="clear">Cancel</button>
      <button @click="submit">Update</button>
    </div>
  </div>
</template>

<script>
const FIELDS_MAP = {
  methodId: 'Method Id',
  selectedResidueType: 'Target Residue Type',
  reason: 'Reason',
  lod: 'LOD',
  loq: 'LOQ',
  methodUsed: 'Method Used',
  tntcTftcLimit: 'TNT',
  tntcLimit: 'TNTC Limit',
  tftcLimit: 'TFTC Limit'
}

const REPLICA_MAPPING = {
  'Api': 'Api',
  'CleaningAgent': 'Api',
  'Bioburden': 'Bioburden',
  'Endotoxin': 'Bioburden'
}

const SAMPLE_DATA = {
  methodId: '',
  selectedResidueType: '',
  reason: '',
  Api: {
    lod: '',
    loq: '',
    swab: {
      methodUsed: '',
      solventName: '',
      solventQuantity: '',
      defaultRecovery: '',
      mocs: []
    },
    rinse: {
      methodUsed: '',
      defaultRecovery: '',
      mocs: []
    }
  },
  Bioburden: {
    methodUsed: '',
    tntcTftcLimit: 'yes',
    tntcLimit: '',
    tftcLimit: '',
    swab: {
      useRecovery: 'swabyes',
      defaultRecovery: '',
      mocs: []
    },
    rinse: {
      solventVolume: '',
      useRecovery: 'rinseyes',
      defaultRecovery: '',
      mocs: []
    }
  }
}

export default {
  name: 'AnalyticalMethodForm',
  created () {
    this.clear()
  },
  data () {
    return {
      residueTypes: [
        {
          id: '',
          label: 'Select'
        },
        {
          id: 'Api',
          label: 'API'
        },
        {
          id: 'CleaningAgent',
          label: 'Cleaning Agent'
        },
        {
          id: 'Bioburden',
          label: 'Bioburden'
        },
        {
          id: 'Endotoxin',
          label: 'Endotoxin'
        }
      ],
      sampleData: null
    }
  },
  methods: {
    updateData (key, value) {
      const residueReplica = REPLICA_MAPPING[this.sampleData.selectedResidueType]
      const splittedKey = key.split('.')
      if (splittedKey.length === 3) {
        this.sampleData[splittedKey[0]][splittedKey[1]][splittedKey[2]] = value
      } else if (splittedKey.length === 2) {
        this.sampleData[splittedKey[0]][splittedKey[1]] = value
      } else {
        this.sampleData[key] = value
      }

      if (key === 'Bioburden.tntcTftcLimit') {
        if (value === 'no') {
          this.sampleData[residueReplica].tntcLimit = 0
          this.sampleData[residueReplica].tftcLimit = 0
        } else {
          this.sampleData[residueReplica].tntcLimit = ''
          this.sampleData[residueReplica].tftcLimit = ''
        }
      }
    },
    clear (residueType) {
      if (!residueType) {
        this.sampleData = { ...SAMPLE_DATA }
      }
      this.sampleData.Api = { ...SAMPLE_DATA.Api }
      this.sampleData.Api.swab = { ...SAMPLE_DATA.Api.swab }
      this.sampleData.Api.rinse = { ...SAMPLE_DATA.Api.rinse }
      this.sampleData.Bioburden = { ...SAMPLE_DATA.Bioburden }
      this.sampleData.Bioburden.swab = { ...SAMPLE_DATA.Bioburden.swab }
      this.sampleData.Bioburden.rinse = { ...SAMPLE_DATA.Bioburden.rinse }
    },
    submit () {
      const emptyKeys = []
      const residueReplica = REPLICA_MAPPING[this.sampleData.selectedResidueType]
      getErrorString(this.sampleData)
      if (residueReplica) {
        getErrorString(this.sampleData[residueReplica])
      }

      function getErrorString (obj) {
        Object.keys(obj).forEach(key => {
          if (!obj[key] && obj[key] !== 0) {
            emptyKeys.push(FIELDS_MAP[key] || key)
          }
        })
      }

      if (emptyKeys.length) {
        alert(`${emptyKeys.join(',')} should be filled before submitting`)
      } else {
        alert('Form Submitted successfully')
        this.clear()
      }
    }
  },
  components: {
    Api: () => import('../methods/api/index.vue'),
    CleaningAgent: () => import('../methods/api/index.vue'),
    Bioburden: () => import('../methods/bioburden/index.vue'),
    Endotoxin: () => import('../methods/bioburden/index.vue'),
    Sampling: () => import('../sampling/index.vue')
  }
}
</script>

<style scoped>
.flexbox {
  display: flex;
  justify-content: space-between;
}
.flexbox > button {
  width: 40%;
}
</style>
