<script setup lang="ts">
/**
 * @usage
 *
 */
import { ref, onMounted } from "vue";
import type { Ref } from "vue";
import ClubActivitiesVue from "@/components/ClubActivities.vue";
import type { Activity } from "@/components/ClubActivities.vue";

const accessToken = import.meta.env.VITE_ACCESS_TOKEN;

// Svelte JS Club
const svelteJsActivities: Ref<Activity[]> = ref([]);
const svelteJsClubUrl = 756826;

// Norfolk Gazelles
const norfolkGazellesActivities: Ref<Activity[]> = ref([]);
const norfolkGazellesClubUrl = 77027;

// Avenues Junior School - Schools of Sanctuary
const schoolsOfSanctuaryActivities: Ref<Activity[]> = ref([]);
const schoolsOfSanctuaryUrl = 1115699;

// mobilityways
const mobilitywaysActivities: Ref<Activity[]> = ref([]);
const mobilitywaysUrl = 1118159;

// make a fetch request to the Strava API
const getActivities = async (clubId: number): Promise<Activity[]> => {
  const url = `https://www.strava.com/api/v3/clubs/${clubId}/activities?per_page=100`;
  let returnValue: Activity[] = [];
  await fetch(url, {
    headers: {
      Authorization: `Bearer ${accessToken}`,
    },
  })
    .then((response) => response.json())
    .then((data) => {
      console.log(data);
      returnValue = data.filter(
        (activity: Activity) => activity.athlete.firstname === "Clive"
      );
    })
    .catch((error) => {
      returnValue = [];
    });
  return returnValue;
};

onMounted(async () => {
  await getActivities(svelteJsClubUrl).then((activities) => {
    svelteJsActivities.value = activities;
  });
  await getActivities(norfolkGazellesClubUrl).then((activities) => {
    norfolkGazellesActivities.value = activities;
  });
  await getActivities(schoolsOfSanctuaryUrl).then((activities) => {
    schoolsOfSanctuaryActivities.value = activities;
  });
  await getActivities(mobilitywaysUrl).then((activities) => {
    mobilitywaysActivities.value = activities;
  });
});
</script>
<template>
  <div class="grid grid-cols-4 gap-2 p-2">
    <ClubActivitiesVue
      title="Svelte JS Club"
      :activities="svelteJsActivities"
    />
    <ClubActivitiesVue
      title="Norfolk Gazelles"
      :activities="norfolkGazellesActivities"
    />
    <ClubActivitiesVue
      title="Avenues Junior School - Schools of Sanctuary"
      :activities="schoolsOfSanctuaryActivities"
    />
    <ClubActivitiesVue
      title="mobilityways"
      :activities="mobilitywaysActivities"
    />
  </div>
</template>
