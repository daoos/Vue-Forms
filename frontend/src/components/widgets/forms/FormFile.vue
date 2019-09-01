<template>
	<div>
    <v-row>
      <v-col cols="6">
        <div class="label">Allow only specific file types</div>
      </v-col>
      <v-col cols="2">
        <v-switch
          v-model="switch_1" 
          :color="theme_color"></v-switch>
      </v-col>
    </v-row>
    <v-row v-show="switch_1">
      <v-col cols="3">
        <v-checkbox 
          class="checkbox"
          v-for="(item, index) in col1_items"
          :color="theme_color"
          :label="item">
        </v-checkbox>       
      </v-col>
      <v-col cols="3">
        <v-checkbox 
          class="checkbox"
          v-for="(item, index) in col2_items"
          :color="theme_color"
          :label="item">
        </v-checkbox>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6">
        <div class="label">Maximum number of files</div>
      </v-col>
      <v-col cols="2">
        <v-select 
          v-model="numberOfFiles"
          :items="maximumNumberOfFiles"
          :item-text="numberOfFiles"
          :item-value="numberOfFiles"></v-select>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6">
        <div class="label">Maximum file size</div>
      </v-col>
      <v-col cols="2">
        <v-select 
          v-model="fileSize"
          :items="maximumFileSize"
          :item-text="fileSize"
          :item-value="fileSize"></v-select>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6">
        <small style="color: #757575">
          This form accept up to 1 GB files. 
          <a>Change</a>
        </small>
      </v-col>
    </v-row>
  </div>
</template>

<script>
  export default {
    props: ["theme_color"],
    data() {
      return {
        switch_1: false,
        numberOfFiles: '1',
        fileSize: '10MB',
        maximumNumberOfFiles: ['1', '5', '10'],
        maximumFileSize: ['1MB', '10MB', '100MB', '1GB', '10GB'],
        col1_items: ['Document', 'Spreadsheet', 'PDF', 'Video'],
        col2_items: ['Presentation', 'Drawing', 'Image', 'Audio'],
      }
    }
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
</style>
