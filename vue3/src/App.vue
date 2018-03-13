<!--10- 1. There's a <template> part -->
<template>
  <div id="app">
    <h2>My awesome list</h2>
    <product-list :products="products"></product-list>

    <add-product @onAddProduct="handleAddProduct"></add-product>



    <hr />



    <orders-list :orders="orders"></orders-list>
    <add-order :products="products" @onAddOrder="handleAddOrder"></add-order>
  </div>
</template>

<!--21- 2. A <script> part -->
<script>
    import uuid from 'uuid/v4';

    import ProductList from './components/ProductList';
    import AddProduct from './components/AddProduct';
    import OrdersList from './components/OrdersList';
    import AddOrder from './components/AddOrder';

    // 4. Now App is not mounted itself, we're just creating a component (more on that later - hold your horses!)
    export default {
        name: 'app',

        components: {
            OrdersList,
            ProductList,
            AddProduct,
            AddOrder
        },

        //11/ 5. Data can no longer be just an object to prevent accidental shared state
        data() {
            return {
                products: [{
                    id: uuid(),
                    name: 'Coffee'
                }, {
                    id: uuid(),
                    name: 'Pizza'
                }],
                orders: []
            }
        },
        methods: {
            handleAddProduct(product) {
                this.products.push(product);
            },

            handleAddOrder(order) {
                this.orders.push(order);
            },

            removeItem(index) {
                console.log(index);
                this.products.splice(index, 1);
            },


        }
    }
</script>

<!--9- 3. And <style> part -->
<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
