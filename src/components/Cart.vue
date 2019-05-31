<template>
    <div>
        <ul v-if="products.length">
            <CartItem v-for="product in products" :key="product.id" :product="product" @remove="removeTodo" />
        </ul>
        <p v-else>
            Nothing left in the list. Add a new product.
        </p>
    </div>
</template>
<script>
import CartItem from './CartItem.vue'

let nextTodoId = 1

export default {
    components: {
        CartItem
    },
    data() {
        return {
            newProductName: '',
            products: [{
	                id: 1,
	                name: "Jeans",
	                number: "1",
	                price: "1200"
	            }, ]
        }
    },
    methods: {
        addTodo() {
            const trimmedText = this.newProductName.trim()
            if (trimmedText) {
                this.todos.push({
                    id: nextTodoId++,
                    text: trimmedText
                })
                this.newProductName = ''
            }
        },
        removeTodo(idToRemove) {
            this.todos = this.todos.filter(todo => {
                return todo.id !== idToRemove
            })
        }
    }
}
</script>