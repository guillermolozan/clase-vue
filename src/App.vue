<template lang="pug">
  main
    px-header(:links="links")
    router-view(class="container px-5 py-10 flex justify-center")
</template>

<script>

import PxHeader from "@/components/PxHeader";

export default {
  name: "App",
  components: {
    PxHeader
  },
  data (){
    return {
      links: [
        {
          title: 'BTC',
          to: { name: 'coin-detail', params: { id: 'bitcoin' } }
        },
        {
          title: 'ETH',
          to: { name: 'coin-detail', params: { id: 'ethereum' } }
        },
        {
          title: 'XRP',
          to: { name: 'coin-detail', params: { id: 'ripple' } }
        }
      ]
    }
  }
};

</script>