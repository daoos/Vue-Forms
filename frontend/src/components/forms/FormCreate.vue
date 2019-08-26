<template>
	<div class="container">
		<v-card>
			<v-tabs
				background-color="white"
				color="deep-purple darken-1"
				slider-color="deep-purple darken-1"
				centered>

				<v-tabs-slider></v-tabs-slider>

				<v-tab href="question">
					Questions
				</v-tab>

				<v-tab href="response">
					Response
				</v-tab>

			</v-tabs>

			<v-form>
				<v-container>
					<v-row>
						<v-col>
							<v-text-field v-model="question.title"/>
							<v-text-field placeholder="Form description" />
						</v-col>
					</v-row>
				</v-container>
			</v-form>

			<v-card 
				class="form-editor" 
				width="36">
				<v-row>
					<v-col>
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn 
                  icon
                  v-on="on">
                  <v-icon>mdi-plus-circle</v-icon>
                </v-btn>
              </template>
              <span class="tooltip">Add question</span>
            </v-tooltip>
					</v-col>
				</v-row>
				<v-row>
					<v-col>
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn 
                  icon
                  v-on="on">
                  <v-icon>mdi-import</v-icon>
                </v-btn>
              </template>
              <span class="tooltip">Import questions</span>
            </v-tooltip>
					</v-col>
				</v-row>
				<v-row>
					<v-col>
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn 
                  icon
                  v-on="on">
                  <v-icon>mdi-format-title</v-icon>
                </v-btn>
              </template>
              <span class="tooltip">Add title and description</span>
            </v-tooltip>
					</v-col>
				</v-row>
				<v-row>
					<v-col>
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn 
                  icon
                  v-on="on">
                  <v-icon>mdi-image</v-icon>
                </v-btn>
              </template>
              <span class="tooltip">Add image</span>
            </v-tooltip>
					</v-col>
				</v-row>
				<v-row>
					<v-col>
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn 
                  icon
                  v-on="on">
                  <v-icon>mdi-youtube</v-icon>
                </v-btn>
              </template>
              <span class="tooltip">Add video</span>
            </v-tooltip>
					</v-col>
				</v-row>
				<v-row>
					<v-col>
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn 
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

		</v-card>
	</div>
</template>

<script>
	export default {
    components: {

    },
    data() {
      return {
        question: {
          title: 'Untitled form',
          description: '',
        }
      }
    }
  }
</script>

<style scoped>
	.container {
		max-width: 770px;
	}

	/* 50px right to the parent element (v-card) */
	.form-editor {
		position: absolute;
		top: 0px;
		right: -50px;
	}
</style>
