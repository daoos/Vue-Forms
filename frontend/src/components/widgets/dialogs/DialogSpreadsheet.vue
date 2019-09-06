<template>
	<v-dialog
    max-width="600px"
    v-model="dialog"
    :fullscreen="$viewport.width < 450">
    <template v-slot:activator="{ on: dialog }">
      <v-tooltip left>
        <template v-slot:activator="{ on: tooltip }">
          <v-btn
            icon
            v-on="{ ...tooltip, ...dialog }">
            <v-icon color="green darken-1">mdi-google-spreadsheet</v-icon>
          </v-btn>
        </template>
        <span class="tooltip">Create Spreadsheet</span>
      </v-tooltip>
    </template>
    <v-card tile>
      <v-card-title v-bind:style="{ backgroundColor: themeColorList[themeColor] }">
        <span class="headline font-weight-medium dialog-title">Select response destination</span>
        <div class="flex-grow-1"></div>
        <v-btn 
          icon
          @click="dialog = false">
          <v-icon color="white">mdi-close</v-icon>
        </v-btn>
      </v-card-title>
      <v-card-text class="text--primary">
        <v-row>
          <v-col 
            cols="12" 
            xl="6" 
            lg="6" 
            md="6" 
            sm="6">
            <v-radio-group v-model="active">
              <v-radio 
                label="Create a new spreadsheet"
                :value="true"
                :color="themeColor">
              </v-radio>
              <v-radio 
                label="Select existing spreadsheet"
                :value="false"
                :color="themeColor">
              </v-radio>
            </v-radio-group>
          </v-col>
          <v-col 
            cols="8" 
            xl="4" 
            lg="4" 
            md="4" 
            sm="4">
            <v-text-field
              :color="themeColor"
              value="Untitle form (Reponses)">
            </v-text-field>
          </v-col>
          <v-col 
            cols="4" 
            xl="2" 
            lg="2" 
            md="2" 
            sm="2">
            <div class="link-container">
              <a href="">Learn more</a>
            </div>
          </v-col>
        </v-row>
      </v-card-text>
      <v-card-actions>
        <div class="flex-grow-1"></div>
        <v-btn 
          text
          @click="dialog = false">CANCEL</v-btn>
        <v-btn 
          :color="themeColor" 
          text
          @click="dialog = false">{{ active ? 'CRAETE' : 'SELECT' }}</v-btn>
      </v-card-actions> 
    </v-card>
  </v-dialog>
</template>

<script>
  export default {
    props: ["themeColor"],
    data() {
      return {
        dialog: false,
        active: true,
        themeColorList: {
          'red darken-1': '#E53935',
          'deep-purple darken-1': '#5E35B1',
          'indigo darken-1': '#3949AB',
          'blue darken-1': '#1E88E5',
          'light-blue darken-1': '#039BE5',
          'cyan darken-1': '#00ACC1',
          'deep-orange darken-1': '#F4511E',
          'orange darken-1': '#FB8C00',
          'teal darken-1': '#00897B',
          'green darken-1': '#43A047',
          'blue-grey darken-1': '#546E7A',
          'grey darken-1': '#757575',
        },
      }
    },
  }
</script>

<style scoped>
  .dialog-title {
    color: #FFFFFF;
  }

  .link-container {
    padding-top: 25px;
  }
</style>
