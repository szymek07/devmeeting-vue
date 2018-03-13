<!--10- 1. There's a <template> part -->
<template>
  <div id="app">
    <h2>My awesome list</h2>
    <ul>
      <li v-for="(p, index) in products" v-bind:key="p.id">{{ p.name }}   <button v-on:click="removeItem( index )">Remove</button></li>
    </ul>
    <p v-if="!products.length">No products!</p>


    <form @submit.prevent="onSubmit()">
      <input name="product" v-model="newProduct.name" v-validate="'required|min:3'">
      <button>Add</button>
      <div v-show="errors.has('product')">
        {{ errors.first('product') }}
      </div>
    </form>

    <hr />

    <!--<div>-->
        <!--<select name="order" v-model="selected">-->
        <!--<option v-for="p in products" v-bind:value="p"  >{{ p.name }}</option>-->
        <!--</select>-->
        <!--<button v-on:click="addToOrderList()">Add</button>-->


        <!--<br/>-->
        <!--Orders:-->
        <!--<ul>-->
            <!--<li v-for="o in orders" > {{o.id}}: {{ o.name }}  </li>-->
        <!--</ul>-->
    <!--</div>-->

      <div>
          <form @submit.prevent="addToOrderList()">
              <select name="order" v-model="selected" v-validate="'required'">-->
                <option v-for="p in products" v-bind:value="p" >{{ p.name }}</option>
              </select>
              <button>Add order</button>
              <div v-show="errors.has('order')">
                  {{ errors.first('order') }}
              </div>
          </form>
          <br/>
          Orders:
          <ul>
          <!-- 2. Then, we're using built-in v-for directive to iterate over products -->
          <li v-for="o in orders" > {{o.id}}: {{ o.name }}  </li>
          </ul>
      </div>

  </div>
</template>

<!--21- 2. A <script> part -->
<script>
    import uuid from 'uuid/v4';

    // 4. Now App is not mounted itself, we're just creating a component (more on that later - hold your horses!)
    export default {
        name: 'app',
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
                newProduct: {
                    name: ''
                },
                selected: '',
                orders: []
            }
        },
        methods: {
            onSubmit() {
                this.$validator.validate('product').then(result => {
                    if (!result) {
                        return;
                    }
                    this.products.push({
                        id: uuid(),
                        ...this.newProduct
                    });

                    this.newProduct.name = '';
                    // 4/ and reset validation state after adding a product
                    this.$validator.reset();
                });
            },

            removeItem(index) {
                console.log(index);
                this.products.splice(index, 1);
            },

            addToOrderList() {

                this.$validator.validate('order').then(result => {
                    if (!result) {
                        return;
                    }

                    console.log(this.selected);
                    this.orders.push(this.selected);
                    this.selected = '';
                    console.log(this.orders);

                    this.selected = '';
                    // 4/ and reset validation state after adding a product
                    this.$validator.reset();
                });


            }
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
