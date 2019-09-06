<template>
  <div>
    <BottomFormEditor 
      v-show="tabs == 0 && $viewport .width < 850"
      @addQuestion="addQuestion" />

    <div class="container whole-container">
      <v-tabs
        v-model="tabs"
        background-color="white"
        :color="themeColor"
        :slider-color="themeColor"
        centered>

        <v-tabs-slider></v-tabs-slider>

        <v-tab>
          QUESTIONS
        </v-tab>
        <v-tab>
          RESPONSE
        </v-tab>

        <v-tab-item>
          <v-card>
            <v-form>
              <v-container>
                <v-row>
                  <v-col>
                    <v-text-field
                      class="title font-weight-medium"
                      :color="themeColor"
                      v-model="question.title"/>
                    <v-text-field
                      :color="themeColor" 
                      placeholder="Form description" />
                  </v-col>
                </v-row>
              </v-container>
            </v-form>

            <FormEditor 
              v-show="$viewport .width > 850"
              @addQuestion="addQuestion" />

          </v-card>

          <draggable 
            v-model="question.questions"
            handle=".handle"
            @end="onEnd">
            <v-card 
              v-for="(question, questionIndex) in question.questions" 
              @click.native="focusForm(questionIndex)"
              :elevation="questionIndex == focusedFormIndex ? '24' : '0'">
              <div class="handle-icon-container">
                <v-icon 
                  class="handle"
                  v-show="isFocused(questionIndex)">mdi-dots-horizontal</v-icon>
              </div>
              <!-- Replace the whole element if the format is File upload -->
              <component
                :is="questionFormatList[question.questionFormat]"
                v-if="question.questionFormat == 'File upload'"
                @cancelFormFile="cancelFormFile(questionIndex)"
                @advanceToFormFile="advanceToFormFile(questionIndex)"
                :themeColor="themeColor" />
              <div v-else>
                <v-form>
                  <v-container>
                    <v-row>
                      <v-col 
                        cols="12" 
                        xl="8" 
                        lg="8" 
                        md="8" 
                        sm="8">
                        <v-text-field
                          class="title"
                          :color="themeColor"
                          :disabled="!isFocused(questionIndex)"
                          placeholder="Question"
                          v-model="question.question">
                        </v-text-field>
                      </v-col>
                      <v-col 
                        cols="8" 
                        xl="4" 
                        lg="4" 
                        md="4" 
                        sm="4">
                        <v-menu offset-y>
                          <template v-slot:activator="{ on }">
                            <v-btn
                              depressed 
                              v-on="on"
                              v-show="isFocused(questionIndex)">
                              <v-icon 
                                color="grey darken-1" 
                                left>
                                {{ question.questionIcon }}
                              </v-icon>
                              {{ question.questionFormat == 'Actually file upload' ? 'File upload' : question.questionFormat }}
                            </v-btn>
                          </template>
                          <v-list>
                            <v-list-item
                              v-for="(format, index) in questionFormat"
                              :key="index"
                              @click="changeQuestionFormat(questionIndex, question.questionFormat, question.questionIcon, format)">
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
                          :is="questionFormatList[question.questionFormat]"
                          @addOption="addOption(questionIndex)"
                          @deleteOption="(...args) => deleteOption(questionIndex, ...args)"
                          @addRow="addRow(questionIndex)"
                          @deleteRow="(...args) => deleteRow(questionIndex, ...args)"
                          @addColumn="addColumn(questionIndex)"
                          @deleteColumn="(...args) => deleteColumn(questionIndex, ...args)"
                          :question="question"
                          :questionIndex="questionIndex"
                          :themeColor="themeColor"
                          :focusedFormIndex="focusedFormIndex" />
                      </v-col>
                    </v-row>
                  </v-container>
                </v-form>

                <v-container v-show="isFocused(questionIndex)">
                  <v-divider></v-divider>
                </v-container>

                <v-card-actions 
                  class="card-actions"
                  v-show="isFocused(questionIndex)">
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
                        @click="deleteQuestion(questionIndex)"
                        v-on="on">
                        <v-icon>mdi-delete</v-icon>
                      </v-btn>
                    </template>
                    <span class="tooltip">Delete</span>
                  </v-tooltip>

                  <v-divider vertical></v-divider>
                  <span class="switch-label">Required</span>
                  <v-switch 
                    class="switch"
                    :color="themeColor"></v-switch>
                  <v-btn icon>
                    <v-icon>mdi-dots-vertical</v-icon>
                  </v-btn>
                </v-card-actions>
              </div>
            </v-card>
          </draggable>
        </v-tab-item>

        <v-tab-item>
          <ItemReponse :themeColor="themeColor" />
        </v-tab-item>
        
      </v-tabs>
    </div>
  </div>
