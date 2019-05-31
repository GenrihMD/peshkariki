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
                                        <b-form-group :id="'product__name-' + product.id" label-for="input-2">
                                            <b-form-input v-model="product.name" required placeholder="Product name"></b-form-input>
                                        </b-form-group>
                                    </b-col>
                                    <b-col cols="3">
                                        <b-form-group :id="'product__price-' + product.id" label-for="input-2">
                                            <b-form-input v-model="product.price" type="number" required placeholder="Product price"></b-form-input>
                                        </b-form-group>
                                    </b-col>
                                    <b-col cols="2">
                                        <b-form-group :id="'product__total-' + product.id" label-for="input-2">
                                            <b-form-input v-model="product.number" type="number" required placeholder="Enter name"></b-form-input>
                                        </b-form-group>
                                    </b-col>
                                    <b-col cols="1">
                                        <b-button type="button" variant="danger" @click="removeProduct(product.id)">-</b-button>
                                    </b-col>
                                </b-row>
                            </template>
                            <b-button type="button" variant="primary" @click="addProduct">Add product</b-button>
                        </div>
                    </b-col>
                    <b-col cols="4">
                        <b-form-group>
                            <b-form-input 
                                v-model="form.name" 
                                required 
                                placeholder="Enter name"
                            ></b-form-input>
                        </b-form-group>
                        <b-form-group>
                            <b-form-input 
                                v-model="form.phone" 
                                @blur="isPhoneTouched = true" 
                                type="tel" 
                                required 
                                placeholder="Enter phone"
                            ></b-form-input>
                        </b-form-group>
                        <b-form-group>
                            <b-form-input 
                                :class="{error : isEmailError}" 
                                v-model="form.email" 
                                @blur="isEmailTouched = true" 
                                type="email" 
                                required 
                                placeholder="Enter email"
                            ></b-form-input>
                        </b-form-group>
                    </b-col>
                </b-row>
                <b-row>
                    <b-col md="1" offset="5" class="mt-3">
                        <b-button type="submit" variant="primary" :disabled="!isEmailValid">Submit</b-button>
                    </b-col>
                </b-row>
            </b-form>
        </b-container>        
        <div>
            <b-modal ref="bv-modal-thanx" id="bv-modal-thanx" hide-footer>
                <div class="d-block text-center">
                    <h3>Data sent!</h3>
                </div>
                <b-button class="mt-3" block @click="hideModal">Thanx</b-button>
            </b-modal>
        </div>
    </div>
</template>
<script>
import Cart from './components/Cart.vue'
let emailCheckRegex = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
let phoneCheckRegex = /^((\+7|7|8)+([0-9]){10})$/;

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
            isEmailTouched: false,
            isPhoneTouched: false
        }
    },
    methods: {
        onSubmit(evt) {
            evt.preventDefault()
            let data = {
                'form': this.form,
                'cart': this.products
            }
            fetch('/post.php', {
                    method: 'post',
                    headers: {
                        'Accept': 'application/json, text/plain, */*',
                        'Content-Type': 'application/json'
                    },
                    body: 'json=' + JSON.stringify(data)
                })
                .then((data) => {
                    this.$refs['bv-modal-thanx'].show()
                })
                .catch((error) => {
                    this.$refs['bv-modal-thanx'].show()
                })
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
        },
        hideModal() {
            this.$refs['bv-modal-thanx'].hide()
        }
    },
    computed: {
        totalPrice: function() {
            return this.products.reduce((sum, product) => {
                return sum + (product.price * product.number)
            }, 0)
        },
        isEmailValid() {
            return emailCheckRegex.test(this.form.email);
        },
        isEmailError() {
            return !this.isEmailValid && this.isEmailTouched;
        },
        isPhoneValid() {
            return phoneCheckRegex.test(this.form.phone);
        },
        isPhoneError() {
            return !this.isPhoneValid && this.isPhoneTouched;
        },
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

.error {
    border-color: red;
}
</style>