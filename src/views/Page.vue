<template>
    <div class="container">

        <div class="search-box">
            <Search @search-data="fromSearch" />
        </div>
        <div class="tags-box">
            <Tags @new-tags="fromTags" :checkbox-status="checkboxStatus"/>
        </div>
        <div class="itemdetail-box">
            <ItemDetail :detailed-item="currentProductDetail" />
        </div>
        <div class="itemcontainer-box">
            <ItemContainer :product-data="selectedTags" @product-detail="changeProductDetail" />
        </div>
    </div>
</template>

<script>
import Search from '@/components/Search';
import Tags from '@/components/Tags';
import ItemDetail from '@/components/ItemDetail';
import ItemContainer from '@/components/ItemContainer';

export default {
    name: 'Page',
    components: {
        Search,
        Tags,
        ItemDetail,
        ItemContainer
    },
    data() {
        return {
            checkboxStatus: 'on',
            products: this.getProducts(),
            selectedTags: this.getProducts(),
            currentProductDetail:  {id:1,name:'Bacon',category:['Meat'], price: 60, url: '/img/bacon.jpg', description: 'Lorem ipsum dolor, sit amet consectetur adipisicing elit.' }
        }
    },
    methods: {
        getProducts(){
            return [
                // url should be in public folder
                {id:1,name:'Bacon',category:['Meat'], price: 60, url: '/img/bacon.jpg', description: 'Bacon is salt-cured meat cut from a pig\'s belly or back. It is served on its own, incorporated into meals (such as eggs and bacon), or used as an ingredient in dishes like sandwiches, soups, salads, and even sweets like maple bacon ice cream.' },
                {id:2,name:'Fish',category:['Seafood','Fresh'], price: 80, url: '/img/fish.jpg', description: 'Poached, smoked, pan fried, roasted or grilled, make the most of this delicate, omega-rich fish. Our recipes include salmon fillets, salads, parcels and tacos.'},
                {id:3,name:'Chicken',category:['Poultry','Fresh'], price: 85, url: '/img/chicken.jpg', description: 'Hearty and warm Chicken Pastel in Creamy Sauce recipe. Available here. A refined classic Pinoy dish for any day! Know Your Cream. Creamy Recipes. Types: Desserts, Pastas, Main Dishes, Appetizers, Salads, Soups.'},
                {id:4,name:'Beef',category:['Meat'], price: 90, url: '/img/beef.jpg', description: 'Beef stew, beef stroganoff, slow cooker pot roast: find the best beef recipes, including hundreds of ways to cook ground beef for tonight\'s dinner. Beef Meatloaf. Ground Beef. Beef Stew. Beef Main Dishes. Beef Chuck. Beef Brisket. Beef Steaks. Beef Short Loin.'},
                {id:5,name:'Soy Sauce',category:['Sauce','Seasoning'], price: 25, url: '/img/soy.jpg', description: 'Soy sauce is an East Asian liquid condiment of Chinese origin, traditionally made from a fermented paste of soybeans, roasted grain, brine, and Aspergillus oryzae or Aspergillus sojae molds. It is considered to contain a strong umami flavor.'},
                {id:6,name:'Milk',category:['Dairy'], price: 38, url: '/img/milk.jpg', description: 'Milk is a nutrient-rich liquid food produced in the mammary glands of mammals. It is the primary source of nutrition for infant mammals (including humans who are breastfed) before they are able to digest other types of food.'},
                {id:7,name:'Cheese',category:['Dairy'], price: 25, url: '/img/cheese.jpg', description: 'Cheese is a dairy product, derived from milk and produced in wide ranges of flavors, textures and forms by coagulation of the milk protein casein. It comprises proteins and fat from milk, usually the milk of cows, buffalo, goats, or sheep.'},
                {id:8,name:'Frying Pan',category:['Utensil','Cookware'], price: 1200, url: '/img/fryingpan.jpg', description: 'A frying pan, frypan, or skillet is a flat-bottomed pan used for frying, searing, and browning foods. It is typically 20 to 30 cm (8 to 12 in) in diamete'},
                {id:9,name:'Egg',category:['Dairy'], price: 10, url: '/img/egg.jpg', description: 'Combine the eggs, milk, salt, and pepper in a medium bowl and mix very well with a fork or a whisk. Set a plate by the stove. Heat a small (about 6 inches) seasoned omelet pan or non-stick skillet over medium-high heat. When the pan is warm, add the butter (it should sizzle gently).'},
                {id:10,name:'Plates',category:['Utensil'], price: 120, url: '/img/plates.jpg', description: 'A plate is a broad, concave, but mainly flat vessel on which food can be served.[1] A plate can also be used for ceremonial or decorative purposes. Most plates are circular, but they may be any shape, or made of any water-resistant material.'},
                {id:11,name:'Pork',category:['Meat'], price: 85, url: '/img/pork.jpg', description: 'Pork is eaten both freshly cooked and preserved. Curing extends the shelf life of the pork products. Ham, smoked pork, gammon, bacon and sausage are examples of preserved pork. Charcuterie is the branch of cooking devoted to prepared meat products, many from pork.'}
            ]
        },
        fromTags(value){ // value is an array of selected category names
            if(value == 'set'){
                this.selectedTags = this.getProducts();
                return
            }
            this.selectedTags = [];
            // algorithm for looping through product array -> categories and comparing it to the value array, 
            if(value != 'Reset'){ 
                this.products.forEach(prod => {
                    prod.category.forEach(cat => {
                        value.forEach(val => {
                            if(cat.includes(val)){
                                // check if it already exists
                                let truth = this.selectedTags.every(elem => elem.name != prod.name);  // check if it already exist
                                if(truth){
                                    this.selectedTags.push(prod);
                                }
                            }
                        })
                    })
                });

            }
        },
        fromSearch(value){ // this value is a string either a name or a category
            // if user will search, default is to disselect all checkboxes
            this.checkboxStatus = 'off';

            // capitalize value, so that lowercase or uppercase queries will still work
            value = value.toLowerCase();
            let capitalized = value.charAt(0).toUpperCase() + value.slice(1);
            this.selectedTags = this.products.filter(prod => prod.category.includes(capitalized) || prod.name == capitalized);


        },
        changeProductDetail(value){ // value is a product coming from ItemContainer component
            // send value as a prop to ItemDetail component
            this.currentProductDetail = value;
            console.log(this.currentProductDetail);
        }
    }
}
</script>

<style lang="scss" scoped>
.container{
    display: grid;
    max-width: 1280px;
    margin: 0 auto;
    grid-template-areas: 
    "search search search search itemcontainer itemcontainer"
    "tags tags tags tags itemcontainer itemcontainer"
    "itemdetail itemdetail itemdetail itemdetail itemcontainer itemcontainer"
    "itemdetail itemdetail itemdetail itemdetail itemcontainer itemcontainer"
    "itemdetail itemdetail itemdetail itemdetail itemcontainer itemcontainer"
    "itemdetail itemdetail itemdetail itemdetail itemcontainer itemcontainer"
    ". . . . itemcontainer itemcontainer"
    ;
    // . means a blank space in grid-template-areas
    grid-template-columns: repeat(6, 1fr);
    grid-auto-rows: minmax(80px, auto);
    grid-gap: 10px;

    .search-box{
        // border: 1px solid grey;
        grid-area: search;
    }
    .tags-box{
        // border: 1px solid grey;
        grid-area: tags;
    }
    .itemdetail-box{
        // border: 1px solid grey;
        grid-area: itemdetail;

    }
    .itemcontainer-box{
        // border: 1px solid grey;
        grid-area: itemcontainer;
    }
}
</style>