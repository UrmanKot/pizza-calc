<template>
    <div class="pizza__checkout checkout">
        <svg width="32" height="32" viewBox="0 0 32 32" class="checkout__icon">
          <path d="M11.2 23.2c-1.32 0-2.4 1.08-2.4 2.4 0 1.32 1.08 2.4 2.4 2.4 1.32 0 2.4-1.08 2.4-2.4 0-1.32-1.08-2.4-2.4-2.4zM4 4v2.4h2.4l4.32 9.12-1.68 2.88c-.12.36-.24.84-.24 1.2 0 1.32 1.08 2.4 2.4 2.4h14.4v-2.4H11.68c-.12 0-.24-.12-.24-.24v-.12l1.08-2.04h8.88c.96 0 1.68-.48 2.04-1.2l4.32-7.8c.24-.24.24-.36.24-.6 0-.72-.48-1.2-1.2-1.2H9.04L7.96 4H4zm19.2 19.2c-1.32 0-2.4 1.08-2.4 2.4 0 1.32 1.08 2.4 2.4 2.4 1.32 0 2.4-1.08 2.4-2.4 0-1.32-1.08-2.4-2.4-2.4z" fill="#c21313" fill-rule="nonzero"></path>
        </svg>
        <h3 class="checkout__text">Пицца &laquo;{{ pizzaName }}&raquo; добавлена в корзину</h3>
        <Constructor :order="order"></Constructor>
        <button class="checkout__button" @click="returnToOrder()">Создать еще раз</button>
      </div>
</template>

<script>
import Constructor from '../components/Constructor.vue';
export default {
    props: ['order', 'pizzaName'],
    components: {Constructor},
    methods: {
        returnToOrder() {
            this.$emit('return-to-order');
        }
    }
}
</script>

<style>
.checkout {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.checkout__icon {
    margin-bottom: 15px;
}

.checkout__text {
  font-size: 24px;
  font-weight: 700;
  color: #70544f;
  width: 100%;
  margin-bottom: 20px;
  text-align: center;
}

.checkout__button {
        font: inherit;
        width: 240px;
        height: 45px;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: #009471;
        color: #ffffff;
        font-weight: 600;
        text-transform: uppercase;
        border-radius: 30px;
        font-size: 14px;
        letter-spacing: 1px;
        cursor: pointer;
        transition: 0.25s;
}
</style>