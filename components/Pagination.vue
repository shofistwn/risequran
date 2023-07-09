<script>

export default {
  props: {
    pagination: {
      Type: Object,
      Required: true
    },
  },
}
</script>

<template>
  <div class="text-white font-bold flex justify-between rounded-md my-6">
    <NuxtLink :to="{ name: pagination.type + '-nomor', params: { nomor: pagination.suratSebelumnya.nomor } }"
      class="flex items-center gap-x-2 px-4 py-2 rounded bg-gray-800 hover:bg-gray-700" v-if="pagination.suratSebelumnya">
      <IconsArrowLeft />

      {{ pagination.suratSebelumnya.namaLatin }}
    </NuxtLink>

    <NuxtLink :to="{ name: pagination.type + '-nomor', params: { nomor: pagination.suratSelanjutnya.nomor } }"
      class="flex items-center gap-x-2 px-4 py-2 rounded bg-gray-800 hover:bg-gray-700 text-right"
      v-if="pagination.suratSelanjutnya">
      {{ pagination.suratSelanjutnya.namaLatin }}

      <IconsArrowRight />
    </NuxtLink>
  </div>
</template>