<template>
  <div>
    <v-card>
      <v-container>
        <v-row>
          <v-col cols="5">
            <span class="title">0 responses</span>
          </v-col>
          <div class="flex-grow-1"></div>
          <v-col cols="1">
            <DialogSpreadsheet :theme_color="theme_color" />
          </v-col>
          <v-col cols="1">
            <v-menu
              left
              bottom
            >
              <template v-slot:activator="{ on }">
                <v-btn 
                  icon 
                  v-on="on">
                    <v-icon>mdi-dots-vertical</v-icon>
                </v-btn>
              </template>

              <v-list>
                <v-list-item
                  v-for="(item, index) in items"
                  :key="index"
                  @click="">
                  <v-list-item-icon>
                    <v-icon>{{ item.icon }}</v-icon>
                  </v-list-item-icon>
                  <v-list-item-title>{{ item.name }}</v-list-item-title>
                </v-list-item>
              </v-list>
            </v-menu>
          </v-col>
        </v-row>
        <v-row>
          <div 
            class="flex-grow-1 switch-label-container-left"
            :style="{ backgroundColor: getBackgroundColor }"></div>
          <v-col 
            class="switch-label-container"
            cols="4" 
            :style="{ backgroundColor: getBackgroundColor }">
            <div
              class="response-switch-label"
              :style="{ color: switch_1 ? '#757575' : 'white' }"
              >{{ switch_1 ? 'Accepting responses' : 'Not accepting responses' }}</div>
          </v-col>
          <v-col 
            class="switch-container"
            cols="2"
            :style="{ backgroundColor: getBackgroundColor }">
            <v-switch 
              class="switch"
              :color="theme_color"
              v-model="switch_1"></v-switch>
          </v-col>
          <v-col 
            class="message-for-respondents-text-field-col"
            cols="12"">
            <v-card
              v-show="!switch_1"
              tile 
              outlined>
              <v-form>
                <v-container>
                  <v-row>
                    <v-col>
                      <v-text-field
                        :color="theme_color"
                        label="Message for respondents"
                        placeholder="This form is no longer accepting responses" />
                    </v-col>
                  </v-row>
                </v-container>
              </v-form>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-card>
    <v-card v-show="switch_1">
      <div class="accepting-response-text">
        Waiting for response
      </div>
    </v-card>
  </div>
</template>

<script>
  import DialogSpreadsheet from '@/components/widgets/dialogs/DialogSpreadsheet'

  export default {
    props: ["theme_color"],
    components: {
      DialogSpreadsheet,
    },
    data() {
      return {
        switch_1: true,
        items: [
          { name: 'Get email notificaitons for new responses', icon: undefined },
          { name: 'Select response destination', icon: undefined },
          { name: 'Unlink form', icon: undefined },
          { name: 'Download responses (.csv)', icon: 'mdi-download' },
          { name: 'Print all responses', icon: 'mdi-printer' },
          { name: 'Delete all responses', icon: undefined },
        ],
      }
    },
    computed: {
      getBackgroundColor() {
        if (this.switch_1) {
          return 'white'
        } else {
          return '#E53935'
        }
      }  
    }
  }
</script>

<style scoped>
  .switch-container {
    padding-bottom: 0px; 
    margin-right: 12px;
  }

  .switch-label-container {
    text-align: right;
  }

  .switch-label-container-left {
    margin-left: 12px;
  }

  .switch-label {
    margin-right:15px; 
    margin-left:15px;
    color: #616161;
    font-weight: bold;
  }

  .response-switch-label {
    position: relative;
    padding-top: 23px;
  }

  .message-for-respondents-text-field-col {
    padding-top: 0px;
  }

  .accepting-response-text {
    text-align: center; 
    padding: 32px 20px 110px 20px; 
    color: #757575;
  }  
</style>
