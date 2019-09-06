<template>
  <v-navigation-drawer
    v-bind:value="value"
    v-on:input="$emit('input', $event)"
    absolute
    temporary
    right
    hide-overlay>
    <v-list>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title 
            v-bind:style="{ color: themeColorList[themeColor] }"
            >THEME OPTIONS
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
    <v-divider></v-divider>
    <v-list nav dense>
      <v-list-item>
        <span class="nav-item-text">HEADER</span>
      </v-list-item>
      <v-list-item>
        <v-btn color="white">
          <v-icon
            color="grey darken-1" 
            left>mdi-image</v-icon> 
            <span class="nav-item-text">Choose image</span>
        </v-btn>
      </v-list-item>
    </v-list>
    <v-divider></v-divider>
    <v-list>
      <v-list-item>
        <span class="nav-item-text">THEME COLOR</span>
      </v-list-item>
      <v-list-item>
        <v-btn
          color="red darken-1" 
          fab
          depressed
          x-small
          @click="changeThemeColor('red darken-1')">
          <v-icon
            v-if="isCurrentThemeColor('red darken-1')" 
            color="white">mdi-check-bold</v-icon>
        </v-btn>
        <v-btn
          class="theme-color"
          color="deep-purple darken-1" 
          fab
          depressed
          x-small
          @click="changeThemeColor('deep-purple darken-1')">
          <v-icon
            v-if="isCurrentThemeColor('deep-purple darken-1')" 
            color="white">mdi-check-bold</v-icon>
        </v-btn>
        <v-btn
          class="theme-color"
          color="indigo darken-1" 
          fab 
          depressed
          x-small
          @click="changeThemeColor('indigo darken-1')">
          <v-icon
            v-if="isCurrentThemeColor('indigo darken-1')" 
            color="white">mdi-check-bold</v-icon>
        </v-btn>
        <v-btn
          class="theme-color" 
          color="blue darken-1" 
          fab 
          depressed
          x-small
          @click="changeThemeColor('blue darken-1')">
          <v-icon
            v-if="isCurrentThemeColor('blue darken-1')" 
            color="white">mdi-check-bold</v-icon>
        </v-btn>
        <v-btn
          class="theme-color" 
          color="light-blue darken-1" 
          fab 
          depressed
          x-small
          @click="changeThemeColor('light-blue darken-1')">
          <v-icon
            v-if="isCurrentThemeColor('light-blue darken-1')" 
            color="white">mdi-check-bold</v-icon>
        </v-btn>
        <v-btn
          class="theme-color" 
          color="cyan darken-1" 
          fab 
          depressed
          x-small
          @click="changeThemeColor('cyan darken-1')">
          <v-icon
            v-if="isCurrentThemeColor('cyan darken-1')" 
            color="white">mdi-check-bold</v-icon>
        </v-btn>
      </v-list-item>
      <v-list-item>
        <v-btn 
          color="deep-orange darken-1" 
          fab 
          depressed
          x-small
          @click="changeThemeColor('deep-orange darken-1')">
          <v-icon
            v-if="isCurrentThemeColor('deep-orange darken-1')" 
            color="white">mdi-check-bold</v-icon>
        </v-btn>
        <v-btn
          class="theme-color" 
          color="orange darken-1" 
          fab 
          depressed
          x-small
          @click="changeThemeColor('orange darken-1')">
          <v-icon
            v-if="isCurrentThemeColor('orange darken-1')" 
            color="white">mdi-check-bold</v-icon>
        </v-btn>
        <v-btn
          class="theme-color" 
          color="teal darken-1" 
          fab 
          depressed
          x-small
          @click="changeThemeColor('teal darken-1')">
          <v-icon
            v-if="isCurrentThemeColor('teal darken-1')" 
            color="white">mdi-check-bold</v-icon>
        </v-btn>
        <v-btn
          class="theme-color" 
          color="green darken-1" 
          fab 
          depressed
          x-small
          @click="changeThemeColor('green darken-1')">
          <v-icon
            v-if="isCurrentThemeColor('green darken-1')" 
            color="white">mdi-check-bold</v-icon>
        </v-btn>
        <v-btn
          class="theme-color" 
          color="blue-grey darken-1" 
          fab 
          depressed
          x-small
          @click="changeThemeColor('blue-grey darken-1')">
          <v-icon
            v-if="isCurrentThemeColor('blue-grey darken-1')" 
            color="white">mdi-check-bold</v-icon>
        </v-btn>
        <v-btn
          class="theme-color" 
          color="grey darken-1" 
          fab 
          depressed
          x-small
          @click="changeThemeColor('grey darken-1')">
          <v-icon
            v-if="isCurrentThemeColor('grey darken-1')" 
            color="white">mdi-check-bold</v-icon>
        </v-btn>
      </v-list-item>
      <v-list-item>
        <v-tooltip left>
          <template v-slot:activator="{ on }">
            <v-btn 
              color="grey lighten-2" 
              fab 
              depressed
              x-small
              v-on="on">
              <v-icon color="grey darken-1">mdi-plus</v-icon>
            </v-btn>
          </template>
          <span class="tooltip">Add custom color</span>
        </v-tooltip>
      </v-list-item>
    </v-list>
    <v-divider></v-divider>
    <v-list>
      <v-list-item>
        <span class="nav-item-text">BACKGROUND COLOR</span>
      </v-list-item>
      <v-list-item>
        <v-btn
          v-for="(color, index) in backgroundColorList[themeColor]"
          class="background-color"
          :color="color" 
          fab
          depressed
          x-small
          @click="changeBackgroundColor(color)">
          <v-icon v-if="isCurrentBackgroundColor(color)">mdi-check-bold</v-icon>
        </v-btn>
        <v-btn
          class="background-color"
          color="#F6F6F6" 
          fab
          depressed
          x-small
          @click="changeBackgroundColor('#F6F6F6')">
          <v-icon
            v-if="isCurrentBackgroundColor('#F6F6F6')" 
            color="white">mdi-check-bold</v-icon>
        </v-btn>
      </v-list-item>
    </v-list>
    <v-divider></v-divider>
    <v-list>
      <v-list-item>
        <span class="nav-item-text">FONT STYLE</span>
      </v-list-item>
      <v-list-item>
        <v-select
          v-model="selectedFont"
          :items="fontList"
          :item-text="selectedFont"
          :item-value="selectedFont"
          single-line>
        </v-select>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>  
