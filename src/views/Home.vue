<template lang="pug">
  div
    bounce-loader(
      :loading="isLoading",
      :color="bounceColor",
      :size="100")
    px-assets-table(
      v-if="!isLoading"
      :assets="assets")
</template>

<script>
import api from '@/api'
import PxAssetsTable from '@/components/PxAssetsTable'

export default {
  name: 'Home',

  components: { PxAssetsTable },

  data() {
    return {
      assets: [],
      isLoading:false,
      bounceColor:"#68d391"
    }
  },

  created() {
    this.isLoading=true;
    api.getAssets()
    .then(assets => (this.assets = assets))
    .catch(error => console.error('Error :', error))
    .finally(()=> ( this.isLoading=false ) )
  } 
}
</script>
