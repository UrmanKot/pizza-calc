<template>
    <div class="pizza__request">
        <a class="pizza__order-button" @click="checkoutOrder()">Заказать</a>
        <div class="pizza__result">
            <p class="pizza__total">Итого:</p>
            <p class="pizza__result-price">{{ orderPrice }} ₽</p>
        </div>
    </div>
</template>

<script>
export default {
    props: ['orderPrice'],
    methods: {
        checkoutOrder() {
            this.$emit('checkout-order');
        }
    }
}
</script>

<style>
    .pizza__request {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .pizza__total {
        color: #70544f;
        font-size: 12px;
        font-weight: 400;
    }

    .pizza__result {
        text-align: right;
    }

    .pizza__result-price {
        color: #70544f;
        font-size: 16px;
        font-weight: 600;
    }

    .pizza__order-button {
        width: 135px;
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

    .pizza__order-button:hover {
        transform: scale(1.1, 1.1);
    }

    .pizza__order-button:active {
        transition: 0.25s;
    }
</style>