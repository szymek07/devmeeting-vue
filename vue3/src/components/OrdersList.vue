<template>
    <div>
        Orders:
        <ul>
            <!-- 2. Then, we're using built-in v-for directive to iterate over products -->
            <li v-for="o in orders" > {{o.id}}: {{ o.name }}  </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "OrdersList",

        props: {
            // Here we also added some basic props validation
            orders: {
                type: Array,
            }
        }
    }
</script>

<style scoped>

</style>