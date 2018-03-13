<template>
    <form @submit.prevent="onSubmit()">
        <input name="product" v-model="newProduct.setup" v-validate="'required|min:3'">
        <button>Add</button>
        <div v-show="errors.has('product')">
            {{ errors.first('product') }}
        </div>
    </form>
</template>

<script>
    import uuid from 'uuid/v4';

    export default {
        name: "AddProduct",

        data() {
            return {
                newProduct: {
                    setup: ''
                }
            }
        },

        methods: {
            onSubmit() {
                this.$validator.validate('product').then(result => {
                    if (!result) {
                        return;
                    }
                    // this.products.push({
                    //     id: uuid(),
                    //     ...this.newProduct
                    // });

                    this.$emit('onAddProduct', {
                        id: uuid(),
                        ...this.newProduct
                    });

                    this.newProduct.name = '';
                    // 4/ and reset validation state after adding a product
                    this.$validator.reset();
                });
            }
        }
    }
</script>

<style scoped>

</style>