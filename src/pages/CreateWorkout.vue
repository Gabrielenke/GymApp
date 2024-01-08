<template>
  <section class="flex w-[80vw] justify-center mt-8 gap-8">
    <div class="h-[40vh] w-1/2">
      <div class="flex justify-between w-full">
        <div class="flex items-center">
          <RouterLink to="/routines">
            <q-icon name="arrow_back" />
          </RouterLink>
          <p>Create Workout</p>
        </div>

        <q-btn>Save Workout</q-btn>
      </div>

      <div class="flex flex-col gap-2">
        <p>Workout Name</p>
        <q-input filled dense debounce="300" placeholder="Workout Name" />
      </div>

      <q-card>
        <q-card-section class="flex flex-col justify-center items-center gap-2">
          <template v-if="!exercises.length > 0">
            <svg width="65" height="35" xmlns="http://www.w3.org/2000/svg">
              <g
                fill="none"
                fill-rule="evenodd"
                stroke="#1D83EA"
                stroke-width="3.5"
              >
                <path d="M47.45 16.7v1.1h-29.5v-1.1h29.5z"></path>
                <rect x="48.25" y="1.75" width="8" height="31" rx="2"></rect>
                <rect x="8.25" y="1.75" width="8" height="31" rx="2"></rect>
                <rect
                  x="56.25"
                  y="8.25"
                  width="6.5"
                  height="17.5"
                  rx="2"
                ></rect>
                <rect
                  transform="matrix(-1 0 0 1 10 0)"
                  x="1.75"
                  y="8.25"
                  width="6.5"
                  height="17.5"
                  rx="2"
                ></rect>
                <path d="M56.575 6.9v19.716"></path>
              </g>
            </svg>
            <p class="">No exercises added</p>
            <p class="">
              So far, you haven't added any exercises to this routine.
            </p>
          </template>
        </q-card-section>
      </q-card>
    </div>

    <div class="w-[20%]">
      <q-card>
        <q-card-section class="flex justify-between">
          <p class="">Library</p>
          <p class="text-blue-600">Add exercise</p>
        </q-card-section>

        <q-separator />

        <q-card-actions class="gap-2" vertical>
          <q-select
            filled
            dense
            v-model="model"
            :options="optionsEquipments"
            label="All Equipment"
          />

          <q-select
            filled
            dense
            v-model="model"
            :options="optionsMuscle"
            label="All Muscles"
          />

          <q-input filled dense debounce="300" placeholder="Search">
            <template v-slot:append>
              <q-icon name="search" />
            </template>
          </q-input>

          <q-separator />

          <q-list v-for="(exercise, index) in exerciseList" :key="index">
            <q-item clickable v-ripple>
              <q-item-section avatar>
                <q-avatar
                  :color="exercise.avatarColor"
                  text-color="white"
                  :icon="exercise.avatarIcon"
                />
              </q-item-section>
              <div class="">
                <q-item-section>{{ exercise.name }}</q-item-section>
                <q-item-section>{{ exercise.muscleGroup }}</q-item-section>
              </div>
            </q-item>
          </q-list>
        </q-card-actions>
      </q-card>
    </div>
  </section>
</template>

<script setup>
const exercises = [];

const optionsEquipments = [
  { label: "Barbell", value: "barbell" },
  { label: "Dumbbell", value: "dumbbell" },
  { label: "Bodyweight", value: "bodyweight" },
  { label: "Cable", value: "cable" },
  { label: "Kettlebell", value: "kettlebell" },
  { label: "Machine", value: "machine" },
  { label: "Medicine Ball", value: "medicine-ball" },
  { label: "Resistance Band", value: "resistance-band" },
  { label: "Foam Roller", value: "foam-roller" },
  { label: "Other", value: "other" },
];

const optionsMuscle = [
  { label: "Abs", value: "abs" },
  { label: "Biceps", value: "biceps" },
  { label: "Calves", value: "calves" },
  { label: "Chest", value: "chest" },
  { label: "Forearms", value: "forearms" },
  { label: "Glutes", value: "glutes" },
  { label: "Hamstrings", value: "hamstrings" },
  { label: "Lats", value: "lats" },
  { label: "Lower Back", value: "lower-back" },
  { label: "Middle Back", value: "middle-back" },
  { label: "Neck", value: "neck" },
  { label: "Quadriceps", value: "quadriceps" },
  { label: "Shoulders", value: "shoulders" },
  { label: "Traps", value: "traps" },
  { label: "Triceps", value: "triceps" },
  { label: "Full Body", value: "full-body" },
  { label: "Other", value: "other" },
];

const exerciseList = [
  {
    name: "Exercise 1",
    muscleGroup: "Muscle Group",
    avatarColor: "teal",
    avatarIcon: "bluetooth",
  },
  {
    name: "Exercise 2",
    muscleGroup: "Muscle Group",
    avatarColor: "orange",
    avatarIcon: "wifi",
  },
];
</script>
