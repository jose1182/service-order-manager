<template>
<v-container
  fluid 
  class="spacing-playground pa-6"
>
    <v-stepper v-model="e8">
      <v-stepper-header>
          <v-stepper-step
            :complete="e8 > 1"
            step="1"
          >
            Order
          </v-stepper-step>

          <v-divider></v-divider>

          <v-stepper-step
            :complete="e8 > 2"
            step="2"
          >
            Costumer
          </v-stepper-step>

          <v-divider></v-divider>

          <v-stepper-step
            :complete="e8 > 3"
            step="3"
          >
            Contact
          </v-stepper-step>

          <v-divider></v-divider>

          <v-stepper-step
            :complete="e8 > 4"
            step="4"
          >
            Address
          </v-stepper-step>

          <v-divider></v-divider>

          <v-stepper-step
            :complete="e8 > 5"
            step="5"
          >
            Service
          </v-stepper-step>

          <v-divider></v-divider>

          <v-stepper-step
            :complete="e8 > 6"
            step="6"
          >
            Description
          </v-stepper-step>

          <v-divider></v-divider>


          <v-stepper-step
            :complete="e8 > 7"
            step="7"
          >
            Status
          </v-stepper-step>

          <v-divider></v-divider>

          <v-stepper-step step="8">
            Validation
          </v-stepper-step>
          
      </v-stepper-header>
      <v-stepper-items>
        <v-stepper-content step="1">          
            <v-row class="my-3">
              <v-col
                cols="12"
                md="3"
              >
                <v-text-field
                  v-model="service.order_service"
                  :disabled="isUpdating"
                  dense
                  label="Service order"
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                md="3"
              >

                <v-menu
                  v-model="menu2"
                  :close-on-content-click="false"
                  :nudge-right="40"
                  transition="scale-transition"
                  offset-y
                  min-width="auto"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-text-field
                      v-model="service.issue_date"
                      :disabled="isUpdating"
                      dense
                      label="Issue date"
                      prepend-icon="mdi-calendar"
                      color="blue-grey lighten-2"
                      readonly
                      v-bind="attrs"
                      v-on="on"
                    ></v-text-field>
                  </template>
                  <v-date-picker
                    v-model="service.issue_date"
                    @input="menu2 = false"
                  ></v-date-picker>
                </v-menu>
              </v-col>
              <v-col
                cols="12"
                md="3"
              >
              <v-select
                v-model="service.project"
                :items="projectList"
                dense
                item-text="name"
                item-value="id"
                label="Select Project"
                color="blue-grey lighten-2"
                return-object
                >
              </v-select>
            
              </v-col>
              <v-col
                cols="12"
                md="3"
              >
                <v-text-field
                  v-model="service.order_details.pev"
                  :disabled="isUpdating"
                  dense
                  color="blue-grey lighten-2"
                  label="Pev"
                ></v-text-field>
              </v-col>
            </v-row>          
          <v-btn
            color="primary"
            @click="e8 = 2"
          >
            Continue
          </v-btn>

          <v-btn text>
            Cancel
          </v-btn>
        </v-stepper-content>

        <v-stepper-content step="2">
            <v-row class="my-3"> 
              <v-col
                cols="12"
                md="3"
              >
            <v-autocomplete
              v-model="service.costumer"
              :items="customerList"
              item-text="name"
              item-value="id"
              dense
              label="Contact"
              @change="onChangeFromCustomer"
              return-object
            ></v-autocomplete>

              </v-col>
              <v-col
                cols="12"
                md="3"
              >
            <v-autocomplete
              v-model="service.contact"
              :items="orderContactList"
              item-text="name"
              item-value="id"
              dense
              label="Contact"
              return-object
            ></v-autocomplete>
              </v-col>
              <v-col
                cols="12"
                md="3"
              >
                <v-text-field
                  v-model="service.contact.phone"
                  :disabled="isUpdating"
                  dense
                  color="blue-grey lighten-2"
                  label="Phone"
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                md="3"
              >
                <v-text-field
                  v-model="service.contact.email"
                  :disabled="isUpdating"
                  dense
                  color="blue-grey lighten-2"
                  label="Email"
                ></v-text-field>
              </v-col>
            </v-row>

          <v-btn
            color="primary"
            @click="e8 = 3"
          >
            Continue
          </v-btn>

          <v-btn text>
            Cancel
          </v-btn>
        </v-stepper-content>

        <v-stepper-content step="3">
            <v-row class="my-3">
              <v-col
                cols="12"
                md="3"
              >
            <v-autocomplete
              v-model="service.endCostumer"
              :items="customerList"
              item-text="name"
              item-value="id"
              dense
              label="Contact"
              @change="onChangeEndFromCustomer"
              return-object
            ></v-autocomplete>

              </v-col>
              <v-col
                cols="12"
                md="3"
              >
            <v-autocomplete
              v-model="service.endContact"
              :items="endContactList"
              item-text="name"
              item-value="id"
              dense
              label="Contact"
              return-object
            ></v-autocomplete>
              </v-col>
              <v-col
                cols="12"
                md="3"
              >
                <v-text-field
                  v-model="service.endContact.phone"
                  :disabled="isUpdating"
                  dense
                  color="blue-grey lighten-2"
                  label="Phone"
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                md="3"
              >
                <v-text-field
                  v-model="service.endContact.email"
                  :disabled="true"
                  dense
                  color="blue-grey lighten-2"
                  label="Email"
                ></v-text-field>
              </v-col>
            </v-row>

          <v-btn
            color="primary"
            @click="e8 = 4"
          >
            Continue
          </v-btn>

          <v-btn text>
            Cancel
          </v-btn>
        </v-stepper-content>

        <v-stepper-content step="4">
            <v-row class="my-3">
              <v-col
                cols="12"
                md="5"
              >
                <v-text-field
                  v-model="service.address.street"
                  :disabled="isUpdating"
                  dense
                  color="blue-grey lighten-2"
                  label="Address"
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                md="2"
              >
                <v-text-field
                  v-model="service.address.city"
                  :disabled="isUpdating"
                  dense
                  color="blue-grey lighten-2"
                  label="City"
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                md="2"
              >
                <v-text-field
                  v-model="service.address.zip"
                  :disabled="isUpdating"
                  dense
                  color="blue-grey lighten-2"
                  label="Zip"
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                md="3"
              >
                <v-text-field
                  v-model="service.address.province"
                  :disabled="isUpdating"
                  dense
                  color="blue-grey lighten-2"
                  label="Province"
                ></v-text-field>
              </v-col>
            </v-row>

          <v-btn
            color="primary"
            @click="e8 = 5"
          >
            Continue
          </v-btn>

          <v-btn text>
            Cancel
          </v-btn>
        </v-stepper-content>

        <v-stepper-content step="5">
            <v-row class="my-3">
              <v-col
                cols="12"
                md="2"
              >
                <v-menu
                  v-model="menu3"
                  :close-on-content-click="false"
                  :nudge-right="40"
                  transition="scale-transition"
                  offset-y
                  min-width="auto"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-text-field
                      v-model="service.service_date"
                      :disabled="isUpdating"
                      dense
                      label="Service date"
                      prepend-icon="mdi-calendar"
                      color="blue-grey lighten-2"
                      readonly
                      v-bind="attrs"
                      v-on="on"
                    ></v-text-field>
                  </template>
                  <v-date-picker
                    v-model="service.service_date"
                    @input="menu3 = false"
                  ></v-date-picker>
                </v-menu>
              </v-col>
              <v-col
                cols="12"
                md="2"
              >
                <v-menu
                  ref="menu"
                  v-model="menu4"
                  :close-on-content-click="false"
                  :nudge-right="40"
                  :return-value.sync="service.start_time"
                  transition="scale-transition"
                  offset-y
                  max-width="290px"
                  min-width="290px"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-text-field
                      v-model="service.start_time"
                      label="Start time"
                      prepend-icon="mdi-clock-time-four-outline"
                      dense
                      color="blue-grey lighten-2"
                      readonly
                      v-bind="attrs"
                      v-on="on"
                    ></v-text-field>
                  </template>
                  <v-time-picker
                    v-if="menu4"
                    v-model="time"
                    full-width
                    @click:minute="$refs.menu.save(time)"
                  ></v-time-picker>
                </v-menu>
              </v-col>
              <v-col
                cols="12"
                md="2"
              >
                <v-text-field
                  v-model="service.expected_hours"
                  :disabled="isUpdating"
                  dense
                  color="blue-grey lighten-2"
                  label="Expected hours"
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                md="3"
              >
                <v-autocomplete
                  v-model="service.responsible"
                  :items="allServiceUsers"
                  item-text="name"
                  item-value="id"
                  dense
                  label="Responsible account"
                  return-object
                ></v-autocomplete>
              </v-col>
              <v-col
                cols="12"
                md="3"
              >
            <v-autocomplete
              v-model="service.technician"
              :items="allServiceUsers"
              item-text="name"
              item-value="id"
              dense
              label="Technical"
              return-object
            ></v-autocomplete>
              </v-col>

            </v-row>

          <v-btn
            color="primary"
            @click="e8 = 6"
          >
            Continue
          </v-btn>

          <v-btn text>
            Cancel
          </v-btn>
        </v-stepper-content>

        <v-stepper-content step="6">
            <v-row>
              <v-col
                cols="12"
                md="12"
              >
                <v-textarea
                  v-model="service.description"
                  auto-grow
                  label="Description"
                  rows="4"
                  row-height="30"
                  counter
                ></v-textarea>            
              </v-col>
            </v-row>

          <v-btn
            color="primary"
            @click="e8 = 7"
          >
            Continue
          </v-btn>

          <v-btn text>
            Cancel
          </v-btn>
        </v-stepper-content>

        <v-stepper-content step="7">
            <v-row>
              <v-col
                cols="12"
                md="9"
              >
              <h2 class="text-h6">
                Issues Service
              </h2>
                <v-row>
                  <v-col
                    cols="12"
                  >
                    <v-switch
                      v-model="service.isIncidence"
                      label="Incidence"
                      color="success"
                      hide-details
                    ></v-switch>      
                  </v-col> 
                  <v-col
                    cols="12"
                  >
                    <v-textarea
                        v-model="todo"
                        auto-grow
                        label="Description"
                        rows="4"
                        row-height="36"
                        counter
                          ></v-textarea>        
                  </v-col>             
                </v-row>
              </v-col>
              <v-col
                cols="12"
                md="3"
              >
              <h2 class="text-h6 mb-2">
                Service finished
              </h2>
                <v-row>
                  <v-col
                    cols="12"
                  >
                    <v-switch
                      v-model="service.isFinished"
                      label="Finished"
                      color="success"
                      @change="change(service.isFinished)"
                      hide-details
                    ></v-switch>      
                  </v-col> 
                  <v-col
                    cols="12"
                  >
                    <v-text-field
                      v-model="service.invested_hours"
                      :disabled="isUpdating"
                      filled
                      color="blue-grey lighten-2"
                      label="Invested hours"
                    ></v-text-field>     
                  </v-col>
                  <v-col
                    cols="12"
                  >
                    <v-text-field
                      v-model="service.end_date"
                      :disabled="isUpdating"
                      filled
                      color="blue-grey lighten-2"
                      label="End date"
                    ></v-text-field>     
                  </v-col>               
                </v-row>
              </v-col>
            </v-row>

          <v-btn
            color="primary"
            @click="e8 = 8"
          >
            Continue
          </v-btn>

          <v-btn text>
            Cancel
          </v-btn>
        </v-stepper-content>   

        <v-stepper-content step="8">
            <v-row class="my-3">
              <v-col
                cols="12"
                md="4"
              >
                <v-checkbox
                  v-model="service.isCheckedByTechnician"
                  label="Technician ST"
                  color="success"
                  hide-details
                ></v-checkbox>
              </v-col>
              <v-col
                cols="12"
                md="4"
              >
                <v-checkbox
                  v-model="service.isCheckedByCoordinator"
                  label="Coordinator ST"
                  color="success"
                  hide-details
                ></v-checkbox>
              </v-col>
              <v-col
                cols="12"
                md="4"
              >
                <v-checkbox
                  v-model="service.isCheckedByAccount"
                  label="Responsible account"
                  color="success"
                  hide-details
                ></v-checkbox>
              </v-col>
            </v-row>
          <v-btn
            color="primary"
            @click="e8 = 1"
          >
            Continue
          </v-btn>

          <v-btn text>
            Cancel
          </v-btn>
        </v-stepper-content>           
      </v-stepper-items>
    </v-stepper>

  <v-card-actions >
        <v-col
          cols="12"
          class="text-right"
        >
          <v-btn color="success" @click="changeService">UPDATE SERVICE</v-btn>
        </v-col>
  
  </v-card-actions>
      

    <v-container 
      v-if="!enabled"
      fill-height fluid>
      <v-row align="center"
          justify="center"
        >
        <v-progress-circular
          size="50"
          indeterminate
          color="primary"
        ></v-progress-circular>
      </v-row>
    </v-container>
