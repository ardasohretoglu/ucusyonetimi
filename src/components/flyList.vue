<template>
    <v-container>
        <v-row>

            <v-col cols="12">
                <v-chip
                    color="red"
                    label
                    dark
                    block
                    >
                    UÇUŞ
                    </v-chip>
                    <h4 class="mt-5">
                        {{selectedCties[0].originAirport.toUpperCase()}} - {{selectedCties[1].destinationAirport.toUpperCase()}}
                    </h4>

                    
            </v-col>
            <v-col cols="3">
                <v-switch
                        id="promotion"
                        v-model="isPromotion"
                        inset
                        label="Promosyon Kodu"
                        ></v-switch>
            </v-col>

            <v-col cols="12">
                <v-card 
                        class="pb-5"
                    >
                <v-system-bar
                    class="py-6"
                    style="background-color:#063048;"
                    dark
                    height="30px"
                    >
                    <v-spacer></v-spacer>
                        
                        <h5 class="mt-1">
                            SIRALAMA KRİTERİ
                        </h5>

                        <v-btn @click="sortForPrice()" outlined text tile elevation="0" class="mx-5"> Ekonomi Ücreti </v-btn>
                        <v-btn @click="sortForDate()" outlined text tile elevation="0"> Kalkış Saati </v-btn>
                        
                    </v-system-bar>
                    <v-row v-for="(flight , index) in flights" :key="index">
                        <v-col cols="8" >
                        <v-card
                            class="ma-5"
                        >
                        
                        <v-row class="ma-2" >
                            <v-col cols="9">
                                <v-row>
                                    <v-col cols="11" class="pb-0">

                                    
                                    <div class="times pr-6">
                                        <span>
                                            {{flight.arrivalDateTimeDisplay}}
                                        </span>
                                        <span>
                                            {{flight.departureDateTimeDisplay}}
                                        </span>
                                    </div>
                                    </v-col>
                                    <v-col cols="3" class="info-color">
                                        <div>
                                            {{flight.originAirport.city.code}}
                                        </div>
                                        <div>
                                            {{flight.originAirport.city.name}}
                                        </div>
                                    </v-col>
                                    <v-col cols="6">
                                        <v-divider></v-divider>
                                    </v-col>
                                    <v-col cols="3" class="info-color">
                                        <div>
                                            {{flight.destinationAirport.city.code}}
                                        </div>
                                        <div>
                                            {{flight.destinationAirport.city.name}}
                                        </div>
                                    </v-col>
                                    
                                
                                </v-row>
                            </v-col>
                            <v-col cols="3" class="fly-duration ">
                                <div class="pt-7">
                                    <h4>
                                        Uçüş Süresi
                                    </h4>
                                    <p>
                                        {{flight.flightDuration}}
                                    </p>
                                </div>
                            </v-col>

                        </v-row>
                        
                        </v-card>
                          </v-col>
                          <v-col cols="2" class="px-0"> 
                              <v-card class="ma-5" height="116"  >
                                  <v-row class="ma-2 pt-6">
                                      <v-col cols="5" class="pa-0">
                                  <v-checkbox
                                        v-model="selectedFly"
                                        :value="{name:'Economy',index:index}"
                                        label="Economy"
                                    ></v-checkbox>
                                    </v-col>
                                    <v-col cols="5" class="pa-0 text-center mt-2">
                                        <h5>
                                          Yolcu Başına
                                      </h5>
                                      {{flight.fareCategories.ECONOMY.subcategories[0].price.currency}}
                                      {{ isPromotion == true ? flight.fareCategories.ECONOMY.subcategories[0].price.amount/ 2 : 
                                      flight.fareCategories.ECONOMY.subcategories[0].price.amount}}
                                    
                                    </v-col>
                                    <v-col cols="2" class="pa-0">
                                        <v-btn x-small elevation="0"  text
                                                fab
                                                @click="setEconomy(index)"
                                                class="mt-4"
                                                >
                                                <v-icon
                                            
                                        >
                                            mdi-chevron-down 
                                        </v-icon>
                                                </v-btn>
                                        
                                    </v-col>
                                  </v-row>
                              </v-card>
                          </v-col>
                          <v-col cols="2" class="px-0" >
                              <v-card class="ma-5" height="116" >
                                  <v-row class="ma-2 pt-6">
                                      <v-col cols="5" class="pa-0">
                                  <v-checkbox
                                        v-model="selectedFly"
                                        :value="{name:'Business',index:index}"
                                        label="Business"
                                    ></v-checkbox>
                                    </v-col>
                                    <v-col cols="5" class="pa-0 text-center mt-2">
                                        <h5>
                                          Yolcu Başına
                                      </h5>
                                      {{flight.fareCategories.BUSINESS.subcategories[0].price.currency}}
                                      {{ isPromotion == true ? flight.fareCategories.BUSINESS.subcategories[0].price.amount / 2 : 
                                      flight.fareCategories.BUSINESS.subcategories[0].price.amount}}
                                    </v-col>
                                     <v-col cols="2" class="pa-0">
                                        <v-btn x-small elevation="0" text
                                                fab
                                                @click="setBusiness(index)"
                                                class="mt-4"
                                                >
                                                <v-icon
                                            
                                            >
                                                mdi-chevron-down 
                                            </v-icon>
                                        </v-btn>
                                    </v-col>
                                  </v-row>
                              </v-card>
                          </v-col>

                          <v-col cols="12" v-if="(selectedFly) && (index == selectedFly.index)">
                              <v-card  class="ma-5">
                                    <v-row>
                                        <v-col cols="4" v-for="(category , index) in 
                                         selectedFly.name == 'Economy' ?
                                         flight.fareCategories.ECONOMY.subcategories :
                                         flight.fareCategories.BUSINESS.subcategories
                                         
                                         " 
                                        
                                        :key="index">
                                            <v-card
                                                class="ml-3"
                                            >
                                            

                                                    <v-card-title style="background-color:#f5f5f5; display:flex; justify-content:space-between; ">
                                                        <h5>
                                                            {{category.brandCode}}

                                                        </h5>
                                                        <div>
                                                            <span style="font-size:small;font-weight: 400;" >
                                                                {{category.price.currency}}
                                                            </span>
                                                            <span>
                                                                {{isPromotion == true ? category.price.amount / 2 : category.price.amount}}
                                                            </span>
                                                        </div>
                                                        </v-card-title>

                                                <v-card-text class="text--primary" style="height:250px">
                                                 <v-list >
                                                            <template>

                                                                <v-list-item v-for="(right, index) in category.rights" :key="right[index]" style="border-bottom: solid 1px black">
                                                                    <v-list-item-title  > 
                                                                        {{right}}    
                                                                     </v-list-item-title>
                                                                    
                                                                </v-list-item>
                                                                
                                                            </template>
                                                        </v-list>
                                                </v-card-text>

                                                <v-card-actions class="pa-0">
                                                <v-btn
                                                    tile
                                                    color="red"
                                                    elevation="0"
                                                    dark
                                                    block
                                                    :disabled="isPromotion && category.brandCode !== 'ecoFly'"
                                                    @click="pushStatusPage(category)"
                                                >
                                                    UÇUŞU SEÇ
                                                </v-btn>

                                                </v-card-actions>
                                            </v-card>
                                        </v-col>
                                    </v-row>
                              </v-card>
                          </v-col>
                    </v-row>
                    </v-card>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
