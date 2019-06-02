<template>
  <div class="card">
    <div class="card-header">
      <p class="card-header-title is-centered">Statistics</p>
    </div>
    <div class="card-content">
      <progress
        class="progress"
        :class="gradeClass"
        :value="statistics.questions"
        :max="goal"
      >
        15%
      </progress>
      <table class="table is-fullwidth">
        <tbody>
          <tr>
            <th>Notes</th>
            <td>{{ statistics.questions }} / {{ goal }}</td>
          </tr>
          <tr>
            <th>Correct</th>
            <td>{{ statistics.correct }} ({{ pct | numeral('0%') }})</td>
          </tr>
          <tr>
            <th>Incorrect</th>
            <td>{{ statistics.incorrect }} ({{ 1 - pct | numeral('0%') }})</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    statistics: {
      type: Object,
      required: true,
    },
  },
  data() {
    return { goal: 20 };
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
    gradeClass() {
      if (this.statistics.questions === 0) { return ''; }

      if (this.letter === 'A') {
        return 'is-success';
      } else if (this.letter === 'D') {
        return 'is-warning';
      } else if (this.letter === 'F') {
        return 'is-danger';
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.card {
  margin-bottom: 20px;
}
</style>
