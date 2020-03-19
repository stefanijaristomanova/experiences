<template>
    <v-card class="card" raised>
        <div>Experience Name: <b> {{name}} </b></div>
        <br>
        <div><i> {{description}} </i></div>
        <br>
        <div> Category: {{category}}</div>
        <div> Price ${{price}}</div>
    </v-card>
</template>

<script>
    export default {
        name: "oneExperience",
        props: {
            name: {
                type: String,
                required: true
            },
            description: {
                type: String,
                required: true
            },
            category: {
                type: String,
                required: true
            },
            price: {
                type: Number,
                required: true
            }
        },
    }
</script>

<style scoped>
    .card {
        min-heigth: 40%;
        min-width: 70px;
        margin: 0px 20px 20px 20px;
    }
</style>