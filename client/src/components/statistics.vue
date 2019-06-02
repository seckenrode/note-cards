<template>
  <table>
    <tbody>
      <tr>
        <th>Answered</th>
        <td>{{ statistics.questions }}</td>
      </tr>
      <tr>
        <th>Correct</th>
        <td>{{ statistics.correct }}</td>
      </tr>
      <tr>
        <th>Incorrect</th>
        <td>{{ statistics.incorrect }}</td>
      </tr>
      <tr :class="`grade-${this.letter.toLowerCase()}`">
        <th>Grade</th>
        <td>{{ grade }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    statistics: {
      type: Object,
      required: true,
    },
  },
  computed: {
    pct() {
      return this.statistics.correct / this.statistics.questions;
    },
    letter() {
      if (this.statistics.questions === 0) {
        return 'na';
      } else if (this.pct >= 0.9) {
        return 'A';
      } else if (this.pct >= 0.8) {
        return 'B';
      } else if (this.pct >= 0.7) {
        return 'C';
      } else if (this.pct > 0.6) {
        return 'D';
      }

      return 'F';
    },
    grade() {
      if (this.statistics.questions === 0) { return 'N/A'; }

      return `${this.letter} (${Math.round(100 * this.pct)}%)`;
    },
  },
};
</script>

<style scoped>
.grade-a {
  background-color: green;
}
.grade-b {
  background-color: blue;
}
.grade-c {
  background-color: yellow;
}
.grade-d {
  background-color: orange;
}
.grade-f {
  background-color: red;
}
</style>
