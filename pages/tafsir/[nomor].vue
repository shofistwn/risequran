<script>
import axios from 'axios'

export default {
  data() {
    return {
      isLoading: true,
      tafsir: [],
      tafsirList: [],
      pagination: [],
    }
  },
  mounted() {
    this.getData()
  },
  methods: {
    async getData() {
      this.isLoading = true
      try {
        const res = await axios.get(`https://equran.id/api/v2/tafsir/${this.$route.params.nomor}`)
        this.data = res.data.data
        const data = res.data.data
        this.tafsir = {
          namaLatin: data.namaLatin,
          nama: data.nama,
          deskripsi: data.deskripsi,
          nomorSurat: data.nomor
        }
        this.tafsirList = data.tafsir
        this.pagination = {
          type: 'tafsir',
          suratSebelumnya: data.suratSebelumnya,
          suratSelanjutnya: data.suratSelanjutnya
        }
      } catch (error) {
        console.log(error);
      } finally {
        this.isLoading = false
      }
    }
  }
}
</script>

<template>
  <div>
    <div v-if="isLoading">
      <p class="text-center">Memuat...</p>
    </div>
    <div v-else>

      <Head>
        <Title>Tafsir {{ tafsir.namaLatin }} - RiseQuran</Title>
      </Head>

      <Pagination :pagination="pagination" />

      <TafsirDetail :tafsir="tafsir" />

      <TafsirSuratList :nomor="tafsir.nomorSurat" :tafsirList="tafsirList" />

      <Pagination :pagination="pagination" />
    </div>
  </div>
</template>
