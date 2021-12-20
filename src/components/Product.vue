<template lang="">
     <div class="product">
        <div class="product-image">
            <img :src="image" alt="" />
        </div>

        <div class="product-info">
            <h1>{{ product }}</h1>
            <p v-show="premium">User is premium</p>
            <p>Shipping: {{ shipping }}</p>
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
    props: ['premium'],
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
        this.product = this.variants[this.selectedVariant].name;
        this.image = this.variants[this.selectedVariant].variantImage;
    },
    computed: {
        shipping() {
            if(this.premium) return "Free"

            return 2.99
        }
    }
};
</script>
<style lang="">
    
</style>