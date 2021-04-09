<template>
  <div :key="jam.id" v-for="jam in jams">
    <Jam
      @delete-jam="$emit('delete-jam', jam.id)"
      :jam="jam"
    />
  </div>
</template>

<script>
import Jam from './Jam'

export default {
  name: 'Jams',
  props: {
    jams: Array,
  },
  components: {
    Jam,
  },
  emits: ['delete-task'],
}
</script>