</v-container>
</template>
<script>

  import {mapActions, mapGetters} from 'vuex'

  export default {
    data () {
      return {
        autoUpdate: true,
        isUpdating: false,
        date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
        modal: false,
        menu2: false,
        menu3: false,
        menu4:false,
        time: null,
        customerSelected:null,
        enabled: false,
        service:{
            id:'',
            order_service: '',
            issue_date:'',
            order_details:'',
            project: {
              'id': null,
              'name': ''
            },
            costumer:'',
            contact:{
              id:'',
              name:'',
              phone:'',
              email:''
            },
            endCostumer:{
              id:'',
              code:'',
              name:'',
              phone:''
            },
            endContact:{
              id:'',
              name:'',
              phone:'',
              email:''
            },
            user:'',
            technician:'',
            responsible:'',
            address:{
              city: '',
              customer_id: '',
              id: '',
              province: '',
              street: '',
              zip: ''

            },
            service_date:'',
            start_time:'',
            expected_hours:'',
            description:'',
            isIncidence:'',
            isFinished:'',
            invested_hours:'',
            end_date:'',
            isCheckedByTechnician:'',
            isCheckedByCoordinator:'',
            isCheckedByAccount:'',          
        },
        e8: 1,
        todo : 'not incluede in db'
      }
    },
    
    props:['serviceId'],

    created(){
      this.getUsers();
      this.projects();
      this.costumers();
      this.getServiceDetail(this.serviceId).then(()=>{
        this.service.id = this.serviceDetails.id;
        this.service.order_service =  this.serviceDetails.order_service;
        this.service.issue_date = this.serviceDetails.issue_date;
        this.service.costumer = this.serviceDetails.costumer;
        this.service.order_details = this.serviceDetails.order_details;
        this.service.project = this.serviceDetails.project;
        this.service.address = this.serviceDetails.address? this.serviceDetails.address: this.service.address;
        this.service.start_time =  this.serviceDetails.start_time;
        this.service.expected_hours = this.serviceDetails.expected_hours;
        this.service.responsible = this.serviceDetails.responsible;
        this.service.technician = this.serviceDetails.technician;
        this.service.description =  this.serviceDetails.description;
        this.service.isFinished = this.serviceDetails.isFinished;
        this.service.isCheckedByTechnician = this.serviceDetails.isCheckedByTechnician;
        this.service.isCheckedByCoordinator = this.serviceDetails.isCheckedByCoordinator;
        this.service.isCheckedByAccount = this.serviceDetails.isCheckedByAccount;
        this.service.invested_hours = this.serviceDetails.invested_hours;
        this.service.end_date = this.serviceDetails.end_date;
        this.service.isIncidence = this.serviceDetails.isIncidence;
        this.service.service_date = this.serviceDetails.service_date;


        if(this.service.costumer.id){

          this.contacts(this.service.costumer.id)

          if(this.serviceDetails.contact){
            this.service.contact = this.serviceDetails.contact;
          }
        }        

        if(this.serviceDetails.endCostumer){
          this.service.endCostumer = this.serviceDetails.endCostumer
        }
        
        if(this.serviceDetails.endContact){
          this.endContacts(this.serviceDetails.endContact.costumer_id)
          this.service.endContact = this.serviceDetails.endContact;
        }
      }).finally(()=>{
        this.enabled=true
      })
/*         this.costumers().then(()=>{
          this.contacts(this.serviceDetails.costumer.id).then(()=>{
            this.costumerById(this.serviceDetails.contacting.customer_id).then(()=>{
              this.customerSelected = this.endCustomer
            }).then(()=>{
              this.endContacts(this.serviceDetails.contacting.customer_id).finally(()=>(this.enabled=true))              
            })
          })
        })  */
     
    },


    computed: {
      ...mapGetters({
        serviceDetails: 'application/serviceDetails',
        allNotifications: 'application/notifications',
        projectList: 'application/projectList',
        customerList: 'application/customers',
        endCustomer: 'application/endCustomer',
        orderContactList:'application/orderContactList',
        endContactList:'application/endContactList',
        allServiceUsers: 'user/allServiceUsers',
      }),
    },
    watch: {
      isUpdating (val) {
        if (val) {
          setTimeout(() => (this.isUpdating = false), 3000)
        }
      }

    },

    methods: {
      ...mapActions({
        getServiceDetail:'application/getServiceDetail',
        addNotification: 'application/addNotification',
        projects: 'application/getProjects',
        costumers: 'application/getCustomers',
        costumerById: 'application/getCostumerById',
        contacts: 'application/getContactsByCostumer',
        endContacts: 'application/getEndContactsByCostumer',
        getUsers: 'user/ListUsers',
        updateServiceDetails: 'application/updateServiceDetails',
      }),

      remove (item) {
        const index = this.friends.indexOf(item.name)
        if (index >= 0) this.friends.splice(index, 1)
      },

      onChangeFromCustomer(item){
          this.contacts(item.id).then(()=>{
            this.service.contact = {
              costumer_id: null,
              email: '',
              id: null,
              name: '',
              phone: ''
            }
          })
      },

      onChangeEndFromCustomer(item){
          this.endContacts(item.id).then(()=>{
            this.service.endContact = {
              customer_id: null,
              email: '',
              id: null,
              name: '',
              phone: ''              
            }
          })
      },

      changeService(){

        //Check validate form
        this.updateServiceDetails(this.service)
        .then(()=>{
          this.addNotification({
              text: 'Service details Change!',
              show: true
          })
        })
        .catch(()=>{
          this.addNotification({
              text: 'Fail to chnage details service!',
              show: true
          })
        })
      },

      beforeRouteUpdate(to, from, next){
          //this.getService(to.params.serviceId).then(()=>{

            next();
         // })

      },     

      change(newValue){
          this.service.end_date = null;
          if(newValue){
            this.service.end_date = (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10);
          }
      }
    }
  }
</script>
<style scoped>
.v-progress-circular {
  margin: 1rem;
}
</style>