<template>
  <q-page class="row items-center justify-evenly">
    <div>
      <fake-list v-model:people="people"></fake-list>
      <code-people title="Parent Data" :people="people"></code-people>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { Person } from 'src/models/Person';
import { ref } from 'vue';
import FakeList from 'src/components/FakeList.vue';
import CodePeople from 'src/components/CodePeople.vue';

const people = ref<Person[]>();
</script>
