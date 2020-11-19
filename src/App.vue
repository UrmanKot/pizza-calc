<template>
  <div class="pizza" id="App">
    <div class="pizza__inner container">
      <div v-if="!checkout">
        <Constructor :order="order"></Constructor>
        <div class="pizza__column">
          <div class="pizza__box pizza__box_left">
            <h1 class="pizza__title">Соберите свою пиццу</h1>
            <p class="pizza__text">У пиццы может быть до 10 любых ингредиентов, иначе она просто не пропечется</p>
            <Tabs @render-ingredients="renderIngredients" @toggle-tabs="toggleTabs"></Tabs>
            <Ingredients 
              :currentIngredints="currentIngredints" 
              @toggle-product-in-order="toggleProductInOrder" 
              @add-active-item="addActiveItem">
            </Ingredients>
            <p class="pizza__error" v-if="order.length >= maxCountIngredients">Пицца уже содержит 10 ингредиентов. Может быть, хотите что-то убрать?</p>
          </div>
          <div class="pizza__box pizza__box_right">
            <div class="pizza__source">
              <img class="pizza__image" src="./assets/img/pizza.png">
              <input class="pizza__name" type="text" placeholder="Придумайте название" v-model="pizzaName">
              <Dough :pizza-dough="pizzaDough" @change-pizza-dough="changePizzaDough"></Dough>
              <SourcePizza :pizza-size="pizzaSize" @change-pizza-size="changePizzaSize"></SourcePizza>
            </div>
            <Order :order="order" @double-product-count="doubleProductCount" @single-product-count="singleProductCount"></Order>
            <OrderCost :order-price="orderPrice" @checkout-order="checkoutOrder"></OrderCost>
          </div>
        </div>
      </div>
      <Checkout v-if="checkout" :order="order" :pizza-name="pizzaName" @return-to-order="returnToOrder"></Checkout>
    </div>
  </div>
</template>

<script>
import Tabs from './components/Tabs.vue';
import Ingredients from './components/Ingredients.vue';
import Order from './components/Order.vue';
import OrderCost from './components/OrderCost.vue';
import SourcePizza from './components/SourcePizza.vue';
import Dough from './components/Dough.vue';
import Constructor from './components/Constructor.vue';
import Checkout from './components/Checkout.vue';

