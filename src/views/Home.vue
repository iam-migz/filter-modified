<template>
<v-container>
    <v-data-iterator
      :items="items"
      :items-per-page.sync="itemsPerPage"
      hide-default-footer
    >
      <template v-slot:header>
        <v-toolbar
          class="mb-2"
          color="indigo darken-5"
          dark
          flat
        >
          <v-toolbar-title>Foods Available</v-toolbar-title>
        </v-toolbar>
      </template>

      <template v-slot:default="props">
        <v-row>
          <v-col
            v-for="item in props.items"
            :key="item.name"
            cols="12"
            sm="6"
            md="4"
            lg="3"
          >
            <v-card>
              <v-card-title class="subheading font-weight-bold">
                {{ item.name }}
              </v-card-title>

              <v-divider></v-divider>

              <v-list dense>
                <v-list-item>
                  <v-list-item-content>Price:</v-list-item-content>
                  <v-list-item-content class="align-end">
                    {{ item.price }}
                  </v-list-item-content>
                </v-list-item>

                <v-list-item >
                  <v-list-item-content>Category: </v-list-item-content>
                  <v-list-item-content v-for="category in item.category" :key="category">
                    {{ category }}
                  </v-list-item-content>
                </v-list-item>

              </v-list>
            </v-card>
          </v-col>
        </v-row>
      </template>
    </v-data-iterator>
  </v-container>
</template>

<script>
  export default {
    data: () => ({
      itemsPerPage: 11,
      items: [
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
    }),
  }
</script>

<style lang="scss" scoped>

</style>