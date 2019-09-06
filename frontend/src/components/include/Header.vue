<template>
  <div>
    <v-app-bar
      :color="themeColor"
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
            v-on="on"
            v-show="$viewport .width > 450">
            <v-icon>mdi-folder</v-icon>
          </v-btn>
        </template>
        <span class="tooltip">Folder</span>
      </v-tooltip>

      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <v-btn 
            icon
            v-on="on"
            v-show="$viewport .width > 450">
            <v-icon @click="isStarred ? isStarred = false : isStarred = true">
              {{ isStarred ? 'mdi-star' : 'mdi-star-outline' }}
            </v-icon>
          </v-btn>
        </template>
        <span class="tooltip">Star</span>
      </v-tooltip>

      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <span
            class="font-italic caption" 
            style="color: #D1C4E9"
            v-on="on"
            v-show="$viewport .width > 450">
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
            v-on="on"
            @click.stop="drawer = !drawer">
            <v-icon>mdi-palette</v-icon>
          </v-btn>
        </template>
        <span class="tooltip">Customize Theme</span>
      </v-tooltip>

      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <v-btn 
            icon
            v-on="on"
            v-show="$viewport .width > 450">
            <v-icon>mdi-eye</v-icon>
          </v-btn>
        </template>
        <span class="tooltip">Preview</span>
      </v-tooltip>

      <DialogSettings :themeColor="themeColor" />

      <DialogSend :themeColor="themeColor" />

      <v-menu
        left
        bottom
      >
        <template v-slot:activator="{ on: menu }">
          <v-tooltip bottom>
            <template v-slot:activator="{ on: tooltip }">
              <v-btn 
                icon 
                v-on="{ ...tooltip, ...menu }">
                  <v-icon>mdi-dots-vertical</v-icon>
              </v-btn>
            </template>
            <span class="tooltip">More</span>
          </v-tooltip>
        </template>

        <v-list>
          <v-list-item
            v-for="(option, index) in options"
            :key="index"
            @click="">
            <v-list-item-icon>
              <v-icon>{{ option.icon }}</v-icon>
            </v-list-item-icon>
            <v-list-item-title>{{ option.name }}</v-list-item-title>
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

    <NavCustomizeThemeColor
      @changeThemeColor="(...args) => changeThemeColor(...args)"
      @changeBackgroundColor="(...args) => changeBackgroundColor(...args)"
      v-model="drawer" />
  </div>
</template>

<script>
  import DialogSettings from '@/components/widgets/dialogs/DialogSettings'
  import DialogSend from '@/components/widgets/dialogs/DialogSend'
  import NavCustomizeThemeColor from '@/components/widgets/navs/NavCustomizeThemeColor'

  export default {
    components: {
      DialogSettings,
      DialogSend,
      NavCustomizeThemeColor,
    },
    data() {
      return {
        options: [
          { name: 'Undo', icon: 'mdi-undo'},
          { name: 'Make a copy', icon: 'mdi-content-copy' },
          { name: 'Move to trash', icon: 'mdi-delete' },
          { name: 'Get pre-filled link', icon: 'mdi-link' },
          { name: 'Print', icon: 'mdi-printer' },
          { name: 'Add collaborators', icon: 'mdi-account-multiple-plus' },
          { name: 'Script editor', icon: 'mdi-code-tags' },
          { name: 'Add-ons', icon: 'mdi-puzzle' },
          { name: 'Preferences', icon: 'mdi-account-settings' },
        ],
        isStarred: false,
        drawer: false,
        themeColor: 'deep-purple darken-1',
      }
    },
    methods: {
      changeThemeColor(args) {
        this.themeColor = args
        this.$emit('changeThemeColor', args)
      },
      changeBackgroundColor(args) {
        this.$emit('changeBackgroundColor', args)
      }
    }
  }
</script>

<style scoped>
  .tooltip {
    font-size: 12px;
  }
</style>
