<template>
     <v-container>
        <v-row>
            <v-col cols="12" >
                    
                    <div class="justify-center">
                        <v-btn
                                class="ma-2"
                                fab
                                small
                                elevation="0"
                                :color="items.status == 'AVAILABLE' ? 'green' : 'red' "
                            >
                                <v-icon
                                                color="white"
                                                >
                                                    {{items.status == 'AVAILABLE' ? 'mdi-check' : 'mdi-close-octagon-outline '}} 
                                                </v-icon>
                            </v-btn>
                            <h3 class="ml-3">
                                {{items.status == 'AVAILABLE' ? 'Kabin Seçimini Tamamladınız' : 'Kabin Seçiminiz Tamamlanamadı'}} 
                                
                            </h3>
                    </div>
                    <v-divider class="my-5"></v-divider>
                        <div class="justify-space-between" v-if="items.status === 'AVAILABLE' ">
                            <h3>
                                Toplam Tutar
                            </h3>
                            <h3 style="color:#1976d2">
                                {{items.price.currency}} {{items.price.amount}}
                            </h3>
                        </div>
                        <div class="justify-end" v-else>
                            <v-btn @click="returnStartingPage()">
                                Başa Dön
                            </v-btn>
                        </div>

            </v-col>
        </v-row>
     </v-container>
</template>
<script>
export default {
    
    data:()=>({
        items:''
    }),

    methods:{
        returnStartingPage(){
            this.$router.push({ name: "Home" });
            localStorage.clear();
        }
    },

    created(){
        this.items = JSON.parse(localStorage.getItem("status"))
        
    },

}
</script>
<style scoped>
.justify-center{
    display:flex;
    justify-content:center;
    align-items:center
}
.justify-space-between{
    display:flex;
    justify-content:space-between;
    align-items:center
}
.justify-end{
    display:flex;
    justify-content:flex-end;
    align-items:center
}
</style>