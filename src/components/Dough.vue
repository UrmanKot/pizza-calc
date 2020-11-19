<template>
    <div class="pizza__dough">
        <button 
            class='pizza__dough-item'
            :class="[item.selected ? 'pizza__dough-item_active' : '']" 
            v-for="(item, i) in pizzaDough" 
            :key="i" 
            @click="changePizzaDough(item)">
            {{ item.name }}
        </button>
    </div>
</template>

<script>
export default {
    props: ['pizzaDough'],
    methods: {
        changePizzaDough(item) {
            this.$emit('change-pizza-dough', item);
        }
    }
}
</script>

<style>
    .pizza__dough {
        width: 285px;
        margin: 0 auto;
        margin-bottom: 10px;
        border: 1px solid #ededed;
        border-radius: 20px;
        background-color: #fff;
    }

    .pizza__dough-item {
        width: 50%;
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

    .pizza__dough-item_active {
        background-color: #ededed;
        cursor: default;
    }

    @media (max-width: 360px) {
        .pizza__dough {
        width: 265px;
        margin: 0 auto;
        margin-bottom: 10px;
        border: 1px solid #ededed;
        border-radius: 20px;
        background-color: #fff;
    }
}
</style>