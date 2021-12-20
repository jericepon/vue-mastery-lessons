<template>
    <form @submit.prevent="addReview" class="review-form">
        <p>
            <label>Name</label>
            <input type="text" v-model="name" />
        </p>
        <p>
            <label>Review</label>
            <textarea v-model="review"></textarea>
        </p>
        <p>
            <label>Rating</label>
            <select v-model.number="rating">
                <option>1</option>
                <option>2</option>
                <option>3</option>
                <option>4</option>
                <option>5</option>
            </select>
        </p>

        <div v-if="errors.length">
            <p>Please correct the following errors</p>
            <ul>
                <li v-for="(error, index) in errors" :key="index">{{ error }}</li>
            </ul>
        </div>
        <!-- <button @click="addReview" type="button">Submit</button> -->
        <button type="submit">Submit</button>
    </form>
</template>
<script>
export default {
    data() {
        return {
            name: "",
            review: "",
            rating: "",
            errors: []
        };
    },
    methods: {
        addReview() {
            if (this.name && this.review && this.rating) {
                let productReview = {
                    name: this.name,
                    review: this.review,
                    rating: this.rating,
                };

                this.$emit("review-submitted", productReview);

                this.name = null;
                this.review = null;
                this.rating = null;
            } else {
                if(!this.name) this.errors.push("name is required")
                if(!this.review) this.errors.push("review is required")
                if(!this.rating) this.errors.push("rating is required")
            }
        },
    },
    emits: ["review-submitted"],
};
</script>
<style lang="">
    
</style>