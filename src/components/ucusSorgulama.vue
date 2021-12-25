<template>
  <v-container>
    <v-row style="height:500px">
      <v-col cols="12" style="display:flex;justify-content:center;align-items:center" >
        
        <div class="form">
          <v-text-field
            label="Outlined"
            solo
            elevation="0"
            class="ma-1"
          ></v-text-field>
          <v-text-field
          class="ma-1"
            label="Outlined"
            solo
            elevation="0"
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
                v-model="menu"
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
                      mdi-human-male  
                    </v-icon>
                    <span class="selected-count" >
                      {{selectCount}}
                    </span>
                      
                      
                  </button>

                </template>

                <v-card style="padding:20px">
                  <v-list>
                    <v-list-item>
                      

                      <v-list-item-content>
                        <h5 style="color:#787878">
                          Kabin ve yolcu seçimi
                        </h5>
                      </v-list-item-content>

                    </v-list-item>
                  </v-list>
                  
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
        </div>

      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'UcusSorgulama',

    data: () => ({
     selectCount:0,
     selectedClass:'econommyClass'
    }),
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
.form-buttons-disabled{
  background-color: #686868;
  display: flex;
  align-items: center;
  color: #ffff;
  height: 50px;
  padding: 1px;
  margin-top: 3px;
  cursor: auto;
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