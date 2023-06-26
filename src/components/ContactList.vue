<script setup>
import { ref } from 'vue'
import { computed } from 'vue'
import ContactListItem from './ContactListItem.vue'
const props = defineProps(['contacts']);
const emit = defineEmits(['delete']);

const search = ref('');

const handleContactDelete = (contact) => {
  emit('delete', contact)
};

const filteredContacts = computed(() => {
  if (search.value === '') {
    return props.contacts
  } else {
    return props.contacts.filter((contact) =>
      `${contact.firstName} ${contact.lastName}`.toLowerCase().includes(search.value.toLowerCase())
    )
  }
});
</script>

<template>
  <div class="panel is-success">
    <div class="panel-heading">Contacts</div>
    <div class="panel-block is-flex is-flex-direction-column is-align-items-stretch">
      <div class="field mb-3">
        <div class="control">
          <input v-model="search" type="text" class="input" placeholder="Search contacts" />
        </div>
      </div>
      <div v-for="contact in filteredContacts" :key="contact.phoneNumber">
        <ContactListItem :contact="contact" @delete="handleContactDelete(contact)" />
      </div>
    </div>
  </div>
</template>

<style scoped></style>
