<script>
export default {
  props: {
    ayatList: {
      type: Array,
      required: true
    },
    nomorSurat: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      audioStatus: {}
    }
  },
  methods: {
    playAudio(nomorAyat, audioUrl) {
      this.stopCurrentAudio();
      this.audioStatus[nomorAyat] = true;
      const audioElement = new Audio(audioUrl);
      audioElement.addEventListener('ended', this.audioEndedHandler);
      audioElement.play();
      this.currentAudio = audioElement;
    },
    stopAudio(nomorAyat) {
      this.audioStatus[nomorAyat] = false;
      this.stopCurrentAudio();
    },
    stopCurrentAudio() {
      for (const key in this.audioStatus) {
        if (this.audioStatus.hasOwnProperty(key) && this.audioStatus[key]) {
          this.audioStatus[key] = false;
        }
      }

      if (this.currentAudio) {
        this.currentAudio.removeEventListener('ended', this.audioEndedHandler);
        this.currentAudio.pause();
        this.currentAudio.currentTime = 0;
      }
    },
    audioEndedHandler() {
      for (const key in this.audioStatus) {
        if (this.audioStatus.hasOwnProperty(key) && this.audioStatus[key]) {
          this.audioStatus[key] = false;
        }
      }
      this.currentAudio = null;
    }
  },
}
</script>

<template>
  <div class="flex flex-col mt-6 gap-y-6">
    <div class="flex flex-col bg-white border rounded-md" v-for="ayat in ayatList" :key="ayat.nomorAyat">
      <div class="bg-gray-800 flex justify-between items-center px-4 py-2 rounded text-white">
        <div class="flex justify-center items-center text-xl">
          {{ nomorSurat }}:{{ ayat.nomorAyat }}
        </div>

        <div>
          <button v-if="!audioStatus[ayat.nomorAyat]" @click.prevent="playAudio(ayat.nomorAyat, ayat.audio['05'])"
            class="flex items-center gap-x-2 px-3 py-1 rounded hover:bg-gray-700">
            Putar Audio
            <IconsPlay />
          </button>
          <button v-else @click.prevent="stopAudio(ayat.nomorAyat)"
            class="flex items-center gap-x-2 px-3 py-1 rounded hover:bg-gray-700">
            Stop Audio
            <IconsStop />
          </button>
        </div>
      </div>

      <div class="p-4">
        <p class="text-4xl text-arab text-right leading-relaxed">
          {{ ayat.teksArab }}
        </p>

        <p class="text-lg mt-4">
          {{ ayat.teksLatin }}
        </p>

        <hr class="my-4">

        <p class="italic">
          "{{ ayat.teksIndonesia }}"
        </p>
      </div>

    </div>
  </div>
</template>