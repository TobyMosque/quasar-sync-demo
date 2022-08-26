<template>
  <q-markdown :src="markdown"> </q-markdown>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { Person } from 'src/models/Person';

const props = defineProps<{
  title: string;
  people?: Person[];
}>();

const markdown = computed(() => {
  return `
::: info ${props.title}
\`\`\`json
${JSON.stringify(props.people, null, 2)}
\`\`\`
:::
  `;
});
</script>
