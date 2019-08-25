<template>
    <div id="app">
        <v-app style="background: #EDE7F6">
            <Header />
            <FormCreate />
            <HelpButton />
        </v-app>
    </div>
</template>

<script>
import Header from '@/components/include/Header'
import FormCreate from '@/components/forms/FormCreate'
import HelpButton from '@/components/include/HelpButton'

export default {
    name: 'App',
    components: {
        Header,
        FormCreate,
        HelpButton,
    },
};
</script>

<style scoped>
</style>
