<template>
  <div class="table-container">
    <table class="table" border="3" cellspacing="0" cellpadding="5">
      <caption>Random data</caption>
      <tr>
        <th>
          <span>
            Number
          </span>
          <p>
            <button
              @click="tableData.sort((prev, next) => prev.number - next.number)">
              &uarr;
            </button>
            <button
              @click="tableData.sort((prev, next) => next.number - prev.number)">
              &darr;
            </button>
          </p>
        </th>
        <th>
          Name
          <p>
            <button
              @click="sortText('up')">
              &uarr;
            </button>
            <button
              @click="sortText('down')">
              &darr;
            </button>
          </p>
        </th>
        <th>
          Date
          <p>
            <button
              @click="tableData.sort((prev, next) => prev.date - next.date)">
              &uarr;
            </button>
            <button
              @click="tableData.sort((prev, next) => next.date - prev.date)">
              &darr;
            </button>
          </p>
        </th>
        <th>
          Status
          <p>
            <button
              @click="tableData.sort((prev, next) => prev.status - next.status)">
              &uarr;
            </button>
            <button
              @click="tableData.sort((prev, next) => next.status - prev.status)">
              &darr;
            </button>
          </p>
        </th>
        <th>
          <span>Check All</span>
          <br>
          <p class="checkbox" @click="updateTableData">
          <span class="marker" :class="{checked : allChecked}"></span>
        </p>
        </th>
      </tr>
      <template v-for="(row, n) in tableData">
        <Row
        :row="row"
        :n="n"
        :key="n"
        @change-value="changeValue"
        />
      </template>
    </table>
    <div class="button-group">
      <button class="btn btn-green" @click="setStatus(true)">Complited</button>
      <button class="btn btn-red" @click="setStatus(false)">In progress</button>
    </div>
  </div>
</template>

<script>
import Row from './Row.vue';
import tableData from '../table-data';

export default {
  name: 'Table',
  components: {
    Row,
  },

  props: {
    isAuthorized: Boolean,
  },

  data() {
    return {
      tableData,
      allChecked: false,
    };
  },

  methods: {
    sortText(direction) {
      if (direction === 'up') {
        this.tableData.sort((prev, next) => {
          if (prev.name < next.name) return -1;
          if (prev.name > next.name) return 1;
        });
      } else if (direction === 'down') {
        this.tableData.sort((prev, next) => {
          if (prev.name < next.name) return 1;
          if (prev.name > next.name) return -1;
        });
      }
    },

    updateTableData() {
      if (this.allChecked === true) {
        this.allChecked = false;
        this.tableData.forEach((row) => {
          row.isChecked = false;
        });
      } else {
        this.allChecked = true;
        this.tableData.forEach((row) => {
          row.isChecked = true;
        });
      }
    },

    changeValue(n) {
      const newRow = this.tableData[n];

      if (newRow.isChecked === false) {
        newRow.isChecked = true;
        this.tableData.splice(n, 1, newRow);
      } else {
        newRow.isChecked = false;
        this.tableData.splice(n, 1, newRow);
      }
    },

    setStatus(bool) {
      this.tableData.forEach((row) => {
        if (row.isChecked) {
          row.status = bool;
        } else {
          this.errorMessage = 'nothing selected';
        }
      });
    },
  },
};
</script>
<style scoped>
  .btn {
    text-transform: uppercase;
    font-size: 20px;
    padding: 10px 20px;
    border-radius: 3px;
    box-shadow: none;
    border: none;
    margin: 20px;
  }

  .btn-green {
    background-color: rgb(89, 218, 50);
  }

  .btn-red {
    background-color: rgb(252, 65, 65);
  }

  .table-container {
    margin: 0 auto;
  }

  .table {
    margin: 0 auto;
  }

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
