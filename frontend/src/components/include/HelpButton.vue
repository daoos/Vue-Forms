<template>
	<div class="fixed-button">
    <v-tooltip left>
      <template v-slot:activator="{ on }">
        <v-btn 
          icon
          v-on="on">
          <v-icon>mdi-help-circle</v-icon>
        </v-btn>
      </template>
      <span class="tooltip">Help & feedback</span>
    </v-tooltip>
	</div>
</template>

<script>
	
</script>

<style scoped>
  .fixed-button {
    position: fixed;
    bottom: 10px;
    right: 10px;
  }
</style>
