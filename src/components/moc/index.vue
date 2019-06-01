<template>
  <div class="moc">
    <select v-model="selectedMocType"
            @change="$emit('updateMocType', selectedMocType)">
      <option v-for="(type, index) in mocTypes"
              :key="index"
              :value="type">
        {{type}}
      </option>
    </select>
    <input type="text"
          v-model="recovery"
          @input="$emit('updateRecovery', recovery)" />
    <div @click="$emit('removeMoc')">
      X
    </div>
  </div>
</template>
<script>
export default {
  name: 'moc',
  data () {
    return {
      mocTypes: ['Stainless Steel', 'Glass', 'Teflon', 'Plastic'],
      selectedMocType: '',
      recovery: ''
    }
  }
}
</script>
<style scoped>
.moc {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0.2rem;
}

.moc > select {
  width: 55%;
}
.moc > input {
  width: 30%;
  box-sizing: border-box;
}
</style>
