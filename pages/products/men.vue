<template>
    <main>
        <div class="relative isolate overflow-hidden py-24 sm:py-32">
            <div class="absolute inset-0 -z-10">
        <img
            src="@/assets/img/men1.jpg"
            alt="Men's Valentine Gift Packages"
            class="absolute inset-0 h-full w-full object-cover object-right md:object-center"
        />
        <!-- Dark Transparent Overlay -->
        <div class="absolute inset-0 bg-black bg-opacity-60"></div>
    </div>

    <div class="mx-auto max-w-7xl px-6 lg:px-8">
        <div class="mx-auto max-w-2xl lg:mx-0">
            <h2 class="text-5xl font-semibold tracking-tight text-white sm:text-7xl">
                For Him: Thoughtful Gifts for the Modern Man 🎩💙
            </h2>
            <p class="mt-8 text-white text-pretty text-lg font-medium text-gray-400 sm:text-xl/8">
                Finding the perfect gift for him just got easier! Whether he’s into 
                <span class="text-blue-400 font-semibold">comfort, style, or luxury</span>, 
                our specially curated <span class="text-blue-400 font-semibold">Valentine’s gift packages</span> 
                offer the perfect blend of <span class="text-blue-400 font-semibold">practicality and sentiment</span>.  
            </p>
            <p class="mt-6 text-lg font-semibold text-white">
                💙 Show him you care with a gift he’ll truly appreciate!
            </p>
        </div>
    </div>
        </div>


<div class="grid grid-cols-1 gap-6 lg:grid-cols-3 lg:gap-10 mt-20 max-w-7xl mx-auto p-6 lg:p-0">
    <Product
            v-for="item in menPackages"
            userType="him"
            :product="item"
            :key="item.name"
        />
</div>
    </main>
</template>


<script setup lang="jsx">
import { ref } from "vue";

const menPackages = ref([
    {
        "name": "Classic Comfort Package",
        "old_price": "25k",
        "new_price": "20k",
        "description": "A cozy and thoughtful gift package for relaxation. Perfect for those who appreciate comfort and a personal touch.",
        "items": [
            "Pyjamas",
            "Customized letter",
            "A box of small chops"
        ]
    },
    {
        "name": "Sweet Indulgence Package",
        "old_price": "30k",
        "new_price": "25k",
        "description": "A delightful mix of comfort and treats, featuring chocolate, scented body spray, and a heartfelt customized letter.",
        "items": [
            "Pyjamas",
            "Chocolate",
            "Body spray",
            "Customized letter",
            "A box of small chops"
        ]
    },
    {
        "name": "Premium Comfort Package",
        "old_price": "35k",
        "new_price": "30k",
        "description": "For the modern gentleman who values both style and sentiment. Includes a premium wallet, luxury pyjamas, and gourmet treats.",
        "items": [
            "Wallet",
            "Chocolate",
            "Customized letter",
            "A box of small chops",
            "Quality cotton pyjamas"
        ]
    },
    {
        "name": "Luxury Delight Package",
        "old_price": "60k",
        "new_price": "50k",
        "description": "A high-end, indulgent gift set for the man who deserves the best. Featuring silk pyjamas, handmade slippers, and a premium wallet.",
        "items": [
            "Wallet",
            "A pack of boxers",
            "Customized letter",
            "Luxury silk pyjamas",
            "A box of small chops",
            "Quality handmade slippers"
        ]
    }
]);
</script>