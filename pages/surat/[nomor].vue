<script>
import axios from 'axios'

export default {
  data() {
    return {
      isLoading: true,
      surat: [],
      ayatList: [],
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
        const res = await axios.get(`https://equran.id/api/v2/surat/${this.$route.params.nomor}`)
        const data = res.data.data
        this.surat = {
          namaLatin: data.namaLatin,
          nama: data.nama,
          deskripsi: data.deskripsi,
          nomorSurat: data.nomor,
          audio: data.audioFull['05']
        }
        this.ayatList = data.ayat
        this.pagination = {
          type: 'surat',
          suratSebelumnya: data.suratSebelumnya,
          suratSelanjutnya: data.suratSelanjutnya
        }
      } catch (error) {
        console.log(error);
      } finally {
        this.isLoading = false
      }
    }
  },
}
</script>

<template>
  <div>
    <div v-if="isLoading">
      <p class="text-center">Memuat...</p>
    </div>

    <div v-else>

      <Head>
        <Title>Surat {{ surat.namaLatin }} - RiseQuran</Title>
      </Head>

      <Pagination :pagination="pagination" />

      <SuratDetail :surat="surat" />

      <BasmalahText />

      <AyatSuratList :nomorSurat="surat.nomorSurat" :ayatList="ayatList" />

      <Pagination :pagination="pagination" />
    </div>
  </div>
</template>
