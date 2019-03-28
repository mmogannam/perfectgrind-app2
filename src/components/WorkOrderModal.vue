<template>
  <div>
    <b-modal ref="WorkOrderModal" size="lg" hide-footer title="Perfectly Ground Work Order">
      <div class="d-block">
        <b-form>
          <b-container class="bv-example-row">
            <b-row>
              <b-col>
                <b-form-group id="modalInputGroup1" label="Coffee" label-for="coffee">
                  <b-form-select id="coffee" v-model="form.coffee_id" :options="coffeeOptions" size="sm" />
                </b-form-group>
              </b-col>
              <b-col>
                <b-form-group id="modalInputGroup2" label="Method" label-for="method">
                  <b-form-select v-model="form.method_id" :options="methodOptions" size="sm"  />
                </b-form-group>
              </b-col>
            </b-row>
            <b-row>
              <b-col>
                <b-form-group id="modalInputGroup5" label="Ship Date" label-size="sm" label-for="ship_date">
                  <b-form-input id="ship_date" type="date" v-model="form.ship_date" />
                </b-form-group>
              </b-col>
              <b-col>
                <b-form-group id="modalInputGroup3" label="Number Of Cases" label-size="sm" label-for="number_of_cases">
                  <b-form-select id="number_of_cases" v-model="form.number_of_cases" :options="numberOfCasesOptions" size="sm" />
                </b-form-group>
              </b-col>
              <b-col>
                <b-form-group id="modalInputGroup4" label="Packets Per Case" label-size="sm" label-for="packets_per_case">
                  <b-form-select id="packets_per_case" v-model="form.packets_per_case" :options="packetsPerCaseOptions" size="sm" />
                </b-form-group>
              </b-col>
            </b-row>
            <b-row>
              <b-col>
                <b-form-group id="modalInputGroup6" label="Notes" label-for="notes">
                  <b-form-textarea
                    id="notes"
                    v-model="form.notes"
                    rows="3"
                    max-rows="6"/>
                </b-form-group>
              </b-col>
            </b-row>
            <b-row>
              <b-col>
                <b-form-checkbox
                  id="priority"
                  v-model="form.priority"
                  value="true"
                  unchecked-value="false">
                  Priority
                </b-form-checkbox>
              </b-col>
            </b-row>
          </b-container>
      </b-form>
      </div>
      <b-button class="mt-2 float-right ml-2" variant="secondary" @click="closeModal">Cancel</b-button>
      <b-button class="mt-2 float-right" variant="primary" @click="saveModal">Create Work Order</b-button>
    </b-modal>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'WorkOrderModal',
  methods:{
    closeModal(){
      this.$refs.WorkOrderModal.hide();
    },
    saveModal(){
      axios.post('http://localhost:3000/workorders', this.form)
      .then(()  =>  {
        location.reload(true);
      }, (error)  =>  {
        this.errorAlert = true;
        this.alertMessage = error;
      })
    }
  },
  data() {
    return {
      form:{
        coffee_id:null,
        method_id:null,
        number_of_cases:null,
        packets_per_case:null,
        notes:'',
        ship_date:null,
        priority:false
      },
      coffeeOptions: [
            { value: 1, text: 'Bella Donovan' },
            { value: 2, text: 'Giant Steps' },
      ],
      methodOptions: [
            { value: 1, text: 'Aeropress' },
            { value: 2, text: 'Coffee Maker' },
            { value: 3, text: 'Cold Brew' },
            { value: 4, text: 'French Press' },
            { value: 5, text: 'Pour Over' }
      ],
      numberOfCasesOptions: [
            { value: 1, text: '1' },
            { value: 2, text: '2' },
            { value: 3, text: '3' },
            { value: 4, text: '4' },
            { value: 5, text: '5' },
            { value: 6, text: '6' },
            { value: 7, text: '7' },
            { value: 8, text: '8' },
            { value: 9, text: '9' },
            { value: 10, text: '10' }
      ],
      packetsPerCaseOptions: [
            { value: 25, text: '25' },
            { value: 50, text: '50' }
      ],
    }
  }
}
</script>
