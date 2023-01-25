<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>Bienvenue chez McDonald's</h1>
    <!-- PLACE -->
    <div v-if="step === 1">
      <p>Sur place ou à emporter ?</p>
      <div class="place">
        <Place v-for="(place, id) in allThePlaces" :key="id" class="place__component" @place-of-the-user="setPlace" :name="place" />
      </div>
    </div>
    <!-- MENU -->
    <div v-if="step === 2">
      <p>Quel menu pour vous ?</p>
      <div class="menu">
        <Menu v-for="(menu, id) in allTheMenus" :key="id" class="menu__component" @menu-of-the-user="setMenu" :name="menu[0]" :price="menu[1]" />
      </div>
    </div>
    <!-- BURGER -->
    <div v-if="step === 3">
      <p>Choisissez votre magnifique burger 🍔</p>
      <div class="burger">
        <Burger v-for="(burger, id) in allTheBurgers" :key="id" class="burger__component" @burger-of-the-user="setBurger" :name="burger[0]" :price="burger[1]" />
      </div>
    </div>
    <!-- ACCOMPANIEMENT -->
    <div v-if="step === 4">
      <p>Votre accompagnement 🍟</p>
      <div class="accompaniement">
        <Accompaniement v-for="(accompaniement, id) in allTheAccompaniements" :key="id" class="accompaniement__component" @accompaniement-of-the-user="setAccompaniement" :name="accompaniement" />
      </div>
    </div>
    <!-- DRINK -->
    <div v-if="step === 5">
      <p>Et enfin, votre boisson 🥤</p>
      <div class="drink">
        <Drink v-for="(drink, id) in allTheDrinks" :key="id" class="drink__component" @drink-of-the-user="setDrink" :name="drink" />
      </div>
    </div>
    <div class="recap" v-if="step === 6">
      <h2>Récapitulatif de la commande</h2>
      <p class="recap__type">Type de commande : {{ place }}</p>
      <div class="recap__menu">
        <ul v-for="(menu, id) in recap" :key="id">
          <p>Numéro de commande : #{{ id + 1 }}</p>
          <li>{{ menu[0] }}</li>
          <li>{{ menu[1] }}</li>
          <li>{{ menu[2] }}</li>
          <li>{{ menu[3] }}</li>
          <li>Prix : {{ menu[4] }} €</li>
        </ul>
      </div>
      <ButtonNewOrder @new-order="setNewOrder" />
    </div>
  </div>
</template>

<script>
import Place from './components/Place.vue'
import Menu from './components/Menu.vue'
import Burger from './components/Burger.vue'
import Accompaniement from './components/Accompaniement.vue'
import Drink from './components/Drink.vue'
import ButtonNewOrder from './components/ButtonNewOrder.vue'

export default {
  name: 'App',
  components: {
    Place,
    Menu,
    Burger,
    Accompaniement,
    Drink,
    ButtonNewOrder
  },
  data() {
    return {
      allThePlaces : ['Sur place', 'À emporter'],
      allTheMenus : [
        ['Best Of', 0.5], 
        ['Maxi Best Of', 0.8], 
        ['Petite faim', 0]
        ],
      allTheBurgers: [['Big Mac', 6], ['280', 7], ['CBO', 7.5], ['Big Tasty', 6]],
      allTheAccompaniements: ['Frites', 'Salade', 'Potatoes'],
      allTheDrinks: ['Eau', 'Oasis', 'Coca'],
      step: 1,
      numberOfOrder: 0,
      place: "",
      totalPrice: 0,
      recap: [[]]
    }
  },
  methods: {
    setPlace(payload) {
      this.place = payload.place;
      this.step = 2;
    },
    setMenu(payload) {
      this.recap[this.numberOfOrder].push(payload.menu);
      this.totalPrice = this.totalPrice + payload.price;
      this.step = 3;
    },
    setBurger(payload) {
      this.recap[this.numberOfOrder].push(payload.burger);
      this.totalPrice = this.totalPrice + payload.price;
      this.step = 4;
    },
    setAccompaniement(payload) {
      this.recap[this.numberOfOrder].push(payload.accompaniement);
      this.step = 5;
    },
    setDrink(payload) {
      this.recap[this.numberOfOrder].push(payload.drink);
      this.recap[this.numberOfOrder].push(this.totalPrice); // Final price
      this.step = 6;
    },
    setNewOrder() {
      this.recap.push([]); // New order
      this.totalPrice = 0; // Reset price for the new order
      this.numberOfOrder = this.numberOfOrder + 1;
      this.step = 2;
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.place, .menu, .burger, .accompaniement, .drink {
  display: flex;
  justify-content: center;
  align-items: center;
  &__component {
    margin: 30px 30px;
  }
}

.recap {
  &__type {
    font-weight: bold;
  }
  &__menu {
    display: flex;
    justify-content: center;
    align-items: center;
    ul {
      list-style-type: none;
      padding: 0;
      margin: 0 30px;
    }
  }
}
</style>