<template>
  <section class="flex items-start p-4 gap-2 justify-center">
    <q-card class="flex flex-col">
      <q-card-section class="bg-[#13161d] text-white">
        <div class="text-h6">My Workout</div>
      </q-card-section>

      <q-separator />

      <q-card-actions class="flex flex-col gap-2">
        <q-btn
          :icon="fasClipboardList"
          class="full-width"
          color="standart"
          text-color="black"
          label="New Workout"
          to="/create-workout"
        />
      </q-card-actions>
    </q-card>

    <div class="w-1/2">
      <q-card class="">
        <q-card-section class="bg-[#13161d] text-white">
          <div class="text-h6">My routines ()</div>
        </q-card-section>

        <q-separator />

        <q-card-actions class="flex flex-col gap-2"> </q-card-actions>
      </q-card>
    </div>
  </section>
</template>

<script setup>
import { fasClipboardList } from "@quasar/extras/fontawesome-v5";

const lorem =
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.";
</script>
