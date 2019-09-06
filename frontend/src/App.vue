<template>
  <div id="app">
      <v-app v-bind:style="{ background: backgroundColor }">
          <Header 
            @changeThemeColor="(...args) => changeThemeColor(...args)"
            @changeBackgroundColor="(...args) => changeBackgroundColor(...args)"  />
          <PageForm :themeColor="themeColor" />
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
        themeColor: 'deep-purple darken-1',
        backgroundColor: '#EDE7F6',
      }
    },
    methods: {
      changeThemeColor(args) {
        this.themeColor = args
      },
      changeBackgroundColor(args) {
        this.backgroundColor = args
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
