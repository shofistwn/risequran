<script>
export default {
  props: {
    tafsirList: {
      Type: Object,
      Required: true
    },
    nomor: {
      Type: Number,
      Required: true
    }
  }
}
</script>

<template>
  <div class="flex flex-col mt-6 gap-y-6">
    <div class="flex flex-col bg-white border rounded-md" v-for="ayat in tafsirList" :key="ayat.ayat">
      <div class="bg-gray-800 flex justify-between items-center px-4 py-2 rounded text-white">
        <div class="flex justify-center items-center text-xl">
          {{ nomor }}:{{ ayat.ayat }}
        </div>
      </div>

      <div class="p-4">
        <p class="text-lg whitespace-normal" v-html="ayat.teks">
        </p>
      </div>

    </div>
  </div>
</template>
