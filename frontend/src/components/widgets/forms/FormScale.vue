<template>
	<div>
   <v-row>
    <v-col 
      cols="2" 
      xl="1" 
      lg="1" 
      md="1" 
      sm="1">
      <v-select 
        :items="min"
        :label="selectedMin">
      </v-select>
    </v-col>
    <v-col 
      cols="2" 
      xl="1" 
      lg="1" 
      md="1" 
      sm="1">
      <div class="to">to</div>
    </v-col>
    <v-col 
      cols="2"
      xl="1" 
      lg="1" 
      md="1" 
      sm="1">
      <v-select 
        :items="max"
        :label="selectedMax">
      </v-select>
    </v-col>
   </v-row>
   <v-row>
    <v-col cols="8" xl="3" lg="3" md="3" sm="3">
      <v-text-field 
        :color="themeColor"
        placeholder="Label (optional)">
      </v-text-field>
    </v-col>
   </v-row>
   <v-row>
    <v-col cols="8" xl="3" lg="3" md="3" sm="3">
      <v-text-field 
        :color="themeColor"
        placeholder="Label (optional)">
      </v-text-field>
    </v-col>
   </v-row>
  </div>
</template>

<script>
	export default {
    props: ["themeColor"],
    data() {
      return {
        selectedMin: "1",
        selectedMax: "5",
        min: [
          '0',
          '1',
        ],
        max: [
          '2',
          '3',
          '4',
          '5',
          '6',
          '7',
          '8',
          '9',
          '10',
        ]
      }
    }
  }
</script>

<style scoped>
  .to {
    position: relative; 
    padding-top: 20px;
  }
</style>
