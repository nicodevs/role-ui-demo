<script setup>
const columns = [{
  key: 'id',
  label: 'ID'
}, {
  key: 'name',
  label: 'Name',
  sortable: true
}, {
  key: 'title',
  label: 'Title',
  sortable: true
}, {
  key: 'email',
  label: 'Email',
  sortable: true,
  direction: 'desc'
}, {
  key: 'actions'
}]

const people = [{
  id: 1,
  name: 'Lindsay Walton',
  title: 'Front-end Developer',
  email: 'lindsay.walton@example.com',
}, {
  id: 2,
  name: 'Courtney Henry',
  title: 'Designer',
  email: 'courtney.henry@example.com',
}, {
  id: 3,
  name: 'Tom Cook',
  title: 'Director of Product',
  email: 'tom.cook@example.com',
}, {
  id: 4,
  name: 'Whitney Francis',
  title: 'Copywriter',
  email: 'whitney.francis@example.com',
}, {
  id: 5,
  name: 'Leonard Krasner',
  title: 'Senior Designer',
  email: 'leonard.krasner@example.com',
}, {
  id: 6,
  name: 'Floyd Miles',
  title: 'Principal Designer',
  email: 'floyd.miles@example.com',
}]

const  modalPeople = ['Jensen Combs','Annie Copeland'];

const q = ref('')

const selected = ref([])

const filteredRows = computed(() => {
  if (!q.value) {
    return people
  }

  return people.filter((person) => {
    return Object.values(person).some((value) => {
      return String(value).toLowerCase().includes(q.value.toLowerCase())
    })
  })
})

const isOpen = ref(false)

const modalSelected = ref([])
const modalQuery = ref('')

const tabs = [{
  label: 'Permissions',
  icon: 'i-heroicons-information-circle',
  content: 'Manage permissions'
}, {
  label: 'Users',
  icon: 'i-heroicons-user-group',
  content: 'Manage users'
}]

function onTabChange (index) {
selectedTab.value = index
}

const selectedTab = ref(0)
</script>

<template>
  <div class="p-16">

    <h1 class="text-3xl font-bold mb-4">Credit 1</h1>

    <div>
        <UTabs :items="tabs" @change="onTabChange" />
    </div>

    <div v-if="selectedTab === 0">
        <Perms />
    </div>

    <div v-if="selectedTab === 1">
        <div class="flex justify-between px-3 py-3.5 border-b border-gray-200 dark:border-gray-700">
      <div class="flex gap-2">
          <UInput v-model="q" placeholder="Filter people..." />
          <UButton label="Remove Role from Users" color="red" v-if="selected.length" />
      </div>
      <UButton label="Add User to Role" color="green" @click="isOpen = true" />
    </div>

    <UTable v-model="selected" :rows="filteredRows" :columns="columns">
        <template #actions-data="{ row }">
            <UButton label="Remove Role" color="red" />
        </template>
    </UTable>

    <UModal v-model="isOpen">
        <UCard :ui="{ ring: '', divide: 'divide-y divide-gray-100 dark:divide-gray-800' }">
            <template #header>
            Add User to Rol
            </template>
                <UInputMenu
                    v-model="modalSelected"
                    v-model:query="modalQuery"
                    :options=" modalPeople"
                    placeholder="Select a person"
                />

                <template #footer>
                    <UButton label="Add" color="green" />
                </template>
            </UCard>
    </UModal>
    </div>

  </div>
</template>

<style>
#headlessui-tabs-panel-v-2{
    display: none;}
#headlessui-tabs-panel-v-3{
    display: none;}
</style>
