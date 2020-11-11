<template>
    <div class="itemcontainer">
        <v-card 
            v-for="(product,index) in productData"
            :key="index"
            @click="send(product)"
            
        >
            <v-card-title> {{ product.name  }} ₱{{ product.price }}</v-card-title>
            <v-card-subtitle> 
                <span
                    v-for="cat in product.category"
                    :key="cat"
                >
                    {{ cat  }}
                </span>
            </v-card-subtitle>
        </v-card>
    </div>
</template>

<script>
export default {
    name: 'ItemContainer',
    props: {
        productData: {
            type: Array
        }
    },
    methods: {
        send(product){
            this.$emit('product-detail', product);
        }
    }
}
</script>

<style lang="scss" scoped>

</style>