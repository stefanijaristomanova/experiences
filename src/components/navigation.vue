<template>
    <v-app-bar
            dense
            dark
            app
    >

        <v-toolbar-title class="toolbar-title">Activity Center </v-toolbar-title>

            <v-tabs
                    dark
            >
                <v-tab> Experiences </v-tab>
                <v-tab> Tab 1 </v-tab>
                <v-tab> Tab 2 </v-tab>
    </v-tabs>

    </v-app-bar>
</template>

<script>
    export default {
        name: 'navigation',
    }
</script>

<style>
    .toolbar-title {
        width: 150px;
    }
</style>
