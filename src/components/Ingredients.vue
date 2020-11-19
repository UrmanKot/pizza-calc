<template>
    <ul class="pizza__list ingredients">
        <li 
            class="ingredients__item" 
            :class="[product.active ? 'ingredients__item_active' : '']"
            v-for="(product, i) in currentIngredints" 
            :key="i" 
            @click="toggleProductInOrder(product)">
                <figure class="ingredients__fig">
                    <img :src="require(`@/assets/svg/${product.image}`)" :alt="product.name">
                </figure>
                <h3 class="ingredients__title">{{ product.name }}</h3>
                <p class="ingredients__price">{{ product.price }} ₽</p>
                <div class="ingredients__add-block"></div>
                <div class="ingredients__remove"></div>
        </li>
    </ul>
</template>

<script>
export default {
    props: ['currentIngredints'],
    methods: {
        toggleProductInOrder(product) {
            this.$emit('toggle-product-in-order', product);
        },
        doubleProductCount(product) {
            this.$emit('double-product-count', product);
        },
        addActiveItem(item) {
            this.$emit('add-active-item', item);
        }
    }
}
</script>

<style scoped>
.ingredients {
    display: flex;
    flex-wrap: wrap;
}

.ingredients__item {
    width: calc(25% - 10px);
    min-height: 145px;
    margin: 5px;
    background-color: #f8f8f8;
    color: #70544f;
    padding: 12px;
    border-radius: 6px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    cursor: pointer;
    transition: 0;
    position: relative;
     user-select: none;
}

.ingredients__item_active {
    background-color: #ffd8a6;
    transition: 0;
}

.ingredients__fig {
    min-height: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.ingredients__title {
    text-align: center;
    font-weight: 700;
    font-size: 12px;
}

.ingredients__price {
    line-height: 1;
    font-weight: 600;
    font-size: 14px;
}

.ingredients__add-block,
.ingredients__remove {
    display: none;
    width: 46px;
    height: 46px;
    background-color: #009471;
    border-radius: 50%;
    position: relative;
    align-items: center;
    justify-content: center;
    animation: bounce 0.4s;
    position: absolute;
    top: 15%;
}

.ingredients__remove {
    background-color: #c21313;
}

.ingredients__remove::after {
    content: '';
    position: absolute;
    background-color: #ffffff;
    width: 16px;
    height: 4px;
}

.ingredients__add-block::before,
.ingredients__add-block::after {
    content: '';
    position: absolute;
    background-color: #ffffff;
}

.ingredients__add-block::before {
    width: 16px;
    height: 4px;
}

.ingredients__add-block::after {
    width: 4px;
    height: 16px;
}

.ingredients__remove {
    display: none;
    position: absolute;
    z-index: 100;
}

.ingredients__item:hover {
    background-color: #ededed;
}

.ingredients__item_active:hover {
    background-color: #ffd8a6;
}

.ingredients__item:hover .ingredients__add-block {
    display: flex;
}

.ingredients__item_active:hover .ingredients__remove {
    display: flex;
}

.ingredients__item_active:hover .ingredients__add-block {
    display: none;
}



@media (max-width: 560px) {
  .ingredients__item {
     width: calc(33.3% - 10px);
  }
}

@media (max-width: 420px) {
  .ingredients__item {
     width: calc(50% - 10px);
  }
}


</style>