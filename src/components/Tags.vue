<template>
    <div class="tags d-flex">
            <v-checkbox
                v-for="tag in tags"
                :key="tag"
                v-model="selected"
                @click="changeTags"
                :label="tag"
                :value="tag"
            ></v-checkbox>
            <v-btn
                outlined
                fab
                color="primary"
                x-small
                @click="reset"
                id="btn-check"
            >
                <v-icon>mdi-check-all</v-icon>
            </v-btn>
    </div>
</template>

<script>
export default {
    name: 'Tags',
    props: {
        checkboxStatus: {
            type: String
        }
    },
    data(){
        return {
            tags: this.getTags(),
            selected: this.getTags()
        }
    },
    methods: {
        reset(){
            console.log(this.uncheckTag);
            // if nothing is selected then select all
            if (this.selected === undefined || this.selected.length == 0) {
                this.selected = this.getTags();
                this.$emit('new-tags', 'set');
            }
            // deselect all
            else {
                this.selected = [];
                 this.$emit('new-tags', 'reset');
            }
        },
        getTags(){
            return ['Meat','Seafood','Fresh','Poultry','Sauce','Seasoning','Dairy','Utensil','Cookware'];
        },
        changeTags(){
            this.$emit('new-tags', this.selected);
        }
    },
    watch: {
        checkboxStatus(newVal){
            // this checks if the prop changed
            // console.log('Prop change', newVal, ' | was ', oldVal);

            if(newVal == 'off'){  // turn off the checkboxes
                this.selected = [];
            }
        }

    }
    
}
</script>

<style lang="scss" scoped>
.tags{
    display: flex;
}
#btn-check{
    margin-top: 15px;
    margin-left: 5px;
}
</style>