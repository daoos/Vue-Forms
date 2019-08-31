<template>
	<div>
   <v-row>
    <v-col :cols="getCols">
      <v-text-field 
        :color="theme_color"
        :placeholder="getPlaceHolder"
        :append-icon="getAppendIcon"
        disabled>
      </v-text-field>
    </v-col>
   </v-row> 
  </div>
</template>

<script>
	export default {
    props: [
      "question",
      "theme_color",
      ],
    computed: {
      getCols() {
        switch(this.question.question_format) {
          case 'Short answer':
            return '6'
          case 'Paragraph':
            return '10'
          case 'Date':
          case 'Time':
            return '4'
        }
      },
      getPlaceHolder() {
        switch(this.question.question_format) {
          case 'Short answer':
            return 'Short answer text'
          case 'Paragraph':
            return 'Long answer text'
          case 'Date':
            return 'Month, day, year'
          case 'Time':
            return 'Time'
        }        
      },
      getAppendIcon() {
        switch(this.question.question_format) {
          case 'Date':
            return 'mdi-calendar-range'
          case 'Time':
            return 'mdi-clock-outline'
          default:
            return undefined
        }        
      },
    }
  }
</script>

<style scoped>
	
</style>
