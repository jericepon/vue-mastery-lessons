<template>
    <div class="nav-bar">
        <img id="logo" alt="Vue logo" src="./assets/logo.png" />
    </div>

    <div class="product">
        <div class="product-image">
            <img :src="image" alt="" />
        </div>

        <div class="product-info">
            <h1>{{ product }}</h1>
            <p v-if="inventory > 10">In Stock</p>
            <p v-else-if="inventory <= 10 && inventory > 0">Almost sold out!</p>
            <p v-else :class="{ outOfStock: !inStock }">Out of stock</p>
            <ul>
                <li v-for="detail of details" :key="detail">
                    {{ detail }}
                </li>
            </ul>
            <div v-for="(variant, index) of variants" :key="variant.variantId">
                <p
                    class="variant-item"
                    :style="{ backgroundColor: variant.variaColor }"
                    @mouseover="updateProduct(index)"
                ></p>
            </div>

            <button
                :disabled="!inStock"
                :class="{ disabledButton: !inStock }"
                @click="addToCart"
            >
                Add to Cart
            </button>
            <div class="cart">
                <p>Cart ({{ cart }})</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            product: "",
            selectedVariant: 0,
            inventory: 99,
            details: ["80% cotton", "20% polyester", "Gender-neutral"],
            variants: [
                {
                    name: "Green Sock",
                    variantId: 2234,
                    variaColor: "green",
                    variantImage: "./image/vmSocks-green-onWhite.jpg",
                },
                {
                    name: "Blue Sock",
                    variantId: 2235,
                    variaColor: "blue",
                    variantImage: "./image/vmSocks-blue-onWhite.jpg",
                },
            ],
            inStock: true,
            cart: 0,
        };
    },
    methods: {
        addToCart() {
            this.cart += 1;
        },
        updateProduct(index) {
            this.image = this.variants[index].variantImage;
            this.product = this.variants[index].name;
        },
    },
    created() {
        this.product = this.variants[this.selectedVariant].name
        this.image = this.variants[this.selectedVariant].variantImage
    }
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#logo {
    max-width: 60px;
    margin: 0 auto;
    border: none;
}


 body {
    font-family: tahoma;
    color:#282828;
    margin: 0px;
  }

  .variant-item {
      cursor: pointer;
      width: 50px;
      height: 50px;
  }
  
  .nav-bar {
    background: linear-gradient(-90deg, #84CF6A, #16C0B0);
    height: 60px;
    margin-bottom: 15px;
  }

  .product {
    display: flex;
    flex-flow: wrap;
    padding: 1rem;
  }

  img {
    border: 1px solid #d8d8d8;
    width: 70%;
    margin: 40px;
    box-shadow: 0px .5px 1px #d8d8d8;
  }
  
  .product-image {
    width: 80%;
  }
  
  .product-image,
  .product-info {
    margin-top: 10px;
    width: 50%;
  }
  
  .color-box {
    width: 40px;
    height: 40px;
    margin-top: 5px;
  }
  
  .cart {
    margin-right: 25px;
    float: right;
    border: 1px solid #d8d8d8;
    padding: 5px 20px;
  }
  
  button {
    margin-top: 30px;
    border: none;
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
    cursor: pointer;
  } 
  
  .disabledButton {
    background-color: #d8d8d8;
    cursor: not-allowed;
  }
  
  .review-form {
    width: 400px;
    padding: 20px;
    margin: 40px;
    border: 1px solid #d8d8d8;
  }

  .outOfStock {
      text-decoration: line-through;
  }
  
  input {
    width: 100%;  
    height: 25px;
    margin-bottom: 20px;
  }
  
  textarea {
    width: 100%;
    height: 60px;
  }

  .tab {
    margin-left: 20px;
    cursor: pointer;
  }

  .activeTab {
    color: #16C0B0;
    text-decoration: underline;
  }
@mohammadrezabehruz

</style>
