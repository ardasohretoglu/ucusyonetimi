<template>
  <v-container>
    <v-row style="height:500px">
      <v-col cols="12" style="display:flex;justify-content:center;align-items:center" >
        
        <div class="form">
          <v-text-field
            label="Nereden"
            solo
            elevation="0"
            class="ma-1"
            prepend-inner-icon="mdi-airplane-takeoff"
            v-model="takeOff"
          ></v-text-field>
          <v-text-field
            class="ma-1"
            label="Nereye"
            solo
            elevation="0"
            prepend-inner-icon="mdi-airplane-landing"
            v-model="landing"
          ></v-text-field>
          
          <button class="form-buttons ml-5">

            <span class="ml-3">
              Tarih
            </span>
            <v-icon
              dark
              right
              large
              class="mr-3"
            >
              mdi-calendar-range 
            </v-icon>
          </button>

          <!-- MENU START -->
           <div class="text-center">
              <v-menu
                :close-on-content-click="false"
                :nudge-width="200"
                offset-y
                rounded
              >
                <template v-slot:activator="{ on, attrs }">
                  

                  <button v-bind="attrs" 
                    v-on="on" class="form-buttons select-button ml-5">
                    <v-icon
                      dark
                      right
                      class="mr-3"
                    >
                      {{ (selectCount == 0 || selectCount == 1) ? 'mdi-human-male ' : 'mdi-human-male-male ' }}  
                    </v-icon>
                    <span class="selected-count" >
                      {{selectCount}}
                    </span>
                      
                      
                  </button>

                </template>

                <v-card style="padding:20px">
                 
                      

                        <h5 style="color:#787878">
                          Kabin ve yolcu seçimi
                        </h5>

                  
                  <v-list>
                     <v-radio-group
                        v-model="selectedClass"
                        row
                      >
                        <v-radio
                          label="Econommy Class"
                          value="econommyClass"
                        ></v-radio>
                        <v-radio
                          label="First Class"
                          value="firstClass"
                        ></v-radio>
                      </v-radio-group>
                  </v-list>

                  <v-card-actions style="display: flex; justify-content: space-between;" >
                    <div>
                      <h4>Yolcu : </h4>
                    </div>
                    <div style="display:flex">
                      <v-btn
                        class="mx-2"
                        tile
                        x-small
                        dark
                        fab
                        color="grey"
                        @click="selectCount != 0 ? --selectCount : selectCount"
                      >
                        <v-icon dark>
                          mdi-minus
                        </v-icon>
                      </v-btn>
                      <div class="mx-5">
                        {{selectCount}}
                      </div>
                      <v-btn
                        class="mx-2"
                        tile
                        x-small
                        dark
                        fab
                        color="grey"
                        @click="++selectCount"
                      >
                        <v-icon dark>
                          mdi-plus
                        </v-icon>
                      </v-btn>
                      </div>
                  </v-card-actions>
                </v-card>
              </v-menu>
            </div>
            <!-- MENU END -->

            <!-- <button class="ml-5 form-buttons"
              @click="toListPage"
             :disabled="!validChoiceTakeOff || !validChoicelanding"
              style="background-color: #E81932 !important;">
              
                        <v-icon
                          dark
                          right
                          large
                          class="ma-1"
                        >
                          mdi-chevron-right 
                        </v-icon>
                      </button> -->
                      <v-btn elevation="0"
                        class="ml-3 mt-1"
                        height="48"
                       style="background-color: #E81932 !important;"
                        :disabled="!validChoiceTakeOff || !validChoicelanding"
                         @click="toListPage" 
                         fab 
                         tile
                         >
                        <v-icon
                        
                          color="#FFFF"
                          right
                          large
                          class="ma-1"
                        >
                          mdi-chevron-right 
                        </v-icon>
                      </v-btn>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import flight from '../../data/flights.json'
  export default {
    name: 'FlySearching',

    data: () => ({
     selectCount:0,
     selectedClass:'econommyClass',
     takeOff:'',
     landing:'',
     flight : flight.flights,
     validChoiceTakeOff : false,
     validChoicelanding : false,

     selectedCities: []
    }),

    methods:{
      toListPage(){
        this.$router.push({ name: "ListPage" });
        this.selectedCities = []

        this.selectedCities = [
          {
            originAirport: this.takeOff
          },
          {
            destinationAirport: this.landing
          }
        ]
        localStorage.setItem('selectedCities', JSON.stringify(this.selectedCities));
      }
    },

    watch:{
      takeOff:{
        handler(val){
          this.validChoiceTakeOff = this.flight.some(item => {
            return item.originAirport.city.name.toUpperCase() == val.toUpperCase()
          })
        }
      },
      landing:{
        handler(val){
          this.validChoicelanding = this.flight.some(item => {
            return item.destinationAirport.city.name.toUpperCase() == val.toUpperCase()
          })
        }
      }
    },

    mounted(){
      // this.flight = JSON.parse(this.flight.flights)
    }

  }
</script>
<style scoped>
.form{
  background-color: rgb(96 105 119 / 60%);
  padding: 15px;
  display: flex;
}
.form-buttons{
  background-color: #01245c;
  display: flex;
  align-items: center;
  color: #ffff;
  height: 50px;
  padding: 1px;
  margin-top: 3px;
}
.form-buttons:hover{
  background-color: #01245c88;
}

.select-button{
  width: 90px;
  display: block !important;

}
.selected-count{
    position: relative;
    left: 0px;
    top: -10px;
}
</style>