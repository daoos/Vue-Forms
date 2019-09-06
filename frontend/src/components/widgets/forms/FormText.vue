<template>
	<div>
   <v-row>
    <v-col 
      :cols="getXsCols" 
      :xl="getOtherCols"
      :lg="getOtherCols"
      :md="getOtherCols"
      :sm="getOtherCols">
      <v-text-field 
        :color="themeColor"
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
      "themeColor",
      ],
    computed: {
      getXsCols() {
        switch(this.question.questionFormat) {
          case 'Paragraph':
            return '10'
          case 'Short answer':
          case 'Date':
          case 'Time':
            return '8'
        }
      },
      getOtherCols() {
        switch(this.question.questionFormat) {
          case 'Paragraph':
            return '10'
          case 'Short answer':
            return '6'
          case 'Date':
          case 'Time':
            return '4'
        }
      },
      getPlaceHolder() {
        switch(this.question.questionFormat) {
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
        switch(this.question.questionFormat) {
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
