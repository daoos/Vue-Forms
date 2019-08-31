<template>
  <div id="app">
      <v-app v-bind:style="{ background: background_color }">
          <Header 
            @changeThemeColor="(...args) => changeThemeColor(...args)"
            @changeBackgroundColor="(...args) => changeBackgroundColor(...args)"  />
          <PageForm :theme_color="theme_color" />
          <HelpButton />
      </v-app>
  </div>
</template>

<script>
import Header from '@/components/include/Header'
import PageForm from '@/components/pages/PageForm'
import HelpButton from '@/components/include/HelpButton'

export default {
    name: 'App',
    components: {
        Header,
        PageForm,
        HelpButton,
    },
    data() {
      return {
        theme_color: 'deep-purple darken-1',
        background_color: '#EDE7F6',
      }
    },
    methods: {
      changeThemeColor(args) {
        this.theme_color = args
      },
      changeBackgroundColor(args) {
        this.background_color = args
      },
    }
};
</script>

<style>
    /* Glocal settings here */
    * {
        text-transform: none !important;
    }
</style>
