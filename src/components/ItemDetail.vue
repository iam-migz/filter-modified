<template>
    <div class="itemdetail">
        <v-card
            max-width="500"
            class="mx-auto my-5"
        >
            <v-img
                :src="detailedItem.url"
                height="250"
            ></v-img>
            <v-card-title>{{detailedItem.name}}</v-card-title>
            <v-card-subtitle>₱ {{detailedItem.price}} only</v-card-subtitle>
            <v-divider></v-divider>

            <v-card-text>
                {{detailedItem.description}}
            </v-card-text>

        </v-card>
    </div>
</template>

<script>
export default {
    name: 'ItemDetail',
    props: {
        detailedItem: {
            type: Object
        }
    },
    data(){
        return{
        }
    }
}
</script>

<style lang="scss" scoped>

</style>