<template>
  <div class="card has-text-centered">
    <div class="card-content">
      <div class="level">
        <div class="level-item">
          <p class="is-size-4">
            The
            <template v-if="card.fret === 0">
              <strong class="has-text-primary">
                root note
              </strong>
              of
            </template>
            <template v-else>
              <strong class="has-text-primary">
                {{ card.fret | numeral('Oo') }}
              </strong>
              fret on
            </template>
            the
            <strong class="has-text-primary">
              {{ card.string }}
            </strong>
            string is:
          </p>
        </div>
      </div>
      <div
        class="answers level buttons"
        v-for="noteGroup in noteGroups"
        v-bind:key="noteGroup"
      >
        <button
          class="button answer-button"
          v-for="note in noteGroup"
          v-bind:key="note"
          @click="answer(note)"
        >
          {{ note }}
        </button>
      </div>
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
  computed: {
    noteGroups() {
      const n = 4;

      return Array.from(
        Array(Math.ceil(this.notes.length / n)),
        (_, i) => this.notes.slice(i * n, i * n + n),
      );
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

<style lang="scss" scoped>
$answer-button-size: 70px;

.answer-button {
  width: $answer-button-size;
  height: $answer-button-size;
  border-radius: 100%;
  margin-left: auto;
  margin-right: auto;
}
</style>
