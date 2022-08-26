<template>
  <q-page class="row items-center justify-evenly">
    <div class="row full-width q-col-gutter-sm">
      <div class="col col-4">
        <fake-list v-model:people="people" :codeRef="codeRef"></fake-list>
      </div>
      <div class="col col-4">
        <code-people title="Parent Data" :people="people"></code-people>
      </div>
      <div class="col col-4">
        <div ref="codeRef" id="child-data-target"></div>
      </div>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { Person } from 'src/models/Person';
import { ref } from 'vue';
import FakeList from 'src/components/FakeList.vue';
import CodePeople from 'src/components/CodePeople.vue';

const people = ref<Person[]>();
const codeRef = ref<HTMLElement>();
</script>
