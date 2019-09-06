<template>
  <div>
    <v-card-title class="font-weight-medium">Let respondents upload files to Drive</v-card-title>
    <v-card-text>Files will be uploaded to the form owner's Google Drive. Respondents will be required to sign in to Google when file upload questions are added to a form. Make sure to only share this form with people you trust.</v-card-text>
    <v-card-actions>
      <div class="flex-grow-1"></div>
      <v-btn
        text
        color="black"
        @click="cancelFormFile">
        CANCEL
      </v-btn>
      <v-btn
        text
        :color="themeColor"
        @click="advanceToFormFile">
        CONTINUE
      </v-btn>
    </v-card-actions>
  </div>
</template>

<script>
	export default {
    props: ["themeColor"],
    methods: {
      cancelFormFile() {
        this.$emit('cancelFormFile')
      },
      advanceToFormFile() {
        this.$emit('advanceToFormFile')
      },
    }
  }
</script>

<style scoped>
	
</style>
