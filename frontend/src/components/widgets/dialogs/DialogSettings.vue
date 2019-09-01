<template>
  <v-dialog 
    max-width="600px"
    v-model="settings_dialog">
    <template v-slot:activator="{ on: settings_dialog }">
      <v-tooltip bottom>
        <template v-slot:activator="{ on: tooltip }">
          <v-btn 
            icon
            v-on="{ ...tooltip, ...settings_dialog }">
            <v-icon>mdi-settings</v-icon>
          </v-btn>
        </template>
        <span class="tooltip">Settings</span>
      </v-tooltip>
    </template>
    <v-card tile>
      <v-card-title v-bind:style="{ backgroundColor: theme_color_list[theme_color] }">
        <span class="headline font-weight-medium dialog-title">Settings</span>
      </v-card-title>
      <v-tabs
        :background-color="theme_color"
        color="white"
        slider-color="white">
        <v-tabs-slider></v-tabs-slider>
        <v-tab>GENERAL</v-tab>
        <v-tab>PRESENTATION</v-tab>
        <v-tab>QUIZZES</v-tab>
      <v-tab-item>
        <v-card-text class="text--primary">
            <v-row>
              <v-col>
                <v-checkbox
                  :color="theme_color"
                  label="Collect email addresses"
                  v-model="isEmailCollected"></v-checkbox>
                <v-checkbox
                  :color="theme_color"
                  label="Response receipts"
                  append-icon="mdi-help-circle"
                  :disabled="!isEmailCollected"></v-checkbox>
              </v-col>
            </v-row>
            <v-row>
              <v-col>
                <span class="font-weight-medium">Requires sign in:</span>
                <v-checkbox
                  :color="theme_color"
                  label="Limit to 1 response"></v-checkbox>
              </v-col>
            </v-row>
            <v-divider></v-divider>
            <v-row>
              <v-col>
                <span class="font-weight-medium">Respondents can:</span>
                <v-checkbox
                  :color="theme_color"
                  label="Edit after submit"></v-checkbox>
                <v-checkbox
                  :color="theme_color"
                  label="See summary charts and response"></v-checkbox>
              </v-col>
            </v-row>
        </v-card-text>
      </v-tab-item>
      <v-tab-item>
        <v-card-text class="text--primary">
          <v-row>
            <v-col>
              <v-checkbox
                :color="theme_color"
                label="Show progress bar">
              </v-checkbox>
              <v-checkbox
                :color="theme_color"
                label="Shuffle question order">
              </v-checkbox>
              <v-checkbox
                :color="theme_color"
                label="Show link to submit another response"
                v-model="checkbox_1">
              </v-checkbox>
              <p class="font-weight-bold">Confirmation message:</p>
              <p>Your response has been recorded.</p>
              <v-divider></v-divider>
            </v-col>
          </v-row>
        </v-card-text>
      </v-tab-item>
      <v-tab-item>
        <v-card-text>
          <v-row>
            <v-col>
              <v-switch 
                class="switch"
                :color="theme_color"
                label="Make this a quiz"
                v-model="isQuiz"></v-switch>
              <span>Assign point values to questions and allow auto-grading.</span>        
            </v-col>
          </v-row>
          <v-divider></v-divider>
          <v-row>
            <v-col>
              <h3 class="font-weight-bold">Quiz options</h3>
              <br>
              <p class="font-weight-bold">Release grade:</p>
              <v-radio-group 
                v-model="active"
                :disabled="!isQuiz">
                <v-radio
                  label="Immediately after each submission"
                  :value="true"
                  :color="theme_color"></v-radio>
                <v-radio
                  label="Later, after manual review"
                  :value="false"
                  :color="theme_color"></v-radio>
              </v-radio-group>
              <p class="font-weight-bold">Respondent can see:</p>
              <v-checkbox
                :color="theme_color"
                label="Missed questions"
                append-icon="mdi-help-circle"
                v-model="checkbox_2"
                :disabled="!isQuiz">
              </v-checkbox>
              <v-checkbox
                :color="theme_color"
                label="Correct answers"
                append-icon="mdi-help-circle"
                v-model="checkbox_3"
                :disabled="!isQuiz">
              </v-checkbox>
              <v-checkbox
                :color="theme_color"
                label="Point values"
                append-icon="mdi-help-circle"
                v-model="checkbox_4"
                :disabled="!isQuiz">
              </v-checkbox> 
            </v-col>
          </v-row>
        </v-card-text>
      </v-tab-item>
      </v-tabs>
      <v-divider></v-divider>
      <v-card-actions>
        <div class="flex-grow-1"></div>
        <v-btn 
          text
          @click="settings_dialog = false">CANCEL</v-btn>
        <v-btn 
          :color="theme_color" 
          text
          @click="settings_dialog = false">SAVE</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
  export default {
    props: ["theme_color"],
    data() {
      return {
        settings_dialog: false,
        active: true,
        checkbox_1: true,
        checkbox_2: true,
        checkbox_3: true,
        checkbox_4: true,
        isQuiz: false,
        isEmailCollected: false,
        theme_color_list: {
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
</style>