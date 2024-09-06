<script setup>
const items = [{
  label: 'Carriers',
  icon: 'i-heroicons-truck',
  defaultOpen: true,
  description: 'getting-started'
}, {
  label: 'Customers',
  icon: 'i-heroicons-user',
  defaultOpen: true,
  description: 'installation'
}, {
  label: 'Requests',
  icon: 'i-heroicons-archive-box',
  defaultOpen: true,
  description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed neque elit, tristique placerat feugiat ac, facilisis vitae arcu. Proin eget egestas augue. Praesent ut sem nec arcu pellentesque aliquet. Duis dapibus diam vel metus tempus vulputate.'
}]
</script>

<template>
  <UAccordion :items="items" multiple>
    <template #item="{ item }">
      <div>
        <UCheckbox name="baz" label="Can create records" />
        <UCheckbox name="foo" label="Can update records" />
        <UCheckbox name="bar" label="Can remove records" />
      </div>
    </template>
  </UAccordion>
  <UButton label="Save" color="green" />
</template>