</template>

<script>
  import draggable from 'vuedraggable'

  import FormChoices from '@/components/widgets/forms/FormChoices'
  import FormText from '@/components/widgets/forms/FormText'
  import FormFile from '@/components/widgets/forms/FormFile'
  import FormBeforeUploadFile from '@/components/widgets/forms/FormBeforeUploadFile'
  import FormScale from '@/components/widgets/forms/FormScale'
  import FormGrid from '@/components/widgets/forms/FormGrid'
  import ItemReponse from '@/components/widgets/tabItems/ItemReponse'
  import FormEditor from '@/components/widgets/cards/CardFormEditor'
  import BottomFormEditor from '@/components/widgets/cards/CardBottomFormEditor'

  export default {
    props: ["themeColor"],
    components: {
      draggable,
      FormText,
      FormChoices,
      FormFile,
      FormBeforeUploadFile,
      FormScale,
      FormGrid,
      ItemReponse,
      FormEditor,
      BottomFormEditor,
    },
    data() {
      return {
        focusedFormIndex: 0,
        tabs: 0,
        question: {
          title: 'Untitled form',
          description: '',
          questions: [
            {
              question: '',
              questionFormat: 'Multiple choices',
              questionIcon: 'mdi-radiobox-marked',
              oldFormat: 'Multiple choices',
              oldIcon: 'mdi-radiobox-marked',
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
        questionFormat: [
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
          questionFormatList: {
            'Short answer': 'FormText',
            'Paragraph': 'FormText',
            'Multiple choices': 'FormChoices',
            'Checkboxes': 'FormChoices',
            'Dropdown': 'FormChoices',
            'File upload': 'FormBeforeUploadFile',
            'Actually file upload': 'FormFile',
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
        // Insert form component into the next to the focused form
        this.question.questions.splice(this.focusedFormIndex + 1, 0, 
            {
              question: '',
              questionFormat: 'Multiple choices',
              questionIcon: 'mdi-radiobox-marked',
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
        this.focusedFormIndex += 1
      },
      deleteQuestion(questionIndex) {
        this.question.questions.splice(questionIndex, 1)
      },
      changeQuestionFormat(questionIndex, oldFormat, oldIcon, format) {
        this.question.questions[questionIndex].oldFormat = oldFormat
        this.question.questions[questionIndex].oldIcon = oldIcon
        this.question.questions[questionIndex].questionFormat = format.name
        this.question.questions[questionIndex].questionIcon = format.icon
      },
      addOption(questionIndex) {
        this.question.questions[questionIndex].options.push({
            option: '',
        })
      },
      deleteOption(questionIndex, args) {
        this.question.questions[questionIndex].options.splice(args, 1)
      },
      addRow(questionIndex) {
        this.question.questions[questionIndex].rows.push({
          row: '',
        })
      },
      deleteRow(questionIndex, args) {
        this.question.questions[questionIndex].rows.splice(args, 1)
      },
      addColumn(questionIndex) {
        this.question.questions[questionIndex].cols.push({
          col: '',
        })
      },
      deleteColumn(questionIndex, args) {
        this.question.questions[questionIndex].cols.splice(args, 1)
      },
      cancelFormFile(questionIndex) {
        this.question.questions[questionIndex].questionFormat = this.question.questions[questionIndex].oldFormat
        this.question.questions[questionIndex].questionIcon = this.question.questions[questionIndex].oldIcon
      },
      advanceToFormFile(questionIndex) {
        this.question.questions[questionIndex].questionFormat = 'Actually file upload'
      },
      focusForm(index) {
        this.focusedFormIndex = index
        // In case the index is out of range when deleting the last question while focusing on the form
        if (this.focusedFormIndex > this.question.questions.length - 1) {
          this.focusedFormIndex -= 1
        }
      },
      isFocused(index) {
        if (index == this.focusedFormIndex) {
          return true
        } else {
          return false
        }
      },
      onEnd(event) {
        this.focusedFormIndex = event.newIndex
      },
    },
  }
</script>

<style scoped>
  .container {
    max-width: 770px;
  }

  .whole-container {
    margin-bottom: 50px;
  }

  @media (max-width: 450px) {
    .whole-container {
      margin-bottom: 100px;
    }
  }

  .handle-icon-container {
    text-align: center;
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
