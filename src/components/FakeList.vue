<template>
  <div class="q-gutter-sm">
    <q-btn
      icon="add"
      label="add random person"
      color="primary"
      @click="addPerson"
    ></q-btn>
    <q-table title="People" :columns="columns" :rows="people" row-key="id">
      <template v-slot:body-cell-avatar="props">
        <q-td :props="props">
          <q-avatar>
            <img :src="props.value" />
          </q-avatar>
        </q-td>
      </template>
      <template v-slot:body-cell-actions="props">
        <q-td :props="props">
          <q-btn
            icon="delete"
            color="negative"
            dense
            round
            @click="deletePerson(props.value)"
          ></q-btn>
        </q-td>
      </template>
    </q-table>
    <code-people title="Child Data" :people="people"></code-people>
  </div>
</template>

<script setup lang="ts">
import { unref, computed, PropType } from 'vue';
import { Person } from 'src/models/Person';
import CodePeople from './CodePeople.vue';
import { uid } from 'quasar';
import { faker } from '@faker-js/faker';

faker.locale = 'en_US';
const emit = defineEmits<(env: 'update:people', val: Person[]) => void>();
const props = defineProps({
  people: {
    type: Array as PropType<Person[]>,
    default() {
      return [] as Person[];
    },
  },
});

const people = computed({
  get() {
    return props.people;
  },
  set(val: Person[]) {
    emit('update:people', val);
  },
});
const columns = [
  { name: 'avatar', label: 'Avatar', field: 'avatar', sortable: true },
  {
    name: 'firstName',
    label: 'First Name',
    field: 'firstName',
    sortable: true,
  },
  { name: 'lastName', label: 'Last Name', field: 'lastName', sortable: true },
  { name: 'email', label: 'Email', field: 'email', sortable: true },
  { name: 'actions', label: 'Actions', field: 'id', sortable: false },
];

const avatars = {
  men: [
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
    22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40,
    41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59,
    60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78,
    79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94,
  ],
  women: [
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
    22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40,
    41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59,
    60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78,
    79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94,
  ],
  lego: [1, 2, 3, 4, 5, 6, 7, 8],
};

function addPerson() {
  const gender = faker.helpers.arrayElement([
    'men',
    'women',
  ]) as keyof typeof avatars;
  const avatar = faker.helpers.arrayElement(avatars[gender]);

  const list = unref(people.value);
  list.push({
    id: uid(),
    avatar: `https://randomuser.me/api/portraits/${gender}/${avatar}.jpg`,
    firstName: faker.name.firstName(),
    lastName: faker.name.lastName(),
    email: faker.internet.email().toLowerCase(),
  });
  people.value = list;
}

function deletePerson(id: Person['id']) {
  const list = unref(people.value);
  const index = list.findIndex((person) => person.id === id);
  if (index !== -1) {
    list.splice(index, 1);
  }
  people.value = list;
}
</script>
