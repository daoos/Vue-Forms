<template>
  <v-card 
    class="form-editor" 
    width="36"
    :style="{ top: distance + 'px' }">
    <v-row>
      <v-col>
        <v-tooltip right>
          <template v-slot:activator="{ on }">
            <v-btn 
              class="form-editor-button"
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
              class="form-editor-button"
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
              class="form-editor-button"
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
              class="form-editor-button"
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
              class="form-editor-button"
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
              class="form-editor-button"
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
    data() {
      return {
        distance: 0,
      }
    },
    methods: {
      addQuestion() {
        this.$emit('addQuestion')
      },
      handleScroll() {
        this.distance = window.scrollY
      },
    },
    created() {
      window.addEventListener('scroll', this.handleScroll)
    },
    destroyed() {
      window.removeEventListener('scroll', this.handleScroll)
    },
  }
</script>

<style scoped>
  /* 50px right to the parent element (v-card) */
  .form-editor {
    position: absolute;
    right: -50px;
  }

  .form-editor-button {
    margin-bottom: 7px;
  }  
</style>
