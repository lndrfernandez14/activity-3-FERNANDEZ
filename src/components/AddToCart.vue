<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Prelim Activity 3</title>
  <script src="https://cdn.jsdelivr.net/npm/vue@2"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
  <style>
    /* CSS styles */
    .container {
      margin: 20px;
    }
    .title {
      font-size: 24px;
      color: #fff;
      background-color: rgb(0, 144, 211);
      padding: 10px;
      border-radius: 4px;
    }
    .product-container {
      display: flex;
      flex-wrap: wrap;
    }
    .product {
      margin: 10px;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
      width: 200px;
    }
    .product-name {
      font-weight: bold;
    }
    .product-price {
      color: green;
    }
    .cart-container {
      margin-top: 20px;
    }
    .cart {
      border: 1px solid #ccc;
      border-radius: 4px;
      padding: 10px;
    }
    .total-price {
      font-weight: bold;
      margin-top: 10px;
    }
  </style>
</head>
<body>

<div id="app" class="container">
  <!-- Vue App -->
  <h1 class="title">Interactive Shopping Cart in Vue.js</h1>
  
  <!-- Products -->
  <div class="product-container">
    <div class="product" v-for="(product, index) in products" :key="index">
      <h3 class="product-name">{{ product.name }}</h3>
      <p class="product-price">Price: ${{ product.price }}</p>
      <input type="number" v-model="product.quantity" placeholder="Quantity">
      <button @click="addToCart(index)">
        <i class="fas fa-cart-plus"></i> Add to Cart
      </button>
    </div>
  </div>

  <!-- Cart -->
  <div class="cart-container">
    <h2 class="title">CART</h2>
    <div class="cart">
      <ul>
        <li v-for="(item, index) in cart" :key="index">
          {{ item.name }} - ${{ item.price * item.quantity }} ({{ item.quantity }})
          <input type="number" v-model="item.quantity" @change="updateQuantity(index)">
          <button @click="removeFromCart(index)">
            <i class="fas fa-trash-alt"></i> Remove
          </button>
        </li>
      </ul>
      <p class="total-price">Total Price: ${{ getTotalPrice() }}</p>
    </div>
  </div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    products: [
      { name: 'Product 1', price: 10, quantity: 0 },
      { name: 'Product 2', price: 20, quantity: 0 },
      { name: 'Product 3', price: 30, quantity: 0 },
      { name: 'Product 4', price: 40, quantity: 0 },
      { name: 'Product 5', price: 50, quantity: 0 },
      { name: 'Product 6', price: 60, quantity: 0 },
      { name: 'Product 7', price: 70, quantity: 0 },
      { name: 'Product 8', price: 80, quantity: 0 }
    ],
    cart: []
  },
  methods: {
    addToCart(index) {
      if (this.products[index].quantity > 0) {
        this.cart.push({
          ...this.products[index],
          quantity: this.products[index].quantity
        });
        this.products[index].quantity = 0; 
      }
    },
    removeFromCart(index) {
      this.cart.splice(index, 1);
    },
    updateQuantity(index) {
      if (this.cart[index].quantity <= 0) {
        this.cart.splice(index, 1); 
    },
    getTotalPrice() {
      let total = 0;
      this.cart.forEach(item => {
        total += item.price * item.quantity;
      });
      return total;
    }
  }
});
</script>

</body>
</html>
