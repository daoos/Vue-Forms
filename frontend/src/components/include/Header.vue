<template>
	<div>
		<v-app-bar
			color="deep-purple darken-1"
			flat
			dark
			>

      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
    			<v-btn 
            icon
            v-on="on">
    				<v-icon>mdi-arrow-left</v-icon>
    			</v-btn>
        </template>
        <span class="tooltip">Forms Home</span>
      </v-tooltip>

			<v-toolbar-title class="font-weight-bold">Untitled form</v-toolbar-title>

      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <v-btn 
            icon
            v-on="on">
            <v-icon>mdi-folder</v-icon>
          </v-btn>
        </template>
        <span class="tooltip">Folder</span>
      </v-tooltip>

      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <v-btn 
            icon
            v-on="on">
            <v-icon>mdi-star-outline</v-icon>
          </v-btn>
        </template>
        <span class="tooltip">Star</span>
      </v-tooltip>

			<v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <span
            class="font-italic caption" 
            style="color: #D1C4E9"
            v-on="on">
            All changes saved in Drive
          </span>
        </template>
        <span class="tooltip">Every change you make is automatically saved in Drive.</span>
      </v-tooltip>

			<div class="flex-grow-1"></div>

      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
			    <v-btn 
            icon
            v-on="on">
				    <v-icon>mdi-palette</v-icon>
			    </v-btn>
        </template>
        <span class="tooltip">Customize Theme</span>
      </v-tooltip>

      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <v-btn 
            icon
            v-on="on">
            <v-icon>mdi-eye</v-icon>
          </v-btn>
        </template>
        <span class="tooltip">Preview</span>
      </v-tooltip>

      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <v-btn 
            icon
            v-on="on">
            <v-icon>mdi-settings</v-icon>
          </v-btn>
        </template>
        <span class="tooltip">Settings</span>
      </v-tooltip>

      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <v-btn 
            icon
            v-on="on">
            <v-icon>mdi-send</v-icon>
          </v-btn>
        </template>
        <span class="tooltip">Send</span>
      </v-tooltip>

			<v-menu
				left
				bottom
			>
				<template v-slot:activator="{ on }">
					<v-btn 
            icon 
            v-on="on">
						<v-icon>mdi-dots-vertical</v-icon>
					</v-btn>
				</template>

				<v-list>
					<v-list-item
						v-for="n in 5"
						:key="n"
						@click="() => {}"
					>
          <v-list-item-icon>
            <v-icon>mdi-undo</v-icon>
          </v-list-item-icon>
					<v-list-item-title>Option {{ n }}</v-list-item-title>
					</v-list-item>
				</v-list>
			</v-menu>

      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <v-btn 
            icon
            v-on="on">
            <v-icon>mdi-account-circle</v-icon>
          </v-btn>
        </template>
        <span class="tooltip">Google Account</span>
      </v-tooltip>

		</v-app-bar>
	</div>
</template>

<script>
	
</script>

<style scoped>
  .tooltip {
    font-size: 12px;
  }
</style>
