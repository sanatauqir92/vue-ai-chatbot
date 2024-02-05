<script setup lang="ts">
const props = defineProps<{
  url: string;
  temperature: number;
}>();
defineEmits(["submit"]);
const form = reactive({
  url: props.url,
  temperature: props.temperature,
});
</script>
<template>
  <p>Step 1: Copy and paste a url from a news source </p>
  <p>(ex: https://www.cnn.com/cnn-underscored/home/hgtv-jasmine-roth-home-essentials)</p>
  <p>Step 2: Drag the temperature slider to set how creative of an announcement you would like to generate</p>
  <form @submit.prevent="$emit('submit', form)" class="mb-10 mt-5">
    <div class="flex">
      <input
        placeholder="Full Article URL"
        v-model="form.url"
        class="input input-bordered rounded-r-none w-full max-w-full"
        type="text"
      />
      <button class="btn rounded-l-none">Generate Announcements</button>
    </div>
    <TemperatureSelector v-model="form.temperature" />
  </form>
</template>
