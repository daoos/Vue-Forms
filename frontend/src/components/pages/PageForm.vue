<template>
  <div class="container whole-container">
    <v-card>
      <v-tabs
        background-color="white"
        color="deep-purple darken-1"
        slider-color="deep-purple darken-1"
        centered>

        <v-tabs-slider></v-tabs-slider>

        <v-tab href="question">
          QUESTIONS
        </v-tab>
        <v-tab href="response">
          RESPONSE
        </v-tab>

      </v-tabs>

      <v-form>
        <v-container>
          <v-row>
            <v-col>
              <v-text-field
                class="input-title font-weight-medium"
                color="deep-purple darken-1"
                v-model="question.title"/>
              <v-text-field
                color="deep-purple darken-1" 
                placeholder="Form description" />
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
      <!-- Replace the whole element if the format is File upload -->
      <component
        :is="question_format_list[question.question_format]"
        v-if="question.question_format == 'File upload'" />
      <div v-else>
        <v-form>
          <v-container>
            <v-row>
              <v-col cols="8">
                <v-text-field
                  color="deep-purple darken-1"
                  placeholder="Question"
                  v-model="question.question">
                </v-text-field>
              </v-col>
              <v-col cols="4">
                <v-menu offset-y>
                  <template v-slot:activator="{ on }">
                    <v-btn
                      depressed 
                      v-on="on">
                      <v-icon 
                        color="grey darken-1" 
                        left>
                        {{ question.question_icon }}
                      </v-icon>
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
            <v-row>
              <v-col>
                <component
                  :is="question_format_list[question.question_format]"
                  @addOption="addOption(question_index)"
                  @deleteOption="(...args) => deleteOption(question_index, ...args)"
                  @addRow="addRow(question_index)"
                  @deleteRow="(...args) => deleteRow(question_index, ...args)"
                  @addColumn="addColumn(question_index)"
                  @deleteColumn="(...args) => deleteColumn(question_index, ...args)"
                  :question="question" />
              </v-col>
            </v-row>
          </v-container>
        </v-form>

        <v-container>
          <v-divider></v-divider>
        </v-container>

        <v-card-actions class="card-actions">
          <div class="flex-grow-1"></div>
          <v-tooltip bottom>
            <template v-slot:activator="{ on }">
              <v-btn
                class="actions-icon"
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
                class="actions-icon"
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
      </div>
    </v-card>
  </div>
</template>

<script>
  import FormChoices from '@/components/widgets/forms/FormChoices'
  import FormText from '@/components/widgets/forms/FormText'
  import FormFile from '@/components/widgets/forms/FormFile'
  import FormScale from '@/components/widgets/forms/FormScale'
  import FormGrid from '@/components/widgets/forms/FormGrid'

  export default {
    components: {
      FormText,
      FormChoices,
      FormFile,
      FormScale,
      FormGrid,
    },
    data() {
      return {
        question: {
          title: 'Untitled form',
          description: '',
          questions: [
            {
              question: '',
              question_format: 'Multiple choices',
              question_icon: 'mdi-radiobox-marked',
              options: [
                {
                  option: 'Option1',
                },
              ],
              rows: [
                {
                  row: 'Row1',
                },
              ],
              cols: [
                {
                  col: 'Column1',
                },
              ],
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
            { name: 'Linear scale', icon : 'mdi-ray-vertex' }, 
            { name: 'Multiple choice grid', icon: 'mdi-gamepad-circle' }, 
            { name:'Checkbox grid', icon: 'mdi-apps' }, 
            { name: 'Date', icon: 'mdi-calendar-range' }, 
            { name:'Time', icon: 'mdi-clock-outline'},
          ],
          question_format_list: {
            'Short answer': 'FormText',
            'Paragraph': 'FormText',
            'Multiple choices': 'FormChoices',
            'Checkboxes': 'FormChoices',
            'Dropdown': 'FormChoices',
            'File upload': 'FormFile',
            'Linear scale': 'FormScale',
            'Multiple choice grid': 'FormGrid',
            'Checkbox grid': 'FormGrid',
            'Date': 'FormText',
            'Time': 'FormText',
          }
      }
    },
    methods: {
      addQuestion() {
        this.question.questions.push({
            question: '',
            question_format: 'Multiple choices',
            question_icon: 'mdi-radiobox-marked',
            options: [
              {
                option: 'Option1',
              },
            ],
            rows: [
              {
                row: 'Row1',
              }
            ],
            cols: [
              {
                col: 'Column1',
              }
            ],
          }
        )
      },
      deleteQuestion(question_index) {
        this.question.questions.splice(question_index, 1)
      },
      changeQuestionFormat(question_index, format) {
        this.question.questions[question_index].question_format = format.name
        this.question.questions[question_index].question_icon = format.icon
      },
      addOption(question_index) {
        this.question.questions[question_index].options.push({
            option: '',
        })
      },
      deleteOption(question_index, args) {
        this.question.questions[question_index].options.splice(args, 1)
      },
      addRow(question_index) {
        this.question.questions[question_index].rows.push({
          row: '',
        })
      },
      deleteRow(question_index, args) {
        this.question.questions[question_index].rows.splice(args, 1)
      },
      addColumn(question_index) {
        this.question.questions[question_index].cols.push({
          col: '',
        })
      },
      deleteColumn(question_index, args) {
        this.question.questions[question_index].cols.splice(args, 1)
      },
    }
  }
</script>

<style scoped>
  .container {
    max-width: 770px;
  }

  .whole-container {
    margin-bottom: 50px;
  }

  /* 50px right to the parent element (v-card) */
  .form-editor {
    position: absolute;
    top: 0px;
    right: -50px;
  }

  .input-title {
    font-size: 24px;
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

  .card-actions {
    height: 60px;
  }

  .actions-icon {
    margin: 0 20px 0 5px;
  }
</style>
