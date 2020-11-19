<template>
    <div class="pizza__order order">
        <h2 class="order__title">Ваша пицца содержит:</h2>
        <ul class="order__list">
            <li class="order__item" v-for="(item, i) in order" :key="i">
                <p class="order__name">{{ item.name }} <span v-if="item.size"> тесто, {{ item.size }} см</span></p>
                <div class="order__buttons" v-if="!item.isDough">
                    <button class="order__button" :class="[item.count == 1 ? 'order__button_active' : 'button_not-active']" 
                        @click="singleProductCount(item)">
                        x1</button>
                    <button class="order__button order__button_double" :class="[item.count == 2 ? 'order__button_active' : 'button_not-active']" 
                        @click="doubleProductCount(item)">
                        x2</button>
                </div>
                <p class="order__price">{{ item.price * item.count }} ₽</p>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: ['order'],
    methods: {
        singleProductCount(product) {
            this.$emit('single-product-count', product);
        },
        doubleProductCount(product) {
            this.$emit('double-product-count', product);
        }
    }
}
</script>

<style>
    .order {
        margin-bottom: 30px;
    }
    
    .order__title {
        font-weight: 600;
        font-size: 13px;
        margin-bottom: 15px;
        color: #70544f; 
    }

    .order__item {
        display: flex;
        width: 100%;
        color: #70544f;   
        align-items: center;
        margin-bottom: 6px;   
        border-bottom: 1px solid rgba(204, 204, 204, 0.3);     
        padding-bottom: 6px;
    }

    .order__buttons {
        margin-left: auto;
    }

    .order__name {
        font-size: 12px;
         width: 175px;
    }

    .order__price {
        margin-left: auto;
        font-weight: 600;
        font-size: 14px;
        width: 40px;
        text-align: right;
    }

    .order__button {
        font: inherit;
        font-size: 12px;
        font-weight: 700;
        padding: 1px 4px;
        color: #a69895;
        border: 1px solid rgba(204, 204, 204, 0.6);
        background-color: transparent;
        cursor: pointer;
        transition: 0.25s;
    }

    .order__button_double {
        border-left: none;
    }

    .order__button:hover {
        color: #70544f; 
    }

    .order__button_active {
        color: #70544f; 
        background-color: #ffd8a6;
    }

    @media (max-width: 420px) {
  .order__name {
     width: 165px;
  }
}
</style>
