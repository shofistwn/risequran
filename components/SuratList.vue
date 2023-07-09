<script>
export default {
  props: {
    suratList: {
      Type: Object,
      Required: true
    },
  }
}
</script>

<template>
  <div class="flex flex-col justify-center gap-y-6 mt-6">
    <NuxtLink :to="{ name: 'surat-nomor', params: { nomor: surat.nomor } }"
      class="bg-white flex items-center gap-x-5 rounded-md border p-3" v-for="(surat, index) in suratList" :key="index">
      <div class="flex justify-center items-center bg-gray-800 rounded-full w-12 h-12 text-2xl text-white">
        {{ surat.nomor }}
      </div>

      <div>
        <h2 class="text-xl font-bold">
          {{ surat.namaLatin }}
        </h2>
        <p class="italic">
          {{ surat.arti }}
        </p>
      </div>

      <div class="flex-auto text-right">
        <p class="text-arab text-2xl">
          {{ surat.nama }}
        </p>
      </div>
    </NuxtLink>
  </div>
</template>