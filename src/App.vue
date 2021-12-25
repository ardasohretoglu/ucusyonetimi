<template>
  <v-app>
    
    <v-main class="app-background">
       <v-container>
    <v-row >
      <v-col cols="12" style="color:#FFFFFF">
        
        <div class="page-header">
          <div>
            <h4>turkishairlines.com</h4>
          </div>
          <div>
            <span class="search">
              Search
            </span>
          <h4 class="display">
            Flight Challenge

          </h4>
          </div>
        </div>

      </v-col>
    </v-row>
  </v-container>
        
        

      
      
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    
  }),
};
</script>

<style scoped>
.app-background{
  background-color: #063048;
}
.page-header{
  display: flex;
  justify-content: space-between;
  border-bottom: solid 1px;
}
.display{
  display: inline;
}
.search{
  font-size: smaller;

}
</style>
