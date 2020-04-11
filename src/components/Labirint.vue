<template>
  <div class="hello">
    <button @click="findRoute">Найти путь</button>
    <table>
      <tbody>
        <tr v-for="(row, i) in labirint" :key="i">
          <td :class="cell.active && 'active'" v-for="(cell, j) in row" :key="i+''+j">{{cell.val}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "Labirint",
  data: () => ({
    routeFinded: false,
    labirint: [
      [36, 22, 78, 70, 30, 40, 12, 13, 52],
      [40, 94, 96, 80, 16, 54, 30, 77, 72],
      [42, 74, 48, 54, 76, 64, 44, 68, 92],
      [60, 56, 28, 22, 98, 86, 18, 22, 36],
      [80, 69, 12, 30, 40, 36, 32, 62, 52],
      [84, 78, 20, 88, 24, 46, 72, 50, 64],
      [92, 38, 22, 90, 66, 34, 96, 34, 70],
      [16, 24, 32, 28, 50, 38, 76, 16, 56],
      [22, 46, 14, 82, 94, 82, 62, 26, 88]
    ].map(row => row.map(val => ({ val, checked: false, active: false })))
  }),
  methods: {
    async checkStep(i, j) {
      if (!(this.labirint[i] && this.labirint[i][j])) return;

      if (!this.labirint[i][j].checked && this.labirint[i][j].val % 4 === 0) {
        this.labirint[i][j].active = true;
        if (i === this.labirint.length - 1) return (this.routeFinded = true);
        await new Promise(r => setTimeout(r, 500));
        this.findNextStep(i, j);
      }
      this.labirint[i][j].checked = true;
    },
    findNextStep(i, j) {
      this.checkStep(i + 1, j);
      this.checkStep(i - 1, j);
      this.checkStep(i, j + 1);
      this.checkStep(i, j - 1);
    },
    findRoute() {
      this.labirint[0].forEach((v, j) => {
        this.checkStep(0, j);
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
td.active {
  background: yellowgreen;
}
</style>
