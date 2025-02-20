
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
          <div class="pizza">
            <div class="pizza--card">
              <div class="pizza--card-picture">
                <img src="./assets/img/pizza/Cheese Pizza.png" />
              </div>
              <div class="pizza--card-label">
                <div class="pizza--card-label-name">
                  Pizza Name
                </div>
                <div class="pizza--card-label-price">
                  $10.00&nbsp; <span class=""> $15.00 </span>
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
            <div class="custom--option">
              <label class="radio-button">Small
                <input type="radio" checked="checked" name="radio">
                <span class="checkmark"></span>
              </label>
              <label class="radio-button">Medium
                <input type="radio" name="radio">
                <span class="checkmark"></span>
              </label>
              <label class="radio-button">Large
                <input type="radio" name="radio">
                <span class="checkmark"></span>
              </label>
            </div>
          </div>
          <div class="custom">
            <div class="custom--label">
              Toppings
            </div>
            <div class="custom--option">
              <div class="toppings">
                One
              </div>
              <div class="toppings selected">
                selected
              </div>
              <div class="toppings disabled">
                disabled
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
                Pizza
              </div>
              <div>
                8$
              </div>
            </div>
            <div class="card--summary-item">
              <div class="card--summary-item-label">
                Size
              </div>
              <div>
                8$
              </div>
            </div>
            <div class="card--summary-item">
              <div class="card--summary-item-label">
                Topping
              </div>
              <div>
                8$
              </div>
            </div>
            <hr/>
            <div class="card--summary-item">
              <div class="card--summary-item-total">
                Total Price
              </div>
              <div>
                <h3>$12.00</h3>
              </div>
            </div>
          </div>
          <div class="card--button">
            <button>Order Now</button>
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


<script setup>

</script>

