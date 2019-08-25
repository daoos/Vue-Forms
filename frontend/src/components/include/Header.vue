<template>
	<div>
		<v-app-bar
			color="deep-purple darken-1"
			flat
			dark
			>

			<v-btn icon>
				<v-icon>mdi-arrow-left</v-icon>
			</v-btn>

			<v-toolbar-title class="font-weight-bold">Untitled form</v-toolbar-title>

			<v-btn icon>
				<v-icon>mdi-folder</v-icon>
			</v-btn>

			<v-btn icon>
				<v-icon>mdi-star-outline</v-icon>
			</v-btn>

			<div class="font-italic caption" style="color: #D1C4E9">All changes saved in Drive</div>

			<div class="flex-grow-1"></div>

			<v-btn icon>
				<v-icon>mdi-palette</v-icon>
			</v-btn>

			<v-btn icon>
				<v-icon>mdi-eye</v-icon>
			</v-btn>

			<v-btn icon>
				<v-icon>mdi-settings</v-icon>
			</v-btn>

			<v-btn icon>
				<v-icon>mdi-send</v-icon>
			</v-btn>

			<v-menu
				left
				bottom
			>
				<template v-slot:activator="{ on }">
					<v-btn icon v-on="on">
						<v-icon>mdi-dots-vertical</v-icon>
					</v-btn>
				</template>

				<v-list>
					<v-list-item
						v-for="n in 5"
						:key="n"
						@click="() => {}"
					>
					<v-list-item-title>Option {{ n }}</v-list-item-title>
					</v-list-item>
				</v-list>
			</v-menu>

			<v-btn icon>
				<v-icon>mdi-account-circle</v-icon>
			</v-btn>

		</v-app-bar>
	</div>
</template>

<script>
	
</script>

<style scoped>

</style>
