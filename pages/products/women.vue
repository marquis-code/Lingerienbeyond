<template>
    <main>
        <div class="relative isolate overflow-hidden py-24 sm:py-32">
            <div class="absolute inset-0 -z-10">
        <img
            src="@/assets/img/women-gifts.jpg"
            alt="Men's Valentine Gift Packages"
            class="absolute inset-0 h-full w-full object-cover object-right md:object-center"
        />
        <!-- Dark Transparent Overlay -->
        <div class="absolute inset-0 bg-black bg-opacity-60"></div>
    </div>
            
            <div class="mx-auto max-w-7xl px-6 lg:px-8">
                <div class="mx-auto max-w-2xl lg:mx-0">
                    <h2
                        class="text-5xl font-semibold tracking-tight text-white sm:text-7xl"
                    >For Her: Thoughtful Gifts to Make Her Feel Special 💖</h2>
                    <p class="mt-8 text-pretty text-lg font-medium text-white sm:text-xl/8">
                Celebrate love this Valentine’s season with a touch of elegance and care!  
                Finding the perfect gift can be tricky, but we’ve made it easier with carefully curated 
                <span class="text-pink-400 font-semibold">affordable yet luxurious</span> 
                Valentine’s gift packages for her. Whether she loves cozy nights in, pampering self-care, or 
                elegant fashion pieces, we have something <span class="text-pink-400 font-semibold">perfect</span> 
                to make her feel truly cherished.  
            </p>

                </div>
            </div>
        </div>

       <div class="grid grid-cols-1 gap-6 lg:grid-cols-3 lg:gap-10 mt-20 container mx-auto p-6 lg:p-0">
        <Product
           userType="her"
            v-for="item in menPackages"
            :product="item"
            :key="item.name"
        />
       </div>
    </main>
</template>

<script setup lang="jsx">
const menPackages = ref([
  {
    "name": "Elegant Night Package",
    "old_price": "20k",
    "new_price": "15k",
    "description": "Perfect for a cozy and relaxing night in! Soft nightgown paired with a refreshing body spray and a heartfelt customized letter.",
    "items": [
      "Night gown",
      "Body spray",
      "Customized letter"
    ]
  },
  {
    "name": "Chic Comfort Package",
    "old_price": "25k",
    "new_price": "20k",
    "description": "Stay stylish and comfortable! A complete self-care package with lounge wear, body spray, and a sweet treat—perfect for students looking to unwind.",
    "items": [
      "Body spray",
      "Lounge wear",
      "Customized letter",
      "A box of small chops",
      "Crochet statement earrings"
    ]
  },
  {
    "name": "Luxury Essence Package",
    "old_price": "35k",
    "new_price": "30k",
    "description": "Elevate your self-care with this luxury package featuring an elegant perfume, premium sleepwear, and delicious small chops. Ideal for those who love a touch of class.",
    "items": [
      "Perfume",
      "Customized letter",
      "A box of small chops",
      "Crochet statement earrings",
      "Quality cotton pyjamas / lingerie"
    ]
  },
  {
    "name": "Opulent Glam Package",
    "old_price": "60k",
    "new_price": "50k",
    "description": "The ultimate indulgence package! Featuring a bottle of wine, silk robe, handmade slippers, and statement accessories—crafted for queens who love the finer things in life.",
    "items": [
      "A bottle of wine",
      "Customized letter",
      "A box of small chops",
      "Crochet hair scrunchie",
      "Luxury silk pyjamas / robe",
      "Quality handmade slippers",
      "Crochet statement earrings"
    ]
  }
])
</script>