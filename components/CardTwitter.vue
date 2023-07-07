<script setup lang="ts">
const props = defineProps<{url: string; temperature: number}>();
const {chat, state, firstMessage} = useChatAi({agent: "twitter"})
const announcement = computed(() => firstMessage.value?.content);

const generate = () => nextTick(() => chat(props)); //alias chat function as a generate function
defineExpose({
  generate
});

const postURL = computed(
  () =>
    `https://twitter.com/intent/tweet?text=${encodeURIComponent(
      announcement.value || ""
    )}`
);
</script>
<template>
  <CardGeneric
    title="Twitter"
    :state="state"
    :body="announcement"
    class="mb-10"
  >
    <div class="flex w-full justify-between items-center">
      <div class="text-xs">
        Character Count:
        <strong>{{ announcement?.length }}</strong>
      </div>
      <div>
        <button class="btn btn-neutral" @click="generate()">Regenerate</button>
        <a class="btn btn-primary" target="_blank" :href="postURL">Post</a>
      </div>
    </div>
  </CardGeneric>
</template>