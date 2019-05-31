<template>
    <div id="app">
        <b-container>
            <b-row>
                <b-col cols="12">
                    <h1>Общая сумма товаров в корзине: {{ totalPrice }}</h1>
                </b-col>
            </b-row>
            <b-form @submit="onSubmit">
                <b-row>
                    <b-col cols="8">
                        <div class="products">
                            <template v-for="product in products">
                                <b-row>
                                    <b-col cols="6">
                                        <b-form-group id="input-group-2" label-for="input-2">
                                            <b-form-input id="input-2" v-model="product.name" required placeholder="Product name"></b-form-input>
                                        </b-form-group>
                                    </b-col>
                                    <b-col cols="3">
                                        <b-form-group id="input-group-2" label-for="input-2">
                                            <b-form-input id="input-2" v-model="product.price" required placeholder="Product price"></b-form-input>
                                        </b-form-group>
                                    </b-col>
                                    <b-col cols="2">
                                        <b-form-group id="input-group-2" label-for="input-2">
                                            <b-form-input id="input-2" v-model="product.number" type="number" required placeholder="Enter name"></b-form-input>
                                        </b-form-group>
                                    </b-col>
                                    <b-col cols="1">
                                        <b-button type="button" variant="danger"  @click="removeProduct(product.id)">-</b-button>
                                    </b-col>
                                </b-row>
                            </template>
                            <b-button type="button" variant="primary" @click="addProduct">Add product</b-button>
                        </div>
                    </b-col>
                    <b-col cols="4">
                        <b-form-group id="input-group-2">
                            <b-form-input id="input-2" v-model="form.name" required placeholder="Enter name"></b-form-input>
                        </b-form-group>
                        <b-form-group id="input-group-2">
                            <b-form-input id="input-2" v-model="form.name" required placeholder="Enter phone"></b-form-input>
                        </b-form-group>
                        <b-form-group id="input-group-1">
                            <b-form-input id="input-1" v-model="form.email" type="email" required placeholder="Enter email"></b-form-input>
                        </b-form-group>
                    </b-col>
                </b-row>
                <b-row>
                    <b-col md="1" offset="5" class="mt-3">
                        <b-button type="submit" variant="primary">Submit</b-button>
                    </b-col>
                </b-row>
            </b-form>
        </b-container>
        <b-card class="mt-3" header="Result">
            <pre class="m-0">{{ form }}</pre>
            <pre class="m-0">{{ products }}</pre>
        </b-card>
    </div>
</template>
<script>
import Cart from './components/Cart.vue'

export default {
    name: 'app',
    data() {
        return {
            form: {
                email: '',
                name: '',
                phone: '',
            },
            products: [{
                id: 1,
                name: "Jeans",
                number: 1,
                price: 1200
            }, ],
            nextProductId: 2,
            show: true
        }
    },
    methods: {
        onSubmit(evt) {
            evt.preventDefault()
            alert(JSON.stringify(this.form))
        },
        addProduct() {
            console.log(this);
            this.products.push({
                id: this.nextProductId,
                name: "",
                number: 1,
                price: 0
            })
            this.nextProductId = this.nextProductId + 1;
        },
        removeProduct(id) {
            this.products = this.products.filter(product => {
                return product.id !== id
            })
        }
    },
    computed: {
        totalPrice: function() {
            return this.products.reduce((sum, product) => {
                return sum + (product.price * product.number)
            }, 0)
        }
    }
}
</script>
<style lang="scss">
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

.products {
    border: 1px solid #bbbbbb88;
    padding: 5px;
    border-radius: 4px;
}
</style>