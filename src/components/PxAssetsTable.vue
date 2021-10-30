<template lang="pug">
table
  thead
    tr(class="bg-gray-600 border-b-2 border-gray-400 text-white")
      th 
      th(:class="{up:this.sortOrder==1,down:this.sortOrder==-1}")
        span(
          class="underline cursor-pointer"
          @click="changeSortOrder"
        ) Ranking
      th Nombre
      th Precio
      th Cap. de Mercado
      th Variación 24hs
      th
        input(
          class="text-black"
          type="text",
          v-model="filter")
      td.hidden(class='sm:block')
  tbody
    tr(
      v-for="a in filteredAssets",
      :key="a.id",
      class="border-b border-gray-200 hover:bg-gray-100 ")
      td: img(
            class="w-6 h-6"
            :src="`https://static.coincap.io/assets/icons/${a.symbol.toLowerCase()}@2x.png`",
            :alt="a.name")
      td: b # {{ a.rank }}
      td {{ a.name }}
      td {{ a.priceUsd | dollar }}
      td {{ a.marketCapUsd | dollar }}
      td(:class=" a.changePercent24Hr.includes('-') ? 'text-red-600 up' : 'text-green-600 down'") {{ a.changePercent24Hr | percent }}
      td 
        px-button(
          @custom-click="gotoCoin(a.id)"
          ) DETALLE
        //- router-link(
        //-   class="bg-transparent hover:bg-green-500 text-green-700 font-semibold hover:text-white py-2 px-2 border border-green-500 hover:border-transparent rounded",
        //-   :to="{ name:'coin-detail', params:{id:a.id} }"
        //-   ) DETALLE
      td.hidden(class='sm:block')
</template>

<script>
import PxButton from '@/components/PxButton'
export default {
  name: "PxAssetsTable",
  data(){
    return {
      filter:'',
      sortOrder:1
    }
  },  
  components:{ PxButton },
  props: {
    assets: {
      type: Array,
      default: () => []
    }
  },
  computed:{
    filteredAssets(){
      
      //- if(!this.filter){
      //-   return this.assets
      //- }

      const altOrder = this.sortOrder == 1 ? -1 : 1;

      return this.assets
        .filter(
          a =>
            a.symbol.toLowerCase().includes(this.filter.toLowerCase()) ||
            a.name.toLowerCase().includes(this.filter.toLowerCase())
        )
        .sort((a,b)=>{
          if ( parseInt(a.rank) > parseInt(b.rank) ){
            return this.sortOrder
          }
          return altOrder
        })

    }
  },
  methods:{
    changeSortOrder(){
      this.sortOrder= this.sortOrder==1 ? -1 : 1
    },
    gotoCoin(id){
      this.$router.push({name:"coin-detail",params:{id:id}})
    }
  }
};
</script>

<style scoped>

.up::before {
  content: "👆";
}

.down::before {
  content: "👇";
}

td {
  padding: 20px 0px;
  font-size: 0.6rem;
  text-align: center;
}

th {
  padding: 5px;
  font-size: 0.6rem;
}

@media (min-width: 640px) {
  td,
  th {
    padding: 20px;
    font-size: 1rem;
  }

  th {
    padding: 12px;
  }
}
</style>