export default {
  name: 'App',
  data() {
    return {
      ingredients: [
            { category: 'meat', name: 'Пепперони', price: 89, image: 'pepperoni.svg', constructor: 'pepperoni.png'},
            { category: 'meat', name: 'Ароматная свинина', price: 89, image: 'smoked_sausages.svg', constructor: 'smoked_sausages.png' },
            { category: 'meat', name: 'Ветчина', price: 89, image: 'ham.svg', constructor: 'ham.png' },
            { category: 'meat', name: 'Бекон', price: 89, image: 'bacon.svg', constructor: 'bacon.png' },
            { category: 'meat', name: 'Говядина', price: 89, image: 'beef.svg', constructor: 'beef.png' },
            { category: 'meat', name: 'Куриная грудка', price: 89, image: 'grilledchicken.svg', constructor: 'grilledchicken.png' },
            { category: 'vegetables', name: 'Шампиньоны', price: 29, image: 'champignons.svg', constructor: 'champignons.png' },
            { category: 'vegetables', name: 'Лук', price: 29, image: 'onions.svg', constructor: 'onions.png' },
            { category: 'vegetables', name: 'Перец халапеньо', price: 29, image: 'jalapenopeppers.svg', constructor: 'jalapenopeppers.png' },
            { category: 'vegetables', name: 'Орегано', price: 29, image: 'oregano.svg', constructor: 'oregano.png' },
            { category: 'vegetables', name: 'Зеленый перец', price: 29, image: 'sweetgreenpepper.svg', constructor: 'sweetgreenpepper.png' },
            { category: 'vegetables', name: 'Ананасы', price: 29, image: 'pineapple.svg', constructor: 'pineapple.png' },
            { category: 'vegetables', name: 'Томаты', price: 29, image: 'tomato.svg', constructor: 'tomato.png' },
            { category: 'vegetables', name: 'Маринованные огурцы', price: 29, image: 'pickles.svg', constructor: 'pickles.png' },
            { category: 'vegetables', name: 'Чеснок', price: 29, image: 'garlic.svg', constructor: 'garlic.png' },
            { category: 'vegetables', name: 'Оливки черные', price: 29, image: 'blackolives.svg', constructor: 'blackolives.png' },
            { category: 'cheese', name: 'Сыр реджанито', price: 79, image: 'reggianito.svg', constructor: 'reggianito.png' },
            { category: 'cheese', name: 'Сыр с голубой плесенью', price: 79, image: 'blue_cheese.svg', constructor: 'blue_cheese.png' },
            { category: 'cheese', name: 'Смесь итальянских сыров', price: 79, image: 'italian_cheese.svg', constructor: 'italian_cheese.png' },
            { category: 'cheese', name: 'Мягкий молодой сыр', price: 79, image: 'soft_cheese.svg', constructor: 'soft_cheese.png' },
            { category: 'cheese', name: 'Сыр моцарелла', price: 79, image: 'mozzarella.svg', constructor: 'mozzarella.png' }
      ],
      currentIngredints: [],
      order: [],
      orderPrice: 0,
      maxCountIngredients: 10,
      pizzaSize: [
        { size: 23, price: 279, selected: true },
        { size: 30, price: 329, selected: false },
        { size: 35, price: 359, selected: false },
        { size: 40, price: 399, selected: false }
      ],
      pizzaDough: [
        { name: 'Традиционное', selected: true },
        { name: 'Тонкое', selected: false }
      ],
      checkout: true
    }
  },

  components: {
    Ingredients,
    Tabs,
    Order,
    OrderCost,
    SourcePizza,
    Dough,
    Constructor,
    Checkout
  },

  created: function() {
    this.renderIngredients('meat');
    this.order[0] = {category: 'dough', name: 'Традиционное', size: 23, price: 279, count: 1, isDough: true, constructor: 'dough.jpg' };
    this.countOrderPrice();
    this.checkout = false;
    this.pizzaName = '';
  },

  watch: {
    pizzaName: function() {
      console.log(this.pizzaName);
    }
  },

  methods: {
    renderIngredients(name) {
      let arr = [];
      this.currentIngredints = [];
      this.ingredients.forEach(item => {
        if (item.category == name) {
        arr.push(item);
        }
      })
      this.currentIngredints = [...arr];
    },
    toggleProductInOrder(product) {
      if (this.order.length < this.maxCountIngredients) {
          const isProductAvailable = this.order.some(item => {
          return item.name === product.name;
        });

        if (!isProductAvailable) {
          this.order.push({name: product.name, price: product.price, count: 1, constructor: product.constructor, category: product.category});
        }

        if (product.active) {
          product.active = false;
          this.order.forEach((item, i) => {
            if (item.name === product.name) {
              this.order.splice(i, 1);
            }
          })
        } else {
          product.active = true;
        }
        this.countOrderPrice(); 
      } 
      else {
          product.active = false;
          this.order.forEach((item, i) => {
            if (item.name === product.name) {
              this.order.splice(i, 1);
            }
          })
        this.countOrderPrice(); 
      }
    },
    toggleTabs(evt) {
      const tabs = document.querySelectorAll('.tabs__item');

      tabs.forEach(item => {
        item.classList.remove('tabs__item_active');
        console.log(item);
      })

      evt.target.classList.add('tabs__item_active');
    },
    countOrderPrice() {
      this.orderPrice = 0;

      this.order.forEach(item => {
        this.orderPrice += (item.price * item.count);
      });
    },
    doubleProductCount(product) {
      if (product.count < 2) {
        product.count = 2;
        this.countOrderPrice();
      }
    },
    singleProductCount(product) {
      if (product.count == 2) {
        product.count = 1;
        this.countOrderPrice();
      }
    },
    addActiveItem: function(item) {
      if (this.order.length < this.maxCountIngredients) {
        item.active = true;
      }
    },
    changePizzaSize: function(item) {
      this.pizzaSize.forEach(elem => {
        elem.selected = false;
      });

      item.selected = true;
      this.order[0].size = item.size;
      this.order[0].price = item.price;

      this.countOrderPrice();
    },
    changePizzaDough: function(item) {
      this.pizzaDough.forEach(elem => {
        elem.selected = false;
      });

      item.selected = true;
      this.order[0].name = item.name;
    }, 
    checkoutOrder: function() {
      if (this.pizzaName == '') {
        this.pizzaName = 'Создай свою пиццу'
      }
        this.checkout = true;
    },
    returnToOrder: function() {
      this.checkout = false;
      window.location.reload();
    }
  }
}
</script>

<style>

.container {
    max-width: 1000px;
    padding: 50px 65px;
    position: relative;
    margin: 0 auto;
}

