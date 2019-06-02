<template>
  <div class="options">
    <h2>Options</h2>
    <h3>Strings</h3>
    <template v-for="string in stringOptions">
      <input
        type="checkbox"
        :id="`string-${string}`"
        :value="string"
        v-model="strings"
        v-bind:key="`checkbox-string-${string}`"
      >
      <label
        :for="`string-${string}`"
        v-bind:key="`label-string-${string}`"
      >
        {{ string }}
      </label>
    </template>
  </div>
</template>

<script>
export default {
  data() {
    return {
      strings: [
        'E',
        'A',
        'D',
        'G',
        'B',
      ],
      stringOptions: [
        'E',
        'A',
        'D',
        'G',
        'B',
      ],
    };
  },
  watch: {
    strings(val) {
      this.$emit('update:strings', val);
    },
  },
};
</script>

<style scoped>
</style>
