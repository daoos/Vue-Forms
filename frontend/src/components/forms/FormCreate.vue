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
							<v-text-field placeholder="Untitled form"/>
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
						<v-btn icon>
							<v-icon>mdi-plus-circle</v-icon>
						</v-btn>
					</v-col>
				</v-row>
				<v-row>
					<v-col>
						<v-btn icon>
							<v-icon>mdi-import</v-icon>
						</v-btn>
					</v-col>
				</v-row>
				<v-row>
					<v-col>
						<v-btn icon>
							<v-icon>mdi-format-title</v-icon>
						</v-btn>
					</v-col>
				</v-row>
				<v-row>
					<v-col>
						<v-btn icon>
							<v-icon>mdi-image</v-icon>
						</v-btn>
					</v-col>
				</v-row>
				<v-row>
					<v-col>
						<v-btn icon>
							<v-icon>mdi-youtube</v-icon>
						</v-btn>
					</v-col>
				</v-row>
				<v-row>
					<v-col>
						<v-btn icon>
							<v-icon>mdi-note-plus</v-icon>
						</v-btn>
					</v-col>
				</v-row>
			</v-card>

		</v-card>
	</div>
</template>

<script>
	
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
