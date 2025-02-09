<template>
    <div class="relative group">
      <!-- Card Container -->
      <div class="relative w-full h-96 [transform-style:preserve-3d] transition-transform duration-700 group-hover:[transform:rotateY(180deg)]">
        <!-- Front Side -->
        <div class="absolute inset-0 [backface-visibility:hidden]">
          <div class="relative w-full h-full">
            <img
              v-if="userType === 'her'"
              src="@/assets/img/for-her.jpg"
              alt="For Her"
              class="h-full w-full rounded-bl-3xl rounded-tr-3xl border border-gray-300 object-cover"
            />
  
            <img
              v-if="userType === 'him'"
              src="@/assets/img/for-him.jpg"
              alt="For Him"
              class="h-full w-full rounded-bl-3xl rounded-tr-3xl border border-gray-300 object-cover"
            />
            <div class="absolute inset-0 bg-black/50 flex items-center justify-center rounded-bl-3xl rounded-tr-3xl">
              <h3 class="text-2xl font-semibold text-white text-center px-4">
                {{ product?.name ?? 'Nil' }}
              </h3>
            </div>
          </div>
        </div>
  
        <!-- Back Side -->
        <div class="absolute inset-0 [transform:rotateY(180deg)] [backface-visibility:hidden] bg-white rounded-bl-3xl rounded-tr-3xl border border-gray-300 p-6 flex flex-col justify-between">
          <div>
            <h3 class="text-xl font-semibold text-gray-900">{{ product?.name ?? 'Nil' }}</h3>
            <p class="mt-2 text-gray-700 text-sm">{{ product?.description ?? 'Nil' }}</p>
            <ul class="mt-4 text-sm text-gray-600 list-disc list-inside">
              <li v-for="(item, index) in product?.items" :key="index">{{ item }}</li>
            </ul>
          </div>
          <button
            @click="openModal"
            class="mt-6 block w-full rounded-md border border-indigo-900 bg-indigo-900 px-5 py-3 text-sm font-medium uppercase tracking-widest text-white transition-colors hover:bg-white hover:text-indigo-900"
          >
            Place Order
          </button>
        </div>
      </div>
  
      <!-- Discount Label -->
      <span class="absolute -right-px -top-px rounded-bl-3xl rounded-tr-3xl bg-rose-600 px-6 py-4 font-medium uppercase tracking-widest text-white">
        Save 10%
      </span>
  
      <!-- Modal -->
      <Teleport to="body">
        <Transition
          enter-active-class="transition duration-300 ease-out"
          enter-from-class="transform opacity-0"
          enter-to-class="opacity-100"
          leave-active-class="transition duration-200 ease-in"
          leave-from-class="opacity-100"
          leave-to-class="transform opacity-0"
        >
          <div v-if="isModalOpen" class="fixed inset-0 z-50 flex items-center justify-center">
            <!-- Modal Backdrop -->
            <div 
              class="fixed inset-0 bg-black/70 backdrop-blur-sm"
              @click="closeModal"
            ></div>
  
            <!-- Modal Content -->
            <div class="relative bg-white rounded-lg shadow-lg p-6 w-full max-w-lg mx-4 animate-fadeIn">
              <h3 class="text-2xl font-semibold text-gray-900">Complete Your Order</h3>
              <p class="mt-2 text-gray-600">Enter your details to proceed with your order.</p>
  
              <div class="max-h-[400px] overflow-y-auto custom-scrollbar mt-4 pr-2">
                <form @submit.prevent="submitOrder" class="mt-4">
                <!-- Full Name -->
                <div class="mb-4">
                  <label for="name" class="block text-sm font-medium text-gray-700">Full Name</label>
                  <input
                    id="name"
                    v-model="orderDetails.name"
                    type="text"
                    class="mt-1 w-full px-3 py-3 outline-none text-sm bg-gray-25 border rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500"
                    placeholder="Enter your full name"
                    required
                  />
                </div>
  
                <!-- Phone Number -->
                <div class="mb-4">
                  <label for="phone" class="block text-sm font-medium text-gray-700">Phone Number</label>
                  <input
                    id="phone"
                    v-model="orderDetails.phone"
                    type="tel"
                    class="mt-1 w-full px-3 py-3 outline-none text-sm bg-gray-25 border rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500"
                    placeholder="Enter your phone number"
                    required
                  />
                </div>
  
                <!-- Delivery Option -->
                <div class="mb-4">
                  <label for="deliveryOption" class="block text-sm font-medium text-gray-700">Pickup or Delivery?</label>
                  <select
                    id="deliveryOption"
                    v-model="orderDetails.deliveryOption"
                    class="mt-1 w-full px-3 py-3 outline-none text-sm bg-gray-25 border rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500"
                  >
                    <option value="pickup">Pickup</option>
                    <option value="delivery">Delivery</option>
                  </select>
                </div>
  
                <!-- Delivery Address -->
                <div v-if="orderDetails.deliveryOption === 'delivery'" class="mb-4">
                  <label for="address" class="block text-sm font-medium text-gray-700">Delivery Address</label>
                  <input
                    id="address"
                    v-model="orderDetails.address"
                    type="text"
                    class="mt-1 w-full px-3 py-3 outline-none text-sm bg-gray-25 border rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500"
                    placeholder="Enter delivery address"
                    required
                  />
                </div>
  
                <!-- Payment Option -->
                <div class="mb-4">
                  <label for="paymentOption" class="block text-sm font-medium text-gray-700">Payment Option</label>
                  <select
                    id="paymentOption"
                    v-model="orderDetails.paymentOption"
                    class="mt-1 w-full px-3 py-3 outline-none text-sm bg-gray-25 border rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500"
                  >
                    <option value="pay_on_delivery">Pay on Delivery</option>
                    <option value="pay_now">Pay Now</option>
                  </select>
                </div>
  
                <!-- Bank Details -->
                <div v-if="orderDetails.paymentOption === 'pay_now'" class="mb-4 p-4 bg-gray-50 rounded-lg">
                  <p class="text-sm text-gray-800 font-semibold">Bank Account Details</p>
                  <p class="text-sm text-gray-600">Bank Name: United Bank Of Africa (UBA)</p>
                  <p class="text-sm text-gray-600">Account Name: Orina Deborah</p>
                  <p class="text-sm text-gray-600">Account Number: <span class="font-semibold">2145448570</span></p>
                  <button 
                    type="button"
                    @click="copyAccountNumber"
                    class="mt-2 text-indigo-600 text-sm hover:text-indigo-800 underline"
                  >
                    Copy Account Number
                  </button>
                  <p class="mt-2 text-sm text-red-500">⚠️ Send evidence of payment to WhatsApp (+234 818 610 9007) after payment.</p>
                </div>
  
                <!-- Action Buttons -->
                <div class="mt-6 flex justify-between gap-4 pt-6">
                  <button
                    type="button"
                    @click="closeModal"
                    class="flex-1 px-5 py-3 outline-none text-sm bg-gray-25 text-gray-600 border rounded-lg hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-gray-200"
                  >
                    Cancel
                  </button>
                  <button
                    type="submit"
                    class="flex-1 px-5 py-3 outline-none text-sm bg-indigo-600 text-white rounded-lg focus:outline-none focus:ring-2 focus:ring-indigo-500"
                  >
                    Confirm Order
                  </button>
                </div>
              </form>
              </div>
            </div>
          </div>
        </Transition>
      </Teleport>
    </div>
  </template>
  
  <script setup lang="ts">
  interface Product {
    name: string;
    description: string;
    items: string[];
    new_price: number;
  }
  
  interface OrderDetails {
    name: string;
    phone: string;
    deliveryOption: 'pickup' | 'delivery';
    address: string;
    paymentOption: 'pay_on_delivery' | 'pay_now';
  }
  
  interface Props {
    userType: 'him' | 'her';
    product?: Product;
  }
  
  const props = withDefaults(defineProps<Props>(), {
    userType: 'her',
    product: () => ({
      name: '',
      description: '',
      items: [],
      new_price: 0
    })
  });
  
  const isModalOpen = ref(false);
  const orderDetails = ref<OrderDetails>({
    name: '',
    phone: '',
    deliveryOption: 'pickup',
    address: '',
    paymentOption: 'pay_on_delivery'
  });
  
  const openModal = () => {
    isModalOpen.value = true;
    // Prevent body scroll when modal is open
    document.body.style.overflow = 'hidden';
  };
  
  const closeModal = () => {
    isModalOpen.value = false;
    // Restore body scroll when modal is closed
    document.body.style.overflow = 'unset';
  };
  
  const copyAccountNumber = () => {
    navigator.clipboard.writeText('2145448570');
    alert('Account number copied to clipboard!');
  };
  
  const submitOrder = () => {
  // Build the WhatsApp message text dynamically
  const message = `Hello,%20I%20would%20like%20to%20place%20an%20order.%20Here%20are%20my%20details:%0A%0A` +
    `Name:%20${encodeURIComponent(orderDetails.value.name)}%0A` +
    `Phone:%20${encodeURIComponent(orderDetails.value.phone)}%0A` +
    `Delivery%20Option:%20${encodeURIComponent(orderDetails.value.deliveryOption)}%0A` +
    (orderDetails.value.deliveryOption === "delivery"
      ? `Address:%20${encodeURIComponent(orderDetails.value.address || "N/A")}%0A`
      : "") +
    `Payment%20Method:%20${encodeURIComponent(orderDetails.value.paymentOption)}%0A` +
    `Selected%20Package:%20${encodeURIComponent(props.product.name)}%0A` +
    `Price:%20${encodeURIComponent(props.product.new_price)}%0A%0A` +
    `Thank%20you!`;

    // Open WhatsApp with the generated message
    window.open(`https://wa.me/2349012345678?text=${message}`, "_blank");
    closeModal();
};

  
  // Cleanup on component unmount
  onUnmounted(() => {
    document.body.style.overflow = 'unset';
  });
  </script>
  
  <style scoped>
  @keyframes fadeIn {
    from {
      opacity: 0;
      transform: scale(0.95);
    }
    to {
      opacity: 1;
      transform: scale(1);
    }
  }

  .custom-scrollbar::-webkit-scrollbar {
  width: 6px;
}

.custom-scrollbar::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 10px;
}

.custom-scrollbar::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 10px;
}

.custom-scrollbar::-webkit-scrollbar-thumb:hover {
  background: #555;
}
  
  .animate-fadeIn {
    animation: fadeIn 0.3s ease-out forwards;
  }
  </style>