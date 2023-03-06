<script setup lang="ts">
import LoadingSvg from "@/components/svgs/Loading.vue";

export type Activity = {
  resource_state: number;
  athlete: {
    resource_state: number;
    firstname: string;
    lastname: string;
  };
  name: string;
  distance: number;
  moving_time: number;
  elapsed_time: number;
  total_elevation_gain: number;
  type: string;
  sport_type: string;
  workout_type: number;
};

defineProps<{
  title: string;
  activities: Activity[];
}>();
</script>

<template>
  <div class="p-2 bg-yellow-50 text-sm">
    <h1 class="mb-1 font-bold">{{ title }}</h1>

    <ul v-if="activities.length" class="text-xs">
      <li v-for="activity in activities">
        {{ activity.name }} ({{ (activity.distance / 1000).toFixed(1) }}km)
      </li>
    </ul>

    <div v-else class="flex justify-center p-2">
      <LoadingSvg />
    </div>
  </div>
</template>
