<template>
        <ul class="pizza__tabs tabs">
            <li class="tabs__item tabs__item_active" @click="renderIngredients('meat'), toggleTabs($event)">Мясо</li>
            <li class="tabs__item" @click="renderIngredients('vegetables'), toggleTabs($event)">Овощи</li>
            <li class="tabs__item" @click="renderIngredients('cheese'), toggleTabs($event)">Сыр</li>
        </ul>
</template>

<script>
export default {
    methods: {
         renderIngredients(name) {
            this.$emit('render-ingredients', name);
        },
         toggleTabs(evt) {
            this.$emit('toggle-tabs', evt);
        }
    }
}
</script>

<style scoped>
    .tabs {
        display: flex;
        widows: 100%;
        box-shadow: inset 0 -3px 0 0 #efeeee;
        margin-bottom: 15px;
    }

    .tabs__item {
        padding-bottom: 20px;
        line-height: 0;
        font-size: 14px;
        font-weight: 600;
        box-sizing: border-box;
        cursor: pointer;
        margin-right: 20px;
        color: #70544f;
    }

    .tabs__item_active {
        border-bottom: 3px solid #009471;
        cursor: default;
        color: #009471;
    }
</style>
