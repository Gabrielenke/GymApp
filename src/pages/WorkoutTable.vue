<template>
  <div class="flex flex-col gap-10 p-4">
    <q-card class="flex flex-col">
      <q-input
        v-model="WorkoutName"
        color="black"
        label-color="black"
        label="Workout Name"
        class="p-2"
      />
      <q-input
        v-model="WorkoutDate"
        color="black"
        label-color="black"
        type="date"
        class="p-2"
        label="Workout Date"
      />
      <q-input
        v-model="WorkoutStartTime"
        color="black"
        label-color="black"
        type="time"
        class="p-2"
        label="Start Time"
      />
      <q-input
        v-model="WorkoutEndTime"
        color="black"
        label-color="black"
        type="time"
        class="p-2"
        label="End Time"
      />
      <q-input
        v-model="WorkoutNotes"
        color="black"
        label-color="black"
        type="textarea"
        class="p-2"
        autogrow
        label="Notes"
      />
    </q-card>

    <q-card
      v-for="(exercise, exerciseIndex) in exercises"
      :key="exerciseIndex"
      class=""
    >
      <q-input
        v-model="exercise.exerciseName"
        filled
        debounce="300"
        placeholder="Exercise name"
      />
      <q-separator />
      <q-input
        v-model="exercise.description"
        filled
        type="textarea"
        autogrow
        debounce="300"
        placeholder="Description Exercise"
      />
      <div v-for="(set, setIndex) in exercise.sets" :key="setIndex" class="">
        <div class="flex gap-4 px-4 items-center">
          <q-input v-model="set.series" class="p-1" label="Series" borderless />
          <q-input v-model="set.weight" label="Weight" borderless />
          <q-input v-model="set.repetitions" label="Reps" borderless />
          <q-input v-model="set.notes" label="Notes" borderless />
          <q-btn
            class="absolute right-0"
            size="10px"
            color="red"
            flat
            @click="exercise.sets.splice(setIndex, 1)"
            icon="delete"
          />
        </div>
        <q-separator inset />
      </div>

      <q-btn @click="addSet(exerciseIndex)" flat no-caps label="Add Set" />
    </q-card>
    <q-btn @click="addExercise" label="Add Exercise" />
    <q-btn label="Submit" @click="handleSubmit" />
  </div>
</template>

<script setup>
import { reactive, ref } from "vue";

const exercises = reactive([]);

const WorkoutName = ref("");
const WorkoutDate = ref("");
const WorkoutStartTime = ref("");
const WorkoutEndTime = ref("");
const WorkoutNotes = ref("");

const addExercise = () => {
  exercises.push({
    exerciseName: "",
    exerciseOrder: exercises.length + 1,
    description: "",
    sets: [
      {
        series: 1,
        weight: 0,
        repetitions: 0,
        notes: "",
      },
    ],
  });
};

const addSet = (exercise) => {
  exercises[exercise].sets.push({
    series: exercises[exercise].sets.length + 1,
    weight: 0,
    repetitions: 0,
    notes: "",
  });
};

const workoutDuration = () => {
  const startTime = WorkoutStartTime.value;
  const endTime = WorkoutEndTime.value;

  const date = new Date().getDate();

  const start = new Date(`${date} ${startTime}`);
  const end = new Date(`${date} ${endTime}`);

  const duration = end - start;

  return duration / 1000 / 60;
};

const handleSubmit = () => {
  const workoutData = {
    workout_name: WorkoutName.value,
    workout_date: WorkoutDate.value,
    workout_start_time: WorkoutStartTime.value,
    workout_end_time: WorkoutEndTime.value,
    workout_notes: WorkoutNotes.value,
    workout_duration: workoutDuration(),
    exercises: exercises.map((exercise) => {
      return {
        name: exercise.exerciseName,
        exercise_order: exercise.exerciseOrder,
        series: exercise.sets.map((set) => {
          return {
            series_order: set.series,
            weight: Number(set.weight),
            repetitions: Number(set.repetitions),
            notes: set.notes,
          };
        }),
      };
    }),
  };

  console.log(workoutData);
  console.log(JSON.stringify(workoutData));
};
</script>