import flight from '../../data/flights.json'


export default {
    name:'FlyList',
    

    data: () =>({
        isPromotion:false,
        selectedCties:[],
        originAirport:'',
        destinationAirport:'',
        flights : flight.flights,
        categoryName: 'ECONOMY',
        openFlyList:false,
        selectedFly:'',
    }),

    methods:{
        setEconomy(index){
            this.selectedFly={name:'Economy',index:index}
        },
        setBusiness(index){
            this.selectedFly={name:'Business',index:index}
        },
        pushStatusPage(category){
            const categoryBearer = {
                status: category.status,
                price : {
                    amount : category.price.amount,
                    currency : category.price.currency
                }
            }
            if(this.isPromotion == true){
                categoryBearer.price.amount = categoryBearer.price.amount / 2
                localStorage.setItem('status', JSON.stringify(categoryBearer));
                this.$router.push({ name: "StatusPage" });
                return
            }else{
                localStorage.setItem('status', JSON.stringify(categoryBearer));
                this.$router.push({ name: "StatusPage" });
            }
            
        },
        sortForPrice(){
                this.flights = this.flights.sort((item1,item2) => {
                    return item1.fareCategories.ECONOMY.subcategories[0].price.amount - item2.fareCategories.ECONOMY.subcategories[0].price.amount
                })
        },
        sortForDate(){
            this.flights = this.flights.sort((item1,item2) => {
                    return new Date(`July 20, 2021 ${item1.arrivalDateTimeDisplay}:00 `) - new Date(`July 20, 2021 ${item2.arrivalDateTimeDisplay}:00 `)
                })
        }
    },

    watch:{
        
        
        
    },

    created(){
        this.selectedCties = JSON.parse(localStorage.getItem("selectedCities"))
        
    },
    
}
</script>
<style scoped>
.times{
    display: flex;
    justify-content: space-between;
}
.info-color{
    color: rgb(114, 114, 114);
}
.fly-duration{
    display: flex;
    justify-content: center;
    align-items: center;
}



</style>