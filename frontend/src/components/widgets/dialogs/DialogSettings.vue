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
      <v-card-title class="dialog-header">
        <span class="headline font-weight-medium dialog-title">Settings</span>
      </v-card-title>
      <v-tabs
        background-color="deep-purple darken-1"
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
                  color="deep-purple darken-1"
                  label="Collect email addresses"
                  v-model="isEmailCollected"></v-checkbox>
                <v-checkbox
                  color="deep-purple darken-1"
                  label="Response receipts"
                  append-icon="mdi-help-circle"
                  :disabled="!isEmailCollected"></v-checkbox>
              </v-col>
            </v-row>
            <v-row>
              <v-col>
                <span class="font-weight-medium">Requires sign in:</span>
                <v-checkbox
                  color="deep-purple darken-1"
                  label="Limit to 1 response"></v-checkbox>
              </v-col>
            </v-row>
            <v-divider></v-divider>
            <v-row>
              <v-col>
                <span class="font-weight-medium">Respondents can:</span>
                <v-checkbox
                  color="deep-purple darken-1"
                  label="Edit after submit"></v-checkbox>
                <v-checkbox
                  color="deep-purple darken-1"
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
                color="deep-purple darken-1"
                label="Show progress bar">
              </v-checkbox>
              <v-checkbox
                color="deep-purple darken-1"
                label="Shuffle question order">
              </v-checkbox>
              <v-checkbox
                color="deep-purple darken-1"
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
                  color="deep-purple darken-1"></v-radio>
                <v-radio
                  label="Later, after manual review"
                  :value="false"
                  color="deep-purple darken-1"></v-radio>
              </v-radio-group>
              <p class="font-weight-bold">Respondent can see:</p>
              <v-checkbox
                color="deep-purple darken-1"
                label="Missed questions"
                append-icon="mdi-help-circle"
                v-model="checkbox_2"
                :disabled="!isQuiz">
              </v-checkbox>
              <v-checkbox
                color="deep-purple darken-1"
                label="Correct answers"
                append-icon="mdi-help-circle"
                v-model="checkbox_3"
                :disabled="!isQuiz">
              </v-checkbox>
              <v-checkbox
                color="deep-purple darken-1"
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
          color="deep-purple darken-1" 
          text
          @click="settings_dialog = false">SAVE</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
  export default {
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
      }
    }
  }
</script>

<style scoped>
  .dialog-header {
    background-color: #5E35B1;
  }
  .dialog-title {
    color: #FFFFFF;
  }
</style>