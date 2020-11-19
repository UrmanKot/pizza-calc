<template>
        <div class="pizza__size">
            <button
                v-for="(item, i) in pizzaSize" 
                @click="changePizzaSize(item)"
                class="pizza__size-item" 
                :class="[item.selected ? 'pizza__size-item_active' : '']"
                :key="i">
                {{ item.size }} см
            </button>
        </div>
</template>

<script>
export default {
    props: ['pizzaSize'],
    methods: {
        changePizzaSize(item) {
            this.$emit('change-pizza-size', item);
        }
    }
}
</script>

<style>
    .pizza__size {
        width: 285px;
        margin: 0 auto;
        border: 1px solid #ededed;
        border-radius: 20px;
        background-color: #fff;
    }

    .pizza__size-item {
        width: 25%;
        border-radius: 20px;
        background-color: #fff;
        color: #70544f;
        box-sizing: border-box;
        padding: 0;
        line-height: 1;
        height: 32px;
        cursor: pointer;
        font-size: 14px;
        transition: 0.25s;
    }

    .pizza__size-item_active {
        background-color: #ededed;
        cursor: default;
    }

    @media (max-width: 360px) {
        .pizza__size {
            width: 265px;
    }
}
</style>