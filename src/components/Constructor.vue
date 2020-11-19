<template>
    <div class="pizza__constructor constructor">
        <div class="constructor__group constructor__group_dough" style="z-index: 0">
          <div v-for="(product, i) in order" :key="i">
            <img v-if="product.category == 'dough'" :src="require(`@/assets/img/${product.constructor}`)" :alt="product.name" width="512">
           </div>
        </div>
        <div class="constructor__group constructor__group_meat" style="z-index: 1">
          <div v-for="(product, i) in order" :key="i">
            <img v-if="product.category == 'meat'" :src="require(`@/assets/img/${product.constructor}`)" :alt="product.name" width="512">
           </div>
        </div>
        <div class="constructor__group constructor__group_vegetables" style="z-index: 2">
          <div v-for="(product, i) in order" :key="i">
            <img v-if="product.category == 'vegetables'" :src="require(`@/assets/img/${product.constructor}`)" :alt="product.name" width="512">
           </div>
        </div>
        <div class="constructor__group constructor__group_cheese" style="z-index: 3">
          <div v-for="(product, i) in order" :key="i">
            <img v-if="product.category == 'cheese'" :src="require(`@/assets/img/${product.constructor}`)" :alt="product.name" width="512">
           </div>
        </div>
      </div>
</template>

<script>
export default {
    props: ['order']
}
</script>

<style>
.constructor {
  position: relative;
  max-width: 512px;
  width: 100%;
  height: 450px;
  margin: 0 auto 50px;
}

.constructor__group {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: auto;
}

.constructor__group div {
  position: absolute;
  top: 0;
  left: 0;
}
</style>
