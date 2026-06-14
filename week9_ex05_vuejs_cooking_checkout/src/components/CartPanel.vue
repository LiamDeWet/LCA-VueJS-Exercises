<template>
  <aside class="cart-panel">
    <h2>🛒 Cart</h2>

    <div v-if="cart.length === 0" class="empty-cart">Your cart is empty.</div>

    <TransitionGroup name="cart" tag="div">
      <div v-for="item in cart" :key="item.id" class="cart-item">
        <strong>
          {{ item.date }}
        </strong>
        <p>R{{ item.price }}</p>

        <div class="qty-controls">
          <button @click="$emit('decrease', item.id)">-</button>
          <span>
            {{ item.quantity }}
          </span>
          <button @click="$emit('increase', item.id)">+</button>
        </div>
        <button class="remove" @click="$emit('remove', item.id)">Remove</button>
      </div>
    </TransitionGroup>

    <div class="coupon">
      <input
        :value="couponCode"
        @input="$emit('update:couponCode', $event.target.value.toUpperCase())"
        placeholder="Enter SAVE10"
      />

      <button @click="$emit('applyCoupon')">Apply</button>

      <p v-if="discountApplied" class="success">
        ✅ SAVE10 applied successfully!
      </p>
    </div>

    <div class="summary">
      <p>Subtotal: R{{ subtotal.toFixed(2) }}</p>
      <p>Discount: -R{{ discount.toFixed(2) }}</p>
      <p>VAT: R{{ tax.toFixed(2) }}</p>
      <h3>Total: R{{ grandTotal.toFixed(2) }}</h3>
    </div>

    <button class="clear" @click="$emit('clear')">Clear Cart</button>
  </aside>
</template>

<script setup>
defineProps({
  cart: Array,
  subtotal: Number,
  discount: Number,
  tax: Number,
  grandTotal: Number,
  couponCode: String,
  discountApplied: Boolean,
});
</script>