.pizza {
    display: flex;
    align-items: center;
    height: 100%;
    font-family: 'Open Sans', sans-serif;
    margin-top: 50px;
    margin-bottom: 50px;
}

.pizza__inner {
    background-color: #ffffff;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
    border-radius: 6px;
}

.pizza__column {
    display: flex;
}

.pizza__box_left {
    flex: 0 1 510px;
    margin-right: 35px;
}

.pizza__box_right {
    flex: 0 1 325px;
}

.pizza__title {
    font-size: 24px;
    font-weight: 700;
    color: #70544f;
    margin-bottom: 10px;
}

.pizza__text {
    font-size: 12px;
    margin-bottom: 40px;
    color: #a69895;
}

.pizza__error {
    color: #c21313;
    font-size: 12px;
    font-weight: 600;
    padding-top: 15px;
}

.pizza__source {
    margin-bottom: 30px;
}

.pizza__image {
    margin: 0 auto;
    display: flex;
    margin-bottom: 20px;
}

.pizza__name {
    font: inherit;
    display: flex;
    width: 285px;
    padding: 0 30px;
    margin: 0 auto 30px;
    text-align: center;
    font-weight: 700;
    font-size: 18px;
    color: #70544f;
}

::-webkit-input-placeholder {
    color: #cacaca;
}

@media (max-width: 1280px) {
    .pizza__column {
        flex-direction: column;
    }

    .pizza__box_left {
        margin-right: 0;
        order: 1;
    }

    .pizza__box_right {
        flex: 0;
        max-width: 450px;
        margin: 0 auto 50px;
    }

    .pizza__image {
        display: none;
    }

    @media (max-width: 768px) {
        .container {
            padding: 30px 30px;
            width: 100%;
            border-radius: none;
            box-shadow: none;
        }

        .pizza {
            margin: 0;
        }
    }

    @media (max-width: 560px) {
        .pizza__constructor {
            display: none;
        }

        .pizza__image {
            display: flex;
        }

        .pizza__box_right {
          margin: 0 0 50px;
        }
    }

    @media (max-width: 420px) {
        .container {
          padding: 30px 15px;
        }

        .pizza__name {
          width: 265px;
          padding: 0;
        }
    }
}
</style>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600;700&display=swap');  

  html,
  body,
  div,
  span,
  applet,
  object,
  iframe,
  h1,
  h2,
  h3,
  h4,
  h5,
  h6,
  p,
  blockquote,
  pre,
  a,
  abbr,
  acronym,
  address,
  big,
  cite,
  code,
  del,
  dfn,
  em,
  img,
  ins,
  kbd,
  q,
  s,
  samp,
  small,
  strike,
  strong,
  sub,
  sup,
  tt,
  var,
  b,
  u,
  i,
  center,
  dl,
  dt,
  dd,
  ol,
  ul,
  li,
  fieldset,
  form,
  label,
  legend,
  table,
  caption,
  tbody,
  tfoot,
  thead,
  tr,
  th,
  td,
  article,
  aside,
  canvas,
  details,
  embed,
  figure,
  figcaption,
  footer,
  header,
  hgroup,
  menu,
  nav,
  output,
  ruby,
  section,
  summary,
  time,
  mark,
  audio,
  video {
    margin: 0;
    padding: 0;
    font-size: 100%;
    vertical-align: baseline;
  }

  body {
    height: 100%;
    background-color: #f8f8f8;
  }

  a {
    text-decoration: none;
  }

  ul,
  li {
    list-style-type: none;
    margin: 0;
    padding: 0;
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    font-size: 100%;
    font-weight: normal;
  }

  html {
    box-sizing: border-box;
  }
  *,
  *:before,
  *:after {
    box-sizing: border-box;
  }
  :focus {
    outline: 0;
  }

  img,
  audio,
  video {
    max-width: 100%;
    height: auto;
  }
  audio,
  canvas,
  iframe,
  video,
  img,
  svg {
    vertical-align: middle;
  }
  iframe {
    border: 0;
  }
  textarea {
    resize: none;
    overflow: auto;
    vertical-align: top;
    box-shadow: none;
    -webkit-box-shadow: none;
    -moz-box-shadow: none;
  }
  input,
  textarea,
  select,
  button {
    outline: none;
    border: none;
    font-size: 100%;
    margin: 0;
  }
  button,
  input {
    line-height: normal;
  }

  table {
    border-collapse: collapse;
    border-spacing: 0;
  }
  td,
  th {
    padding: 0;
    text-align: left;
  }
</style>
