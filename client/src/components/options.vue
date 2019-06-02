<template>
  <div class="card">
    <div class="card-header">
      <p class="card-header-title is-centered">Options</p>
    </div>
    <div class="card-content">
      <div class="field">
        <label class="label">Strings (space separated)</label>
        <div class="control">
          <input
            class="input"
            type="text"
            v-model="strings"
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      strings: 'E A D G D'
    };
  },
  watch: {
    strings(val) {
      const newStrings = val.split(" ").map((str) => str.replace(/\s/g, ""));
      this.$emit('update:strings', newStrings);
    },
  },
};
</script>

<style scoped>
</style>
