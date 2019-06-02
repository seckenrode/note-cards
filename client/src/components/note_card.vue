<template>
  <div class="card">
    The {{ card.fret | numeral('Oo') }}
    fret on the {{ card.string }} string is:
    <div class="answers">
      <button
        v-for="note in notes"
        v-bind:key="note"
        @click="answer(note)"
      >
        {{ note }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      notes: [
        'A',
        'A#',
        'B',
        'C',
        'C#',
        'D',
        'D#',
        'E',
        'F',
        'F#',
        'G',
        'G#',
      ],
    };
  },
  props: {
    card: {
      type: Object,
      required: true,
    },
  },
  methods: {
    answer(value) {
      if (value === this.card.answer) {
        this.$emit('correct');
      } else {
        this.$emit('incorrect');
      }
    },
  },
};
</script>

<style>
</style>
