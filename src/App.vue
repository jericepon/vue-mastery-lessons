<template>
    <div class="nav-bar">
        <img id="logo" alt="Vue logo" src="./assets/logo.png" />
        <div class="cart">
            <p>Cart ({{ cart.length }})</p>
        </div>
    </div>
    <Product @add-to-cart="updateCart" :premium="premium" />
    <Tab @selected-tab-content="selectTabContent" :tabs="tabs">
        <div class="tab-content" :class="{ active: selectedTabContent == 0 }">
            <h2>Reviews</h2>
            <p v-if="!reviews.length">There are no reviews yet.</p>
            <ul>
                <li v-for="(item, index) in reviews" :key="index">
                    {{ item.review }}
                </li>
            </ul>
        </div>
        <div class="tab-content" :class="{ active: selectedTabContent == 1 }">
            <ProductReview @review-submitted="addReview" />
        </div>
    </Tab>
</template>

<script>
import Product from "./components/Product.vue";
import ProductReview from "./components/ProductReview.vue";
import Tab from "./components/Tab.vue";
export default {
    components: { Product, ProductReview, Tab },
    data() {
        return {
            premium: true,
            cart: [],
            reviews: [],
            tabs: [
                { index: 0, text: "Reviews" },
                { index: 1, text: "Make a review" },
            ],
            selectedTabContent: 0,
        };
    },
    methods: {
        updateCart(variantId) {
            this.cart.push(variantId);
        },
        addReview(productReview) {
            console.log(productReview);
            this.reviews.push(productReview);
        },
        selectTabContent(tab) {
            this.selectedTabContent = tab.index;
        },
    },
    emits: ["eview-submitted"],
};
</script>

<style>
.tab-content:not(.active) {
    display: none;
}
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

</style>
