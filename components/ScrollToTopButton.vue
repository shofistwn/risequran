<template>
  <button class="sticky float-right right-6 bottom-10 md:right-10 md:bottom-20 lg:right-20 xl:right-48"
    @click="scrollToTop" v-if="showButton">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" stroke-width="1" stroke="currentColor"
      class="w-14 h-14 fill-transparent hover:fill-gray-800 hover:stroke-white">
      <path stroke-linecap="round" stroke-linejoin="round"
        d="M15 11.25l-3-3m0 0l-3 3m3-3v7.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
    </svg>
  </button>
</template>

<script>
export default {
  data() {
    return {
      showButton: false,
      scrollOffset: 300,
      scrollDuration: 500,
    };
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    handleScroll() {
      this.showButton = window.pageYOffset > this.scrollOffset;
    },
    scrollToTop() {
      const scrollStep = -window.scrollY / (this.scrollDuration / 15);
      const scrollInterval = setInterval(() => {
        if (window.scrollY !== 0) {
          window.scrollBy(0, scrollStep);
        } else {
          clearInterval(scrollInterval);
        }
      }, 15);
    },
  },
};
</script>