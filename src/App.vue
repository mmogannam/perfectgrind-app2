<template>
  <div class="overflow-auto container-fluid">
    <DateDisplay/>
    <div class="h1 float-left m-3">Perfectly Ground Work Orders</div>
    <b-button @click="showModal" variant="primary" class="float-right m-4">Create Order</b-button>
    <WorkOrderTable />
    <WorkOrderModal ref="WorkOrderModal"/>
  </div>
</template>

<script>
  import WorkOrderModal from './components/WorkOrderModal.vue';
  import WorkOrderTable from './components/WorkOrderTable.vue';
  import DateDisplay from './components/DateDisplay.vue';

  export default {
    methods:{
      showModal(){
        this.$refs.WorkOrderModal.$refs.WorkOrderModal.show();
      }
    },
    components: {
      WorkOrderTable,
      WorkOrderModal,
      DateDisplay
    }
  }
</script>
