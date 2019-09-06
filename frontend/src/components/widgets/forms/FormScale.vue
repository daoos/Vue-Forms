<template>
	<div>
   <v-row>
    <v-col 
      cols="2" 
      xl="1" 
      lg="1" 
      md="1" 
      sm="1">
      <v-select 
        :items="min"
        :label="question.minScale"
        :disabled="!isFocused"
        v-model="question.minScale">
      </v-select>
    </v-col>
    <v-col 
      cols="2" 
      xl="1" 
      lg="1" 
      md="1" 
      sm="1">
      <div 
        class="to"
        :style="{ color: !isFocused ? '#BDBDBD' : undefined }">to</div>
    </v-col>
    <v-col 
      cols="2"
      xl="1" 
      lg="1" 
      md="1" 
      sm="1">
      <v-select 
        :items="max"
        :label="question.maxScale"
        :disabled="!isFocused"
        v-model="question.maxScale">
      </v-select>
    </v-col>
   </v-row>
   <v-row>
    <v-col 
      cols="8" 
      xl="3" 
      lg="3" 
      md="3" 
      sm="3">
      <v-text-field 
        :color="themeColor"
        placeholder="Label (optional)"
        :disabled="!isFocused"
        v-model="question.minScaleLabel">
      </v-text-field>
    </v-col>
   </v-row>
   <v-row>
    <v-col 
      cols="8" 
      xl="3" 
      lg="3" 
      md="3" 
      sm="3">
      <v-text-field 
        :color="themeColor"
        placeholder="Label (optional)"
        :disabled="!isFocused"
        v-model="question.maxScaleLabel">
      </v-text-field>
    </v-col>
   </v-row>
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
        min: [
          '0',
          '1',
        ],
        max: [
          '2',
          '3',
          '4',
          '5',
          '6',
          '7',
          '8',
          '9',
          '10',
        ]
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
    }
  }
</script>

<style scoped>
  .to {
    position: relative; 
    padding-top: 20px;
  }
</style>
