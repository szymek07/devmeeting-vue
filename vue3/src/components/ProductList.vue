<template>
    <div>
        <ul>
            <li v-for="(p, index) in products" v-bind:key="p.id">{{ p.name }}   <button v-on:click="removeItem( index )">Remove</button></li>
        </ul>
        <p v-if="!products.length">No products!</p>
    </div>
</template>

<script>
    export default {
        name: "ProductList",
        // The case is, we have to define props (inputs)
        props: {
            // Here we also added some basic props validation
            products: {
                type: Array,
            }
        }
    }
</script>

<style scoped>

</style>