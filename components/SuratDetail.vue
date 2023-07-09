<script>
export default {
  props: {
    surat: {
      Type: Object,
      Required: true
    }
  },
}
</script>

<template>
  <div class="bg-white border rounded-md p-4">
    <div class="text-center">
      <h1 class="text-4xl font-bold">
        {{ surat.namaLatin }}
      </h1>
      <p class="text-arab text-2xl mt-2">
        {{ surat.nama }}
      </p>
    </div>

    <hr class="my-4">

    <p class="whitespace-normal text-lg" v-html="surat.deskripsi"></p>

    <hr class="my-4">

    <div class="flex justify-center gap-x-4">
      <NuxtLink :to="{ name: 'tafsir-nomor', params: { nomor: surat.nomorSurat } }"
        class="px-4 py-2 bg-gray-800 text-white font-bold rounded hover:bg-gray-700">Tafsir</NuxtLink>
    </div>
  </div>
</template>