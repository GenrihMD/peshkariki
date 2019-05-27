<template>
    <div id="app">
        <b-container>
            <b-form @submit="onSubmit" @reset="onReset" v-if="show">
                <b-row>
                    <div class="col-8">
                        <div class="products">
                            <li v-for="product in products">
                              {{ product.name }}
                            </li>
                            <b-row>
                                <b-col cols="6">
                                    <b-form-group id="input-group-2" label-for="input-2">
                                        <b-form-input id="input-2" v-model="form.name" required placeholder="Enter name"></b-form-input>
                                    </b-form-group>
                                </b-col>
                                <b-col cols="3">
                                    <b-form-group id="input-group-2" label-for="input-2">
                                        <b-form-input id="input-2" v-model="form.name" required placeholder="Enter name"></b-form-input>
                                    </b-form-group>
                                </b-col>
                                <b-col cols="2">
                                    <b-form-group id="input-group-2" label-for="input-2">
                                        <b-form-input id="input-2" v-model="form.name" type="number" required placeholder="Enter name"></b-form-input>
                                    </b-form-group>
                                </b-col>
                                <b-col cols="1">
                                    <b-button type="button" variant="danger">-</b-button>
                                </b-col>
                            </b-row>
                            <b-button type="button" variant="primary">Add</b-button>

                        </div>
                    </div>
                    <div class="col-4">
                        <b-form-group id="input-group-2">
                            <b-form-input id="input-2" v-model="form.name" required placeholder="Enter name"></b-form-input>
                        </b-form-group>
                        <b-form-group id="input-group-2">
                            <b-form-input id="input-2" v-model="form.phone" required placeholder="Enter phone"></b-form-input>
                        </b-form-group>
                        <b-form-group id="input-group-1">
                            <b-form-input id="input-1" v-model="form.email" type="email" required placeholder="Enter email"></b-form-input>
                        </b-form-group>
                    </div>
                </b-row>
                <b-row>
                    <b-button type="submit" variant="primary">Submit</b-button>
                    <b-button type="reset" variant="danger">Reset</b-button>
                </b-row>
            </b-form>
        </b-container>
        <b-card class="mt-3" header="Form Data Result">
            <pre class="m-0">{{ form }}</pre>
        </b-card>
    </div>
</template>
<script>
export default {
    name: 'app',
    data() {
        return {
            form: {
                email: '',
                name: '',
                phone: '',
                products: {},
            },
            show: true
        }
    },
    methods: {
        onSubmit(evt) {
            evt.preventDefault()
            alert(JSON.stringify(this.form))
        },
        onReset(evt) {
            evt.preventDefault()
            // Reset our form values
            this.form.email = ''
            this.form.name = ''
            this.form.food = null
            this.form.checked = []
            // Trick to reset/clear native browser form validation state
            this.show = false
            this.$nextTick(() => {
                this.show = true
            })
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
  border: 1px solid #777777;
  padding: 5px;
  border-radius: 2px;
}
</style>