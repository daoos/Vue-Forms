<template>
  <div>
  	<div v-show="isFocused">
      <v-row>
        <v-col 
          cols="8" 
          xl="6" 
          lg="6" 
          md="6" 
          sm="6">
          <div class="label">Allow only specific file types</div>
        </v-col>
        <v-col 
          cols="2" 
          xl="2" 
          lg="2" 
          md="2" 
          sm="2">
          <v-switch
            v-model="question.isSpecificFileAllowed" 
            :color="themeColor"></v-switch>
        </v-col>
      </v-row>
      <v-row v-show="question.isSpecificFileAllowed">
        <v-col 
          cols="6" 
          xl="3" 
          lg="3" 
          md="3" 
          sm="3">
          <v-checkbox 
            class="checkbox"
            v-for="(item, index) in items1"
            :color="themeColor"
            :label="item">
          </v-checkbox>       
        </v-col>
        <v-col 
          cols="6" 
          xl="3" 
          lg="3" 
          md="3" 
          sm="3">
          <v-checkbox 
            class="checkbox"
            v-for="(item, index) in items2"
            :color="themeColor"
            :label="item">
          </v-checkbox>
        </v-col>
      </v-row>
      <v-row>
        <v-col 
          cols="8" 
          xl="6" 
          lg="6" 
          md="6" 
          sm="6">
          <div class="label">Maximum number of files</div>
        </v-col>
        <v-col 
          cols="2" 
          xl="2" 
          lg="2" 
          md="2" 
          sm="2">
          <v-select 
            v-model="question.numberOfFiles"
            :items="maximumNumberOfFiles"
            :item-text="question.numberOfFiles"
            :item-value="question.numberOfFiles"></v-select>
        </v-col>
      </v-row>
      <v-row>
        <v-col 
          cols="8" 
          xl="6" 
          lg="6" 
          md="6" 
          sm="6">
          <div class="label">Maximum file size</div>
        </v-col>
        <v-col 
          cols="4" 
          xl="2" 
          lg="2" 
          md="2" 
          sm="2">
          <v-select 
            v-model="question.fileSize"
            :items="maximumFileSize"
            :item-text="question.fileSize"
            :item-value="question.fileSize"></v-select>
        </v-col>
      </v-row>
      <v-row>
        <v-col 
          cols="12" 
          xl="6" 
          lg="6" 
          md="6" 
          sm="6">
          <small style="color: #757575">
            This form accept up to 1 GB files. 
            <a>Change</a>
          </small>
        </v-col>
      </v-row>
    </div>
    <div 
      class="add-file"
      v-show="!isFocused">
      ADD FILE
    </div>
  </div>
</template>

<script>
  export default {
    props: [
      "question",
      "questionIndex",
      "themeColor",
      "focusedFormIndex",
      ],
    data() {
      return {
        maximumNumberOfFiles: ['1', '5', '10'],
        maximumFileSize: ['1MB', '10MB', '100MB', '1GB', '10GB'],
        items1: ['Document', 'Spreadsheet', 'PDF', 'Video'],
        items2: ['Presentation', 'Drawing', 'Image', 'Audio'],
      }
    },
    computed: {
      isFocused() {
        if (this.focusedFormIndex == this.questionIndex) {
          return true
        } else {
          return false
        }
      },
    },
  }
</script>

<style scoped>
  .label {
    padding-top: 19px;
  }

  .checkbox {
    margin-top: 0;
    padding-top: 0;
  }

  .add-file {
    color: #BDBDBD;
  }
</style>
