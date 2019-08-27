<template>
  <div id="app">
      <v-app style="background: #EDE7F6">
          <Header />
          <PageForm />
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
};
</script>

<style>
    /* Glocal settings here */
    * {
        text-transform: none !important;
    }
</style>
