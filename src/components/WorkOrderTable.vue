<template>
  <div>
    <b-table
      ref="WorkOrderTable"
      striped hover
      id="workOrdersTable"
      :items="workorders"
      :fields="fields"
      :per-page="perPage"
      :current-page="currentPage">
      <template>
        <div class="fa fa-eye text-primary"></div>
      </template>
      <template slot="priority" slot-scope="data">
        <span class="fa fa-star text-warning" v-if="data.value"></span>
      </template>
    </b-table>
    <b-pagination
      v-model="currentPage"
      :total-rows="rows"
      :per-page="perPage"
      aria-controls="workOrdersTable"
      align="center"
    />
    <b-alert v-model="errorAlert" variant="danger">
      {{alertMessage}}
    </b-alert>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'WorkOrderTable',
  mounted()
  {
    //get current orders
    axios.get("http://localhost:3000/workorders")
    .then((response)  =>  {
      this.workorders = response.data;
      this.rows = this.workorders.length;
    }, (error)  =>  {
      this.errorAlert = true;
      this.alertMessage = error;
    })
  },
  data() {
    return {
      fields:[
        {
          key: 'coffee',
          sortable: true,
        },
        {
          key: 'method',
          sortable: true,
        },
        {
          key: 'number_of_cases',
          sortable: true
        },
        {
          key: 'packets_per_case',
          sortable: true
        },
        {
          key: 'ship_date',
          sortable: true,
          formatter: (value) => {
            var shipDate = new Date(value);
            return shipDate.getMonth() + 1 + '/' + shipDate.getDate() + '/' + shipDate.getFullYear();
          }
        },
        {
          key: 'priority',
          sortable:true
        },
        {
          key: 'order_number',
          sortable: true,
          formatter: (value) => {
            return '#' + value;
          }
        },
        {
          key: 'view',
          sortable: false
        }
      ],
      perPage: 6,
      currentPage: 1,
      workorders: [],
      rows: 0,
      alertMessage:'',
      errorAlert:false
    }
  }
}
</script>
