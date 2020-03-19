<template>
    <v-container class="grid-container">
        <v-layout row wrap>
            <v-flex xs12 md4 v-for="item in experiencesList" v-bind:key="item.id">
                <one-experience
                        :name="item.name"
                        :category="item.category"
                        :description="item.desc"
                        :price="item.price">
                </one-experience>
            </v-flex>
        </v-layout>
    </v-container>
</template>

<script>
    import OneExperience from "./oneExperience";

    export default {
        name: "gridLayoutComponent",
        props: {
            experiencesList: {
                type: Array,
                required: true
            },
        },
        components: {OneExperience},


    }
</script>

<style scoped>
    .grid-container {
        margin-right: 40px;
        margin-left: 10px;
    }


</style>