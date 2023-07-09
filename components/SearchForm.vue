<script>
export default {
  data() {
    return {
      query: ''
    };
  },
  methods: {
    emitValue() {
      this.$emit('query', this.query);
    }
  }
}
</script>

<template>
  <div>
    <input type="text" placeholder="Cari..." v-model="query" @input="emitValue"
      class="border rounded-md px-4 py-3 w-full text-lg focus:outline-gray-800">
  </div>
</template>