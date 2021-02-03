<template>
  <div class="content-container">
    <h1>Content</h1>
    <Table
      :isAuthorized="isAuthorized"
      v-if="isAuthorized"
    />
    <div v-if="!isAuthorized">
      <h3>Authorization required</h3>
    </div>
  </div>
</template>

<script>
import Table from '@/components/Table.vue';

export default {
  name: 'Content',
  components: {
    Table,
  },

  props: {
    isAuthorized: Boolean,
  },
};
</script>
