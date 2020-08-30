<template>
  <div class="flex-col">
    <div class="flex justify-center">
      <moon-loader :loading="isLoading" :color="'#0000ff'" :size="100"></moon-loader>
    </div>
    <px-assets-table v-if="!isLoading" :assets="assets" />
  </div>
</template>

<script>
import api from '@/api'
import PxAssetsTable from '../components/PxAssetsTable'

export default {
  name: 'Home',

  components: { PxAssetsTable },

  data() {
    return { assets: [], isLoading: true }
  },

  async created() {
    try {
      this.isLoading = true
      const assets = await api.getAssets()
      this.assets = assets
      this.isLoading = false
    } catch (e) {
      this.isLoading = false
    }
  }
}
</script>
