<template>
  <tr>
    <td>{{ row.number }}</td>
    <td><input type="text" v-model="row.name"></td>
    <td>{{ new Date(row.date) }}</td>
    <td>{{ getStatus() }}</td>
    <td>
      <div>
        <p class="checkbox" @click="$emit('change-value', n)">
          <span class="marker" :class="{checked : row.isChecked === true}"></span>
        </p>
      </div>
    </td>
  </tr>
</template>

<script>
export default {
  name: 'Row',

  props: {
    row: Object,
    n: Number,
  },

  methods: {
    getStatus() {
      return this.row.status ? 'complited' : 'in progress';
    },
  },
};
</script>

<style scoped>
  .checkbox {
    width: 20px;
    height: 20px;
    border: 1px solid;
    margin: 0 auto;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 3px;
  }

  .marker {
    display: none;
    width: 16px;
    height: 16px;
    background-color: rgb(8, 105, 37);
    border-radius: 3px;
  }

  .checked {
    display: inline-block;
  }

</style>
