<template>
  <v-card 
    class="bottom-form-editor"
    elevation="24">
    <v-row>
      <v-col>
        <v-tooltip right>
          <template v-slot:activator="{ on }">
            <v-btn 
              class="bottom-form-editor-button"
              icon
              @click="addQuestion"
              v-on="on">
              <v-icon>mdi-plus-circle</v-icon>
            </v-btn>
          </template>
          <span class="tooltip">Add question</span>
        </v-tooltip>
        <v-tooltip right>
          <template v-slot:activator="{ on }">
            <v-btn 
              class="bottom-form-editor-button"
              icon
              v-on="on">
              <v-icon>mdi-import</v-icon>
            </v-btn>
          </template>
          <span class="tooltip">Import questions</span>
        </v-tooltip>
        <v-tooltip right>
          <template v-slot:activator="{ on }">
            <v-btn 
              class="bottom-form-editor-button"
              icon
              v-on="on">
              <v-icon>mdi-format-title</v-icon>
            </v-btn>
          </template>
          <span class="tooltip">Add title and description</span>
        </v-tooltip>
        <v-tooltip right>
          <template v-slot:activator="{ on }">
            <v-btn 
              class="bottom-form-editor-button"
              icon
              v-on="on">
              <v-icon>mdi-image</v-icon>
            </v-btn>
          </template>
          <span class="tooltip">Add image</span>
        </v-tooltip>
        <v-tooltip right>
          <template v-slot:activator="{ on }">
            <v-btn 
              class="bottom-form-editor-button"
              icon
              v-on="on">
              <v-icon>mdi-youtube</v-icon>
            </v-btn>
          </template>
          <span class="tooltip">Add video</span>
        </v-tooltip>
        <v-tooltip right>
          <template v-slot:activator="{ on }">
            <v-btn 
              class="bottom-form-editor-button"
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
</template>

<script>
  export default {
    methods: {
     addQuestion() {
        this.$emit('addQuestion')
      },      
    }
  }
</script>

<style scoped>
  .bottom-form-editor {
    position :fixed;
    width: 90%; 
    margin: 0 16px;
    bottom: 0px; 
    z-index: 1; 
    text-align: center;
  }

  .bottom-form-editor-button {
    margin-left: 2%;
    margin-right: 2%;
  }  
</style>