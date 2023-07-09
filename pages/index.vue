<script>
import axios from 'axios'

export default {
  data() {
    return {
      isLoading: true,
      suratList: [],
    }
  },
  mounted() {
    this.getData()
  },
  methods: {
    async getData(query) {
      this.isLoading = true

      if (!query) {
        query = ''
      }

      try {
        const res = await axios.get('https://equran.id/api/v2/surat')
        this.suratList = res.data.data.filter((surat) => {
          return (
            surat.namaLatin.toLowerCase().includes(query.toLowerCase()) ||
            surat.arti.toLowerCase().includes(query.toLowerCase())
          );
        });
      } catch (error) {
        console.log(error);
      } finally {
        this.isLoading = false
      }
    },
    searchSurat(query) {
      this.getData(query)
    }
  }
}
</script>

<template>
  <div>
    <SearchForm @query="searchSurat" />
    <div v-if="isLoading">
      <p class="text-center mt-6">Memuat...</p>
    </div>
    <div v-else>

      <SuratList :suratList="suratList" />
    </div>
  </div>
</template>