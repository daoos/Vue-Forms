<template>
  <div class="container">
    <v-card>
      <v-tabs
        background-color="white"
        color="deep-purple darken-1"
        slider-color="deep-purple darken-1"
        centered>

        <v-tabs-slider></v-tabs-slider>

        <v-tab href="question">
          Questions
        </v-tab>

        <v-tab href="response">
          Response
        </v-tab>

      </v-tabs>

      <v-form>
        <v-container>
          <v-row>
            <v-col>
              <v-text-field v-model="question.title"/>
              <v-text-field placeholder="Form description" />
            </v-col>
          </v-row>
        </v-container>
      </v-form>

      <v-card 
        class="form-editor" 
        width="36">
        <v-row>
          <v-col>
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn 
                  icon
                  @click="addQuestion"
                  v-on="on">
                  <v-icon>mdi-plus-circle</v-icon>
                </v-btn>
              </template>
              <span class="tooltip">Add question</span>
            </v-tooltip>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn 
                  icon
                  v-on="on">
                  <v-icon>mdi-import</v-icon>
                </v-btn>
              </template>
              <span class="tooltip">Import questions</span>
            </v-tooltip>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn 
                  icon
                  v-on="on">
                  <v-icon>mdi-format-title</v-icon>
                </v-btn>
              </template>
              <span class="tooltip">Add title and description</span>
            </v-tooltip>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn 
                  icon
                  v-on="on">
                  <v-icon>mdi-image</v-icon>
                </v-btn>
              </template>
              <span class="tooltip">Add image</span>
            </v-tooltip>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn 
                  icon
                  v-on="on">
                  <v-icon>mdi-youtube</v-icon>
                </v-btn>
              </template>
              <span class="tooltip">Add video</span>
            </v-tooltip>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn 
                  icon
                  v-on="on">
                  <v-icon>mdi-note-plus</v-icon>
                </v-btn>
              </template>
              <span class="tooltip">Add section</span>
            </v-tooltip>
          </v-col>
        </v-row>
      </v-card>

    </v-card>

    <v-card v-for="(question, question_index) in question.questions">
      <v-form>
        <v-container>
          <v-row>
            <v-col 
              cols="12" 
              md="8">
              <v-text-field v-model="question.question">
              </v-text-field>
            </v-col>
            <v-col
              cols="6"
              md="4">
              <v-menu offset-y>
                <template v-slot:activator="{ on }">
                  <v-btn
                    depressed 
                    v-on="on">
                    <v-icon 
                      color="#757575" 
                      left>{{ question.question_icon }}</v-icon>
                    {{ question.question_format }}
                  </v-btn>
                </template>
                <v-list>
                  <v-list-item
                    v-for="(format, index) in question_format"
                    :key="index"
                    @click="changeQuestionFormat(question_index, format)">
                    <v-list-item-icon>
                      <v-icon>{{ format.icon }}</v-icon>
                    </v-list-item-icon>
                    <v-list-item-title>
                      {{ format.name }}
                    </v-list-item-title>
                  </v-list-item>
                </v-list>
              </v-menu>
            </v-col>
          </v-row>
        </v-container>
      </v-form>

      <v-container>
        <v-divider></v-divider>
      </v-container>

      <v-card-actions>
        <div class="flex-grow-1"></div>
        <v-tooltip bottom>
          <template v-slot:activator="{ on }">
            <v-btn 
              icon
              v-on="on">
              <v-icon>mdi-content-copy</v-icon>
            </v-btn>
          </template>
          <span class="tooltip">Duplicate</span>
        </v-tooltip>

        <v-tooltip bottom>
          <template v-slot:activator="{ on }">
            <v-btn 
              icon
              @click="deleteQuestion(question_index)"
              v-on="on">
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </template>
          <span class="tooltip">Delete</span>
        </v-tooltip>

        <v-divider vertical></v-divider>
        <span class="switch-label">Required</span>
        <v-switch class="switch"></v-switch>
        <v-btn icon>
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </v-card-actions>
    </v-card>

  </div>
</template>

<script>
  export default {
    components: {

    },
    data() {
      return {
        question: {
          title: 'Untitled form',
          description: '',
          questions: [
            {
              question: 'Untitled question',
              question_format: 'Multiple choices',
              question_icon: 'mdi-radiobox-marked',
            }
          ],
        },
        question_format: [
            { name: 'Short answer', icon: 'mdi-text-short' }, 
            { name: 'Paragraph', icon: 'mdi-text' }, 
            { name : 'Multiple choices', icon: 'mdi-radiobox-marked' }, 
            { name: 'Checkboxes', icon: 'mdi-checkbox-marked' }, 
            { name: 'Dropdown', icon: 'mdi-arrow-down-drop-circle' }, 
            { name:'File upload', icon: 'mdi-cloud-upload' }, 
            { name: 'Linear scale', icon : 'mdi-undo' }, 
            { name: 'Multiple choice grid', icon: 'mdi-undo' }, 
            { name:'Checkbox grid', icon: 'mdi-undo' }, 
            { name: 'Date', icon: 'mdi-calendar-range' }, 
            { name:'Time', icon: 'mdi-clock-outline'},
          ],
      }
    },
    computed: {

    },
    methods: {
      addQuestion() {
        this.question.questions.push({
            question: 'Untitled question',
            question_format: 'Multiple choices',
            question_icon: 'mdi-radiobox-marked',
          }
        )
      },
      deleteQuestion(question_index) {
        this.question.questions.splice(question_index, 1)
      },
      changeQuestionFormat(question_index, format) {
        this.question.questions[question_index].question_format = format.name
        this.question.questions[question_index].question_icon = format.icon
      }
    }
  }
</script>

<style scoped>
  .container {
    max-width: 770px;
  }

  /* 50px right to the parent element (v-card) */
  .form-editor {
    position: absolute;
    top: 0px;
    right: -50px;
  }

  .switch-label {
    margin-right:15px; 
    margin-left:15px;
    color: #616161;
    font-weight: bold;
  }

  .switch {
    padding-top: 8px;
  }
</style>