</template>

<script>
  export default {
    props: {
      value: {
        type: Boolean,
        default: false,
      },
    },
    data() {
      return {
        themeColor: 'deep-purple darken-1',
        backgroundColor: '#EDE7F6',
        selectedFont: 'Basic',
        themeColorList: {
          'red darken-1': '#E53935',
          'deep-purple darken-1': '#5E35B1',
          'indigo darken-1': '#3949AB',
          'blue darken-1': '#1E88E5',
          'light-blue darken-1': '#039BE5',
          'cyan darken-1': '#00ACC1',
          'deep-orange darken-1': '#F4511E',
          'orange darken-1': '#FB8C00',
          'teal darken-1': '#00897B',
          'green darken-1': '#43A047',
          'blue-grey darken-1': '#546E7A',
          'grey darken-1': '#757575',
        },
        backgroundColorList: {
          'red darken-1': ['#FFEBEE', '#FFCDD2', '#EF9A9A'],
          'deep-purple darken-1': ['#EDE7F6', '#D1C4E9', '#B39DDB'],
          'indigo darken-1': ['#E8EAF6', '#C5CAE9', '#9FA8DA'],
          'blue darken-1': ['#E3F2FD', '#BBDEFB', '#90CAF9'],
          'light-blue darken-1': ['#E1F5FE', '#B3E5FC', '#81D4FA'],
          'cyan darken-1': ['#E0F7FA', '#B2EBF2', '#80DEEA'],
          'deep-orange darken-1': ['#FBE9E7', '#FFCCBC', '#FFAB91'],
          'orange darken-1': ['#FFF3E0', '#FFE0B2', '#FFCC80'],
          'teal darken-1': ['#E0F2F1', '#B2DFDB', '#80CBC4'],
          'green darken-1': ['#E8F5E9', '#C8E6C9', '#A5D6A7'],
          'blue-grey darken-1': ['#ECEFF1', '#CFD8DC', '#B0BEC5'],
          'grey darken-1': ['#FAFAFA', '#F5F5F5', '#EEEEEE'],
        },
        fontList : ['Basic', 'Formal', 'Decorative', 'Playful'],      
      }
    },
    methods: {
      changeThemeColor(color) {
        this.themeColor = color
        this.backgroundColor = this.backgroundColorList[color][0]
        this.$emit('changeThemeColor', color)
        this.$emit('changeBackgroundColor', this.backgroundColorList[color][0])
      },
      changeBackgroundColor(color) {
        this.backgroundColor = color
        this.$emit('changeBackgroundColor', color)
      },
      isCurrentThemeColor(currentColor) {
        if (this.themeColor == currentColor) {
          return true
        } else {
          return false
        }
      },
      isCurrentBackgroundColor(currentColor) {
        if (this.backgroundColor == currentColor) {
          return true
        } else {
          return false
        }
      },
    }
  }
</script>

<style scoped>
  .theme-color, .background-color {
    margin-left: 5px;
  }
  .nav-item-text {
    color: #757575;
  } 
  .tooltip {
    font-size: 12px;
  }
</style>
