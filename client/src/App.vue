<template>
  <div id='app'>
    <h1>Note Cards</h1>
    <NoteCard
      :card="currentCard"
      @correct="onCorrectAnswer"
      @incorrect="onIncorrectAnswer"
    />
    <Statistics :statistics="statistics" />
    <Options :strings.sync="strings" />
  </div>
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

<style>
</style>
