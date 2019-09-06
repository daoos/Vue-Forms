<template>
	<div>
		<v-row>
      <v-col 
        cols="12" 
        xl="6" 
        lg="6"
        md="6" 
        sm="6">
        <div>Rows</div>
          <div v-for="(row, index) in numberOfRows">
            <v-text-field 
              :color="themeColor"
              :append-outer-icon="numberOfRows >= 2 ? 'mdi-window-close' : undefined"
              @click:append-outer="deleteRow(index)"
              :disabled="!isFocused"
              v-model="question.rows[index].row">
            </v-text-field>
          </div>
          <v-text-field 
            :color="themeColor"
            placeholder="Add row"
            v-show="isFocused"
            @click="addRow">
          </v-text-field>
      </v-col>
      <v-col 
        cols="12" 
        xl="6" 
        lg="6" 
        md="6" 
        sm="6">
        <div>Columns</div>
          <div v-for="(col, index) in numberOfColumns">
            <v-text-field
              :color="themeColor"
              :prepend-icon="getPrependIcon"
              :append-outer-icon="numberOfColumns >= 2 ? 'mdi-window-close' : undefined"
              @click:append-outer="deleteColumn(index)"
              :disabled="!isFocused"
              v-model="question.cols[index].col">
            </v-text-field>
          </div>
          <v-text-field 
            :color="themeColor"
            :prepend-icon="getPrependIcon"
            placeholder="Add column"
            v-show="isFocused"
            @click="addColumn">
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
        numberOfRows: this.question.rows.length,
        numberOfColumns: this.question.cols.length,
      }
    },
    computed: {
      getPrependIcon() {
        switch (this.question.questionFormat) {
          case 'Multiple choice grid':
            return 'mdi-circle-outline'
          case 'Checkbox grid':
            return 'mdi-checkbox-blank-outline'
        }
      },
      isFocused() {
        if (this.focusedFormIndex == this.questionIndex) {
          return true
        } else {
          return false
        }
      },
    },
    methods: {
      addRow() {
        this.numberOfRows += 1
        this.$emit('addRow')
      },
      deleteRow(rowIndex) {
        this.numberOfRows -= 1
        this.$emit('deleteRow', rowIndex)
      },
      addColumn() {
        this.numberOfColumns += 1
        this.$emit('addColumn')
      },
      deleteColumn(colIndex) {
        this.numberOfColumns -= 1
        this.$emit('deleteColumn', colIndex)
      },
    }
  }
</script>

<style scoped>
  
</style>
