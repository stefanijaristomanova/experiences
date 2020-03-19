<template>
    <v-app>
        <navigation></navigation>
        <v-content>
            <experiences></experiences>
        </v-content>
        <Footer></Footer>
    </v-app>
</template>

<script>
    import Navigation from "./components/navigation.vue";
    import Footer from "./components/footer.vue";
    import Experiences from "./components/experiences.vue";

    export default {
        name: 'App',
        components: {
            Experiences,
            Navigation,
            Footer,
        },
    };
</script>