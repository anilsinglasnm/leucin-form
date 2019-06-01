<template>
  <div>
    <label for="methodId">Analytical Method Id
        <input id="methodId"
               type="text"
               v-model="methodId" />
    </label>
    <label for="residueType">Target Residue Type
      <select id="residueType"
              v-model="selectedResidueType">
        <option v-for="item in residueTypes"
                :key="item.id"
                :value="item.id">
          {{item.label}}
        </option>
      </select>
    </label>
    <component :is="selectedResidueType" />
    <Sampling v-if="selectedResidueType"
              :residueType="selectedResidueType" />
    <label for="reason">Reason
        <input id="reason"
               type="text"
               v-model="reason" />
    </label>

    <div class="flexbox">
      <button>Cancel</button>
      <button>Update</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AnalyticalMethodForm',
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
      methodId: '',
      selectedResidueType: '',
      reason: ''
    }
  },
  methods: {
    onSelect (id) {
      this.selectedResidueType = id
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
