<template>
  <v-app>
    <v-main  :style="currentRouteName == 'Home' ? 'background-color: #063048;' : 'background-color: #FFFF;' ">
       <v-container>
    <v-row >
      <v-col cols="12" :style="currentRouteName == 'Home' ? 'color: #FFFFFF;' : 'color: #000000;' " >
        
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

  computed: {
    currentRouteName() {
        return this.$route.name;
    }
}

};
</script>

<style scoped>
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
