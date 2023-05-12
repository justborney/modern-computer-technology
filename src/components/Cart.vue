<template>
  <div class="cart">
    <div class="products">
      <div class="title">Товары</div>

      <div class="wrapper">
        <div v-for="product in products" :key="product.title" class="product">
          <div class="product-image">{{ product.image }}</div>
          <div class="product-title">{{ product.title }}</div>
          <div class="product-price">{{ product.price }} ₽</div>

          <button @click="addProduct(product)">Добавить</button>
        </div>
      </div>
    </div>

    <div class="basket">
      <div class="title">Корзина. Итого: {{ totalPrice }} ₽</div>

      <div class="wrapper">
        <div v-for="product in cart" :key="product.title" class="product">
          <div class="product-image">{{ product.image }}</div>
          <div class="product-title">{{ product.title }}</div>
          <div class="product-price">{{ product.price }} ₽</div>
          <div class="product-count">Количество: {{ product.count }}</div>

          <div class="basket-buttons">
            <button @click="addProduct(product)">➕</button>
            <button @click="deleteProduct(product)">➖</button>
            <button @click="deleteCompletely(product)">🗑️</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const cart = ref([]);

const products = computed(() => [
  {
    image: "🍎",
    title: "Яблоки, 1 кг",
    price: 120,
  },
  {
    image: "🍌",
    title: "Бананы, 1 кг",
    price: 60,
  },
  {
    image: "🍞",
    title: "Хлеб",
    price: 40,
  },
]);

const totalPrice = computed(() => {
  return cart.value.reduce((acc, { price, count }) => {
    return acc + price * count;
  }, 0);
});

const addProduct = (product) => {
  const productInCart = cart.value.find(({ title }) => title === product.title);

  if (productInCart) {
    productInCart.count += 1;
  } else {
    cart.value.push({
      ...product,
      count: 1,
    });
  }
};

const deleteProduct = (product) => {
  const productInCart = cart.value.find(({ title }) => title === product.title);

  if (productInCart.count > 1) {
    productInCart.count -= 1;
  } else {
    cart.value = cart.value.filter(({ title }) => title !== product.title);
  }
};

const deleteCompletely = (product) => {
  cart.value = cart.value.filter(({ title }) => title !== product.title);
};
</script>

<style lang="scss" scoped>
.cart {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;

  .products,
  .basket {
    height: 50%;
    width: 100%;

    .title {
      font-size: 2rem;
      font-weight: 600;
      margin-bottom: 18px;
    }
  }

  .products .wrapper,
  .basket .wrapper {
    display: flex;
    gap: 8px;
  }

  .products {
    border-bottom: 1px solid hsla(160, 100%, 37%, 0.5);
  }

  .product {
    position: relative;
    display: flex;
    flex-direction: column;
    width: 180px;
    border: 1px solid hsla(160, 100%, 37%, 0.5);
    padding: 16px 16px 48px;
    font-size: 2rem;

    &-image {
      text-align: center;
      font-size: 3rem;
    }

    &-title {
      font-size: 1rem;
      font-weight: 600;
    }

    &-price {
      text-align: right;
      font-weight: 700;
    }

    &-count {
      font-size: 1rem;
    }

    .basket-buttons {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      display: flex;
      justify-content: flex-start;

      button {
        font-size: 1.5rem;
        position: relative;
        width: 45px;
        height: 40px;

        &:last-child {
          margin-left: auto;
        }
      }
    }

    button {
      background-color: hsla(160, 100%, 37%, 0.8);
      font-size: 2rem;
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      border: none;
      cursor: pointer;

      &:active {
        background: #282828;
        color: rgba(235, 235, 235, 0.64);
      }
    }
  }
}
</style>
