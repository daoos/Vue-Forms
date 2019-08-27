<template>
	<div>
		<v-row>
      <v-col cols="6">
        <div>Rows</div>
          <div v-for="(row, index) in numberOfRows">
            <v-text-field 
              color="deep-purple darken-1"
              :append-outer-icon="numberOfRows >= 2 ? 'mdi-window-close' : undefined"
              @click:append-outer="deleteRow(index)"
              v-model="question.rows[index].row">
            </v-text-field>
          </div>
          <v-text-field 
            color="deep-purple darken-1"
            placeholder="Add row"
            @click="addRow">
          </v-text-field>
      </v-col>
      <v-col cols="6">
        <div>Columns</div>
          <div v-for="(col, index) in numberOfColumns">
            <v-text-field
              color="deep-purple darken-1"
              :prepend-icon="getPrependIcon"
              :append-outer-icon="numberOfColumns >= 2 ? 'mdi-window-close' : undefined"
              @click:append-outer="deleteColumn(index)"
              v-model="question.cols[index].col">
            </v-text-field>
          </div>
          <v-text-field 
            color="deep-purple darken-1"
            :prepend-icon="getPrependIcon"
            placeholder="Add column"
            @click="addColumn">
          </v-text-field>
      </v-col>
    </v-row>
	</div>
</template>

<script>
  export default {
    props: ["question"],
    data() {
      return {
        numberOfRows: this.question.rows.length,
        numberOfColumns: this.question.cols.length,
      }
    },
    computed: {
      getPrependIcon() {
        switch (this.question.question_format) {
          case 'Multiple choice grid':
            return 'mdi-circle-outline'
          case 'Checkbox grid':
            return 'mdi-checkbox-blank-outline'
        }
      }
    },
    methods: {
      addRow() {
        this.numberOfRows += 1
        this.$emit('addRow')
      },
      deleteRow(row_index) {
        this.numberOfRows -= 1
        this.$emit('deleteRow', row_index)
      },
      addColumn() {
        this.numberOfColumns += 1
        this.$emit('addColumn')
      },
      deleteColumn(col_index) {
        this.numberOfColumns -= 1
        this.$emit('deleteColumn', col_index)
      }
    }
  }
</script>

<style scoped>
  
</style>
