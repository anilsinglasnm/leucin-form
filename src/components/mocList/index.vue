<template>
  <div class="moclist">
    <div class="flexbox">
      <div class="star">Select MOC</div>
      <div class="star">Recovery (%)</div>
      <div>X</div>
    </div>
    <Moc v-for="(item, index) in mocsArr"
          :key="item.id"
          :selectedMocTypes="selectedMocTypes"
          @updateMocType="updateMocType(index, $event)"
          @updateRecovery="updateRecovery(index, $event)"
          @removeMoc="removeMoc(index)" />
    <div class="add" v-if="mocsArr.length !== mocTypesCount">
      <span @click="addNewMoc">Add another</span> or <span @click="addNewMoc">Create a new MOC</span>
    </div>
  </div>
</template>
<script>
export default {
  name: 'moc',
  data () {
    return {
      count: 1,
      mocsArr: [{id: 0, type: '', recovery: ''}],
      selectedMocTypes: {
        'Stainless Steel': 0,
        'Glass': 0,
        'Teflon': 0,
        'Plastic': 0
      },
      recovery: ''
    }
  },
  computed: {
    mocTypesCount () {
      return Object.keys(this.selectedMocTypes).length
    }
  },
  methods: {
    addNewMoc () {
      this.mocsArr.push({id: this.count++, type: '', recovery: ''})
    },
    removeMoc (index) {
      this.selectedMocTypes[this.mocsArr[index].type] = 0
      this.mocsArr.splice(index, 1)

      if (this.mocsArr.length === 0) {
        this.$emit('showAddMocButton')
      }
    },
    updateMocType (index, value) {
      this.selectedMocTypes[this.mocsArr[index].type] = 0
      this.selectedMocTypes[value] = 1
      this.mocsArr[index].type = value
    },
    updateRecovery (index, value) {
      this.mocsArr[index].recovery = value
    }
  },
  components: {
    Moc: () => import('../moc/index.vue')
  }
}
</script>
<style scoped>
.add span {
  color: skyblue;
}
.flexbox {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.star::before {
  content: '*';
  color: red;
}
.flexbox > div:nth-child(1) {
  width: 55%;
}
.flexbox > div:nth-child(2) {
  width: 30%;
}
.flexbox > div:nth-child(3) {
  opacity: 0;
}
.moclist {
  border: 1px solid grey;
  background: #f3f3f3;
  padding: 0.5rem;
  margin-top: 0.5rem;
}
</style>
