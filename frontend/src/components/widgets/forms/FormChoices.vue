<template>
	<div>
    <div v-for="(option, index) in numberOfOptions">
      <v-row>
        <v-col cols="10">
          <v-text-field
            :color="theme_color"
            :prepend-icon="getPrependIcon"
            :append-outer-icon="numberOfOptions >= 2 ? 'mdi-window-close' : undefined"
            @click:append-outer="deleteOption(index)"
            v-model="question.options[index].option">
          </v-text-field>
        </v-col>
      </v-row>
    </div>
    <v-row>
      <v-col cols="10">
        <v-text-field
          :color="theme_color"
          :prepend-icon="getPrependIcon"
          placeholder='Add option or ADD "OTHER"'
          @click="addOption">
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
    data() {
      return {
        numberOfOptions: this.question.options.length,
      }
    },
    computed: {
      getPrependIcon() {
        switch (this.question.question_format) {
          case 'Multiple choices':
            return 'mdi-circle-outline'
          case 'Checkboxes':
            return 'mdi-checkbox-blank-outline'
          case 'Dropdown':
            return 'mdi-arrow-down-drop-circle'
          }
      }
    },
    methods: {
      addOption() {
        this.numberOfOptions += 1
        this.$emit('addOption')
      },
      deleteOption(option_index) {
        this.numberOfOptions -= 1
        this.$emit('deleteOption', option_index)
      },
    }
	}
</script>

<style scoped>

</style>
