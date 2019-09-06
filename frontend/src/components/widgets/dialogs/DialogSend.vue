<template>
  <v-dialog 
    max-width="600px"
    v-model="dialog"
    :fullscreen="$viewport.width < 450">
    <template v-slot:activator="{ on: dialog }">
      <v-tooltip bottom>
        <template v-slot:activator="{ on: tooltip }">
          <v-btn 
            icon
            v-on="{ ...tooltip, ...dialog }">
            <v-icon>mdi-send</v-icon>
          </v-btn>
        </template>
        <span class="tooltip">Send</span>
      </v-tooltip>
    </template>
    <v-card tile>
      <v-card-title v-bind:style="{ backgroundColor: themeColorList[themeColor]  }">
        <span class="headline font-weight-medium dialog-title">Send form</span>
        <div class="flex-grow-1"></div>
        <v-btn 
          icon
          @click="dialog = false">
          <v-icon color="white">mdi-close</v-icon>
        </v-btn>
      </v-card-title>        
      <v-card-text class="text--primary">
          <v-row>
            <v-col>
              <v-checkbox
                :color="themeColor"
                label="Collect email addresses"></v-checkbox>
            </v-col>
          </v-row>
      <v-tabs
        background-color="white"
        color="grey darken-1"
        :slider-color="themeColor">
        <span class="send-via">Send via</span>
        <v-tabs-slider></v-tabs-slider>
        <v-tab><v-icon>mdi-email</v-icon></v-tab>
        <v-tab><v-icon>mdi-attachment</v-icon></v-tab>
        <v-tab><v-icon>mdi-code-tags</v-icon></v-tab>
        <div class="flex-grow-1"></div>
        <v-icon>mdi-facebook-box</v-icon>
        <v-icon>mdi-twitter-box</v-icon>
      <v-tab-item>
        <v-container>
        <v-row>
          <v-col>
            <span>Email</span>
            <v-text-field 
              placeholder="To"
              :color="themeColor">
            </v-text-field>
            <v-text-field 
              label="Subject"
              :color="themeColor">
            </v-text-field>
            <v-text-field 
              label="Message"
              :color="themeColor"
              value="I've invited you to fill out a form.">
            </v-text-field>
            <v-checkbox
              :color="themeColor"
              label="Include from in email"></v-checkbox>
          </v-col>
        </v-row>
        </v-container>
      </v-tab-item>
      <v-tab-item>
        <v-container>
        <v-row>
          <v-col>
            <span>Link</span>
            <v-text-field :color="themeColor">
            </v-text-field>
            <v-checkbox
              :color="themeColor"
              label="Shorten URL"></v-checkbox>
          </v-col>
        </v-row>
        </v-container>
      </v-tab-item>
      <v-tab-item>
        <v-container>
        <v-row>
          <v-col>
            <span>Embed HTML</span>
            <v-text-field :color="themeColor">
            </v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="2">
            <span class="append-text">Width</span>
          </v-col>
          <v-col cols="2" class="width-height-text-field">
            <v-text-field :color="themeColor"></v-text-field>
          </v-col>
          <v-col cols="1">
            <span class="append-text">px</span>
          </v-col>
          <v-divider vertical></v-divider>
          <v-col cols="2">
            <span class="append-text">Height</span>
          </v-col>
          <v-col cols="2" class="width-height-text-field">
            <v-text-field :color="themeColor"></v-text-field>
          </v-col>
          <v-col cols="1">
            <span class="append-text">px</span>
          </v-col>
        </v-row>
        </v-container>
      </v-tab-item>
      </v-tabs>
      </v-card-text>
      <v-card-actions>
        <div class="flex-grow-1"></div>
        <v-btn 
          text
          @click="dialog = false">CANCEL</v-btn>
        <v-btn 
          :color="themeColor" 
          text
          @click="dialog = false">SAVE</v-btn>
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
    }
	}
</script>

<style scoped>
  .dialog-title {
    color: #FFFFFF;
  }
  .send-via {
    color: black;
    padding-top: 15px;
  }
  .append-text {
    position: absolute;
    padding-top: 25px;
  }
  .width-height-text-field {
    padding-left: 0px;
  }
</style>
