<template>
    <v-container fluid class="pa-0; container-wrapper">
        <v-layout>
            <div class="search-wrapper">
                <v-text-field v-model="search" outlined label="Search Name / Description"></v-text-field>

                <v-select
                        v-model="selectedCategory"
                        :items="categories"
                        label="Select Category"
                        item-text="name"
                        item-value="id"
                        outlined>
                </v-select>

                <div>Price Range</div>
                <form>
                    <input v-model="priceRange" type="range" class="slider" name="amountRange" min="0"
                           max="10000" value="0" oninput="this.form.amountInput.value=this.value"/>
                    <input v-model="priceRange" type="text" class="text" readonly name="amountInput" min="0"
                           max="10000" value="0" oninput="this.form.amountRange.value=this.value"/>
                </form>

                <v-btn class="clear-btn" @click="clearFilter">Clear Filter</v-btn>

            </div>

            <grid-layout-component :experiences-list="filteredList"></grid-layout-component>
        </v-layout>
    </v-container>
</template>

<script>
    import GridLayoutComponent from "./gridLayoutComponent.vue";
    import axios from "axios";

    export default {
        name: "experiences",
        components: {
            GridLayoutComponent
        },
        data() {
            return {
                list: [],
                categories: [
                    {id: 'animals', name: 'Animals'},
                    {id: 'sport', name: 'Sport'},
                    {id: 'brain games', name: 'Brain games'}
                ],
                search: '',
                selectedCategory: null,
                priceRange: 0,
            }
        },

        computed: {
            filteredList() {
                return this.list.filter(post => {
                    if (this.selectedCategory) {
                        if (this.priceRange) {
                            return (post.name.toLowerCase().includes(this.search.toLowerCase()) || post.desc.toLowerCase().includes(this.search.toLowerCase())) && post.category.toLowerCase().includes(this.selectedCategory.toLowerCase()) && post.price <= this.priceRange
                        } else {
                            return (post.name.toLowerCase().includes(this.search.toLowerCase()) || post.desc.toLowerCase().includes(this.search.toLowerCase())) && post.category.toLowerCase().includes(this.selectedCategory.toLowerCase())
                        }
                    } else if (this.priceRange) {
                        if (this.selectedCategory) {
                            return post.name.toLowerCase().includes(this.search.toLowerCase()) || post.desc.toLowerCase().includes(this.search.toLowerCase())(post.name.toLowerCase().includes(this.search.toLowerCase())
                                || post.desc.toLowerCase().includes(this.search.toLowerCase())) && post.category.toLowerCase().includes(this.selectedCategory.toLowerCase()) && post.price <= this.priceRange
                        } else {
                            return (post.name.toLowerCase().includes(this.search.toLowerCase()) || post.desc.toLowerCase().includes(this.search.toLowerCase())) && post.price <= this.priceRange
                        }
                    } else {
                        return post.name.toLowerCase().includes(this.search.toLowerCase()) || post.desc.toLowerCase().includes(this.search.toLowerCase())

                    }
                })
            },

        },
        methods: {
            clearFilter() {
                this.priceRange = null;
                this.selectedCategory = '';
                this.search = '';
            }
        },
        mounted() {
            let self = this;
            axios.get("/metadata/dummyData.json")
                .then((response) => {
                    console.log('response', response)
                    response.data.forEach(function (val) {
                        self.list.push({
                            name: val.name,
                            id: val.id,
                            desc: val.desc,
                            category: val.category,
                            price: val.price,
                        });
                    });
                })
                .catch((error) => {
                    console.log(`[ERROR] ${error}`);
                })
        }
    }
</script>

<style scoped>
    .container-wrapper {
        margin-top: 20px;
    }

    .search-wrapper {
        margin-left: 50px;
        margin-top: 15px;
        min-width: 250px;
    }

    .slider {
        min-width: 78%;
    }

    .text {
        max-width: 20%;
        padding: 1%;
    }

    .clear-btn {
        margin: 10%;
    }
</style>