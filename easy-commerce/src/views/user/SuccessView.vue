<script setup>
import { onMounted } from 'vue';
import { ref } from 'vue';
import UserLayout from '@/layouts/UserLayout.vue';

import { useCartStore } from "@/stores/user/cart";

const cartStore = useCartStore();
const orderData = ref({})

onMounted(() => {
    cartStore.loadCheckout()
    if (cartStore.checkout.orderNumber) {
        orderData.value = cartStore.checkout
    }
})

</script>

<template>
    <UserLayout>
        <div class="max-w-2xl mx-auto border border-base-200 shadow-xl p-8 my-4">
            <div>
                <div class="text-2xl font-bold flex justify-center">Your order is successfull 🎉</div>
                <div class="flex justify-center">Hi {{ orderData.name }}</div>
                <div class="flex justify-center">เตรียมรอรับสินค้าของคุณได้เลย 😊</div>
            </div>
            <div class="divider"></div>
            <div class="grid grid-cols-4 gap-2">
                <div>
                    <div class="font-bold">Order data</div>
                    <div>{{ orderData.createdData }}</div>
                </div>
                <div class="mx-auto">
                    <div class="font-bold">Order Number</div>
                    <div>{{ orderData.orderNumber }}</div>
                </div>
                <div class="mx-auto">
                    <div class="font-bold">Payment method</div>
                    <div>{{ orderData.paymentMethod }}</div>
                </div>
                <div class="mx-auto">
                    <div class="font-bold">Address</div>
                    <div>{{ orderData.address }}</div>
                </div>
            </div>
            <div class="divider"></div>
            <div v-for="product in orderData.products" class="grid grid-cols-4 gap-2 mb-4 items-center">
                <div>
                    <img class="w-full" :src="product.imageUrl">
                </div>
                <div>
                    <div class="font-bold">
                        photo
                    </div>
                    {{ product.name }}
                </div>
                <div>
                    จำนวน {{ product.quantity }}
                </div>
                <div>
                    {{ product.price * product.quantity }} ฿
                </div>
            </div>
            <div class="divider"></div>
            <div class="flex justify-between my-4">
                <div class="font-bold">ราคาสินค้าทั้งหมด</div>
                <div>{{ orderData.totalPrice }} ฿</div>
            </div>
            <div class="flex justify-between">
                <div class="font-bold">ค่าส่ง</div>
                <div>0 ฿</div>
            </div>
            <div class="divider"></div>
            <div class="flex justify-between my-4">
                <div class="font-bold">ราคาทั้งสิ้น</div>
                <div>{{ orderData.totalPrice }} ฿</div>
            </div>
            <div class="divider"></div>
            <div class="text-xl font-bold flex justify-center">
                ขอบคุณสําหรับการสั่งซื้อ 🫶🫶🫶
            </div>
        </div>
    </UserLayout>
</template>