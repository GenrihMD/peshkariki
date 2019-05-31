<template>
  <li>
    {{ product.text }}
    <input v-model="product.text">
    <button @click="$emit('remove', product.id)">
      X
    </button>

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
            <b-button type="button" variant="danger">-</b-button>
        </b-col>
    </b-row>

  </li>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      required: true
    }
  }
}
</script>