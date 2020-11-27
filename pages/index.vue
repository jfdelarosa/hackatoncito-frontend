<template>
  <div class="container">
    <div class="block">
      <input
        type="text"
        class="input"
        v-model="search"
        @keydown.enter.stop="doSearch"
        placeholder="Buscar noticia o tema"
      />
    </div>
    <div class="trends">
      <div class="tred-title">Trends:</div>
      <ul>
        <li
          v-for="(trend, index) in trends"
          :key="index"
          @click="doTrend(index)"
        >
          - {{ trend }}
        </li>
      </ul>
    </div>
    <noticia v-for="(item, index) in data" :item="item" :key="index"></noticia>
  </div>
</template>

<script>
import Noticia from '@/components/Noticia.vue'
export default {
  data: () => ({
    search: '',
    data: [],
    trends: ['COVID', 'Elecciones 2020 US', 'Vaccines'],
  }),
  components: { Noticia },
  methods: {
    async doTrend(index) {
      this.search = this.trends[index]
      await this.doSearch()
    },
    async doSearch() {
      if (this.search == '') {
        this.data = []
        return
      }
      try {
        const { data } = await this.$axios.get(`/?q=${this.search}`)
        this.data = data.claims
      } catch (error) {
        console.log(error)
      }
    },
  },
}
</script>

<style>
.input {
  @apply block;
  @apply border;
  @apply rounded-lg;
  @apply border-gray-300;
  @apply border;
  @apply border-solid;
  @apply w-full;
  @apply px-6;
  @apply py-2;
  @apply mb-10;
}
.trends {
  @apply bg-gray-100;
  @apply p-4;
  @apply mb-4;
  @apply rounded;
}
.tred-title {
  @apply mb-2;
  @apply font-semibold;
}
</style>
