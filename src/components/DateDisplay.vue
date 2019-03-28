<template>
  <div class="card float-left m-1 bg-primary text-white" style="width: 5rem; text-align:center">
    <div>
      <div>
        {{month}}
      </div>
      <div>
        <h2>{{day}}</h2>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'DateDisplay',
  data() {
    return {
      month: '',
      day: new Date().getDate()
    }
  },
  mounted(){
    //get current month and day
    const months = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec']
    this.month = months[new Date().getMonth() + 1];
  }
}
</script>
