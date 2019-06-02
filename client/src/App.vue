<template>
  <section class="note-cards section is-medium">
    <div class="container">
      <div class="columns">
        <div class="column is-three-quarters">
          <NoteCard
            :card="currentCard"
            @correct="onCorrectAnswer"
            @incorrect="onIncorrectAnswer"
          />
        </div>
        <div class="column">
          <Statistics :statistics="statistics" />
          <Options :strings.sync="strings" />
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import NoteCard from './components/note_card';
import Statistics from './components/statistics';
import Options from './components/options';

export default {
  name: 'App',
  components: { NoteCard, Statistics, Options },
  data() {
    return {
      strings: ['E', 'A', 'D', 'G', 'B'],
      currentCard: {},
      statistics: {
        questions: 0,
        correct: 0,
        incorrect: 0,
      },
    };
  },
  methods: {
    randomInt(max) {
      return Math.floor(Math.random() * Math.floor(max));
    },
    generateCard() {
      const notes = [
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
      ];

      const string = this.strings[this.randomInt(this.strings.length)];
      const fret = this.randomInt(12);
      const answer = notes[(notes.indexOf(string) + fret) % 12];

      return { fret, string, answer };
    },
    onCorrectAnswer() {
      this.statistics.questions += 1;
      this.statistics.correct += 1;
      this.nextCard();
    },
    onIncorrectAnswer() {
      this.statistics.questions += 1;
      this.statistics.incorrect += 1;
      this.nextCard();
    },
    nextCard() {
      this.currentCard = this.generateCard();
    },
  },
  mounted() {
    this.nextCard();
  },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Questrial&display=swap');
$family-primary: 'Questrial', sans-serif;
$seafoam: hsl(174, 62%, 47%);
$orange: hsl(35, 100%, 55%);
$primary: $seafoam;
@import "../node_modules/bulma/bulma";

.note-cards {
  padding-top: 1.5rem;

  .card {
    border-radius: 20px;

    .card-header {
      border-radius: 20px 20px 0 0;
    }
  }
}
</style>
