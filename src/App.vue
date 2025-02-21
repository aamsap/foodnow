<script setup>
import { ref } from "vue";
import OrderSuccessModal from "@/components/OrderSuccessModal.vue";
import pizzaData from "@/assets/json/pizza-list.json";
import sizeData from "@/assets/json/size-list.json";
import toppingData from "@/assets/json/topping-list.json";

const pizzas = ref(pizzaData.data);
const sizes = ref(sizeData.data);
const toppings = ref(toppingData.data);

const selectedPizza=ref(1);
const selectedSize=ref(1);
const selectedToppings=ref([]);


const toogleActive=(id)=>{
  selectedToppings.value=[];
  selectedSize.value=1;
  selectedPizza.value=parseInt(id);
};

const toogleSize=(id)=>{
  selectedSize.value=parseInt(id);
};

const checkActive = (actid) =>{
  if(parseInt(actid)===selectedPizza.value) return "selected";
};

const checkDiscount = (dis) =>{
  if(dis) return "discounted";
};

const checkTopping = (tid) => {
  const pizza = pizzas.value.find(p => p.id === selectedPizza.value);
  if (!pizza) return "disabled";
  return pizza.toppings.includes(tid) ? "" : "disabled";
};

const toggleToppings = (id) => {
  const currentPizza = pizzas.value.find(pizza => pizza.id === selectedPizza.value);

  if (!currentPizza) return;

  if (!currentPizza.toppings.includes(id)) {
    console.log(`Topping ${id} is not available for this pizza`);
    return;
  }

  const index = selectedToppings.value.indexOf(id);
  if (index !== -1) {
    selectedToppings.value.splice(index, 1);
  } else {
    selectedToppings.value.push(id); 
  }
};

const getToppingClass = (id) => {
  return selectedToppings.value.includes(id) ? "selected" : "";
};

const getTotal  = () => {
  const pizza = pizzas.value[selectedPizza.value - 1];
  const size = sizes.value[selectedSize.value - 1];
  
  if (!pizza || !size) return 0; 
  
  const toppingsCost = selectedToppings.value.reduce((total, toppingId) => {
    const topping = toppings.value.find(t => t.id === toppingId);
    return total + (topping ? topping.price : 0);
  }, 0);

  return pizza.price + size.extra_price + toppingsCost;
};

const showModal = ref(false);

const openModal = () => {
  showModal.value = true;
};

const closeModal = () => {
  showModal.value = false;
};

</script>

