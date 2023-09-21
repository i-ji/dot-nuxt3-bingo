<template>
  <div>
    <table>
      <thead>
        <tr>
          <th>B</th>
          <th>I</th>
          <th>N</th>
          <th>G</th>
          <th>O</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="tr in bingo" :key="tr">
          <td>{{ tr[0] }}</td>
          <td>{{ tr[1] }}</td>
          <td>{{ tr[2] }}</td>
          <td>{{ tr[3] }}</td>
          <td>{{ tr[4] }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup lang="ts">
function createColumn(col: number): number[] {
  const source = ref<number[]>([]);
  for (let i = ref<number>(0); i.value < 15; i.value++) {
    source.value[i.value] = i.value + 1 + 15 * col;
  }

  const column = ref<number[]>([]);

  for (let i = ref<number>(0); i.value < 5; i.value++) {
    column.value[i.value] = source.value.splice(
      Math.floor(Math.random() * source.value.length),
      1
    )[0];
  }

  return column.value;
}

const columns = ref<any[]>([]);
columns.value[0] = createColumn(0);
columns.value[1] = createColumn(1);
columns.value[2] = createColumn(2);
columns.value[3] = createColumn(3);
columns.value[4] = createColumn(4);
columns.value[2][2] = "free";

console.table(columns.value);

const bingo = ref<any[]>([]);
for (let row = ref(0); row.value < 5; row.value++) {
  bingo.value[row.value] = [];
  for (let col = ref(0); col.value < 5; col.value++) {
    bingo.value[row.value][col.value] = columns.value[col.value][row.value];
  }
}
console.table(bingo.value);
</script>
