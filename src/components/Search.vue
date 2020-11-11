<template>
    <div class="search">
        <v-text-field
            v-model="searchData"
            label="Search..."
            append-icon="mdi-card-search"
            @keyup.enter="send"
        >
        </v-text-field>
    </div>
</template>

<script>

export default {
    name: 'Search',
    data() {
        return {
            searchData: ''
        }
    },
    methods: {
        send(){
            this.$emit('search-data', this.searchData);
            this.searchData = '';
        }
    }
}
</script>

<style lang="scss" scoped>

</style>