<template>

  <section class="header">
    <div class="navbar">
      <img class="navbar--logo" src="./assets/img/logo.svg" alt="Foodnow">
      <ul class="navbar--menu">
          <li class="navbar--menu-item"> <a href="">Home</a></li>
          <li class="navbar--menu-item navbar--menu-item-selected"> <a href="">Order</a></li>
          <li class="navbar--menu-item"> <a href="">About</a></li>
          <li class="navbar--menu-item"> <a href="">Blog</a></li>
          <li class="navbar--menu-item"> <a href="">Contact Us</a></li>
      </ul>
      <div class="navbar--auth">
        <span class="navbar--auth-item"><a href="">Login</a></span>
        <button class="button button--orange">Register</button>
      </div>
    </div>
    <div class="hero">
      <h1>Pizza Order</h1>
    </div>
  </section>
  <section class="container">
    <div class="content">
      <div class="content--order">
        <div class="content--order-pizza">
          <h2>Choose your pizza</h2>
          <div class="pizza" v-for="pizza in pizzas" :key="pizza.id" >
            <div :class="'pizza--card '+checkDiscount(pizza.discount['is_active'])+' '+checkActive(pizza.id)" @click="toogleActive(pizza.id)">
              <div class="pizza--card-picture">
                <img :src="'/src/assets/img/pizza/'+pizza.name +'.png'" />
              </div>
              <div class="pizza--card-label">
                <div class="pizza--card-label-name">
                  {{pizza.name}}
                </div>
                <div class="pizza--card-label-price">
                  ${{pizza.price}}.00&nbsp; 
                  <span :class="checkDiscount(pizza.discount['is_active'])+' '+checkActive(pizza.id)"> ${{pizza.discount["final_price"]}} </span>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="content--order-custom">
          <h2>Custom Pizza</h2>
          <div class="custom">
            <div class="custom--label">
              Size
            </div>
            <div class="custom--option" v-for="size in sizes" :key="size.id">
              <label class="radio-button" @click="toogleSize(size.id)">
                {{ size.name }}
                <span v-if="size.extra_price>0" class="extra">(+{{ size.extra_price }}$)</span>
                <input type="radio" :checked="size.id==selectedSize" name="radio" :id="size.id">
                <span class="checkmark"></span>
              </label>
            </div>
          </div><br>
          <div class="custom">
            <div class="custom--label">
              Toppings
            </div>
            <div class="custom--option" v-for="topping in toppings" :key="topping.id" >
              <div :class="['toppings', checkTopping(topping.id), getToppingClass(topping.id)]" @click="toggleToppings(topping.id)">
                {{ topping.name }}
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="content--payment">
        <div class="card">
          <h3>Payment Summary</h3>
          <div class="card--summary">
            <div class="card--summary-item">
              <div class="card--summary-item-label">
                 {{pizzas[selectedPizza-1]['name']}}
              </div>
              <div>
                {{pizzas[selectedPizza-1]['price']}}$
              </div>
            </div>
            <div class="card--summary-item">
              <div class="card--summary-item-label">
                Size - {{ sizes[selectedSize-1]['name'] }}
              </div>
              <div>
                {{sizes[selectedSize-1]['extra_price']}}$
              </div>
            </div>
            <div class="card--summary-item" v-for="topping in selectedToppings" :key="topping">
              <div class="card--summary-item-label">
                {{toppings[topping-1]['name']}}
              </div>
              <div>
                {{toppings[topping-1]['price']}}$
              </div>
            </div>
            <hr/>
            <div class="card--summary-item">
              <div class="card--summary-item-total">
                Total Price
              </div>
              <div>
                <h3>${{ getTotal() }}.00</h3>
              </div>
            </div>
          </div>
          <div class="card--button">
            <button @click="openModal">Order Now</button>
            <OrderSuccessModal :isOpen="showModal" @close="closeModal" />
          </div>
        </div>
      </div>
    </div>
  </section>
  
  <hr/>
  
  <section class="footer">
    
    <div class="footer--section">
      <img class="footer--section-image" src="./assets/img/logo-alt.svg"/>
      <h3>Find Us :</h3>
      <div class="footer--section-icons">
        <div class="icon fb"></div>
        <div class="icon ig"></div>
        <div class="icon yt"></div>
      </div>
    </div>
    <div class="footer--section">
      <h3>Navigation</h3>
      <div class="footer--section-nav">
        <div class="route">Home</div>
        <div class="route">Contact</div>
        <div class="route">Order</div>
        <div class="route">Login</div>
        <div class="route">About</div>
        <div class="route">Register</div>
        <div class="route">Blog</div>
      </div>
    </div>
    <div class="footer--section">
      <h3>Contact</h3>
      <div class="footer--section-contact">
        <div class="contact">
          <div class="contact--icon mail"> </div>
          <div class="contact--text">Food.now@mail.com</div> 
        </div>
        <div class="contact">
          <div class="contact--icon phone"> </div> 
          <div class="contact--text">+62848477102943</div>
        </div>
        <div class="contact">
          <div class="contact--icon wa"> </div> 
          <div class="contact--text">+628184938494</div>
        </div>
      </div>
    </div>
    <div class="footer--section">
      <h3>Location</h3>
      <div class="footer--section-contact">
        <div class="contact">
          <div class="contact--icon loc"> </div>
          <div class="contact--text">
            <div class="loc">Kerobogan</div> 
            Jl Raya Kerobokan Br Taman, Kuta No.98,<br>Kerobokan Kelod, Kec. Kuta Utara,<br>Kabupaten Badung, Bali 80361
        </div> 
        </div>
      </div>
    </div>
  </section>

  <hr/>

</template>




