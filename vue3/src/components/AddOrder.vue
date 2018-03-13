<template>
    <form @submit.prevent="addToOrderList()">
        <select name="order" v-model="selected" v-validate="'required'">-->
            <option v-for="p in products" v-bind:value="p" >{{ p.name }}</option>
        </select>
        <button>Add order</button>
        <div v-show="errors.has('order')">
            {{ errors.first('order') }}
        </div>
    </form>
</template>

<script>
    export default {
        name: "AddOrder",

        props: {
            // Here we also added some basic props validation
            products: {
                type: Array,
            }
        },

        data() {
            return {
                selected: ''
            }
        },

        methods: {
            addToOrderList() {

                this.$validator.validate('order').then(result => {
                    if (!result) {
                        return;
                    }

                    console.log(this.selected);

                    this.$emit('onAddOrder', this.selected);

                    // this.orders.push(this.selected);
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

<style scoped>

</style>