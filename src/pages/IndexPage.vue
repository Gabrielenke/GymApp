<template>
  <div class="q-pa-md">
    <q-input
      v-model="tableTitle"
      filled
      debounce="300"
      placeholder="Exercise name"
      style="width: 30%"
    />

    <q-table
      :title="tableTitle"
      :rows="rows"
      :columns="columns"
      row-key="series"
      :rows-per-page-options="[10]"
    >
      <template v-slot:top-right>
        <q-btn @click="addRow" label="Add Row" />
        <q-btn @click="removeLastRow" label="Remove Row" />
      </template>

      <template v-slot:bottom>
        <q-btn @click="postData" label="Send" />
      </template>

      <template v-slot:body="props">
        <q-tr :props="props">
          <q-td key="series" :props="props">
            <q-input
              class="q-mb-sm"
              v-model="props.row.series"
              filled
              dense
              debounce="300"
              placeholder="Series"
              style="width: 30%"
            />
          </q-td>

          <q-td key="weight" :props="props">
            <q-input
              v-model="props.row.weight"
              filled
              dense
              debounce="300"
              placeholder="Weight"
              style="width: 30%"
            />
          </q-td>

          <q-td key="reps" :props="props">
            <q-input
              v-model="props.row.reps"
              filled
              dense
              debounce="300"
              placeholder="Reps"
              style="width: 30%"
            />
          </q-td>

          <q-td key="notes" :props="props">
            <q-input
              v-model="props.row.notes"
              filled
              dense
              debounce="300"
              placeholder="Notes"
              style="width: 50%"
            />
          </q-td>
        </q-tr>
      </template>
    </q-table>
  </div>
</template>

<script setup>
import { reactive, ref } from "vue";
const tableTitle = ref("");
const columns = [
  {
    name: "series",
    required: true,
    label: "Series",
    align: "left",
    field: "series",
    sortable: true,
  },
  {
    name: "weight",
    align: "left",
    label: "Weight",
    field: "weight",
    sortable: true,
  },
  { name: "reps", label: "Reps", field: "reps", sortable: true, align: "left" },
  {
    name: "notes",
    label: "Notes",
    field: "notes",
    align: "left",
  },
];

const rows = reactive([
  { series: "1", weight: 22, reps: 5, notes: "" },
  { series: "2", weight: 22, reps: 5, notes: "" },
  { series: "3", weight: 22, reps: 5, notes: "" },
  { series: "4", weight: 22, reps: 5, notes: "" },
]);

const addRow = () => {
  const newSeries = String(rows.length + 1);
  const newRow = { series: newSeries, weight: 0, reps: 0, notes: "" };
  rows.push(newRow);
};

const removeLastRow = () => {
  if (rows.length > 0) {
    rows.pop();
  }
};

const postData = () => {
  const exerciseData = {
    name: tableTitle.value,
    series: rows.length,
    series_list: rows.map((row) => ({
      weight: row.weight,
      reps: row.reps,
      notes: row.notes,
    })),
  };

  console.log(exerciseData);
};
</script>

<style scoped></style>
