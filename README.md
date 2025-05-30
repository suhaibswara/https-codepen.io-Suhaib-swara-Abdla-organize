# https-codepen.io-Suhaib-swara-Abdla-organize
Suhaiib
<!DOCTYPE html>
<html lang="ku">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>mxm - Designs for the Bold</title>
<style>
  body {
    font-family: 'Arial', sans-serif;
    background: #111;
    color: #eee;
    margin: 0;
    padding: 0;
  }
  header {
    background: #222;
    padding: 1rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  header h1 {
    font-weight: 900;
    font-size: 1.8rem;
    letter-spacing: 3px;
    color: #ff2d55;
    margin: 0;
  }
  nav a {
    color: #eee;
    text-decoration: none;
    margin-left: 1.5rem;
    font-weight: 600;
    transition: color 0.3s;
  }
  nav a:hover {
    color: #ff2d55;
  }
  .hero {
    background: url('https://images.unsplash.com/photo-1503342217505-b0a15ec3261c?auto=format&fit=crop&w=1350&q=80') center/cover no-repeat;
    height: 350px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #ff2d55;
    font-size: 2.5rem;
    font-weight: 900;
    text-shadow: 2px 2px 8px #000;
  }
  main {
    max-width: 1000px;
    margin: 2rem auto;
    padding: 0 1rem;
  }
  h2 {
    text-align: center;
    font-size: 2rem;
    margin-bottom: 1rem;
    color: #ff2d55;
  }
  .gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit,minmax(250px,1fr));
    gap: 1.5rem;
  }
  .card {
    background: #222;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 0 8px #ff2d55aa;
    display: flex;
    flex-direction: column;
  }
  .card img {
    width: 100%;
    height: 300px;
    object-fit: cover;
  }
  .card-body {
    padding: 1rem;
    flex-grow: 1;
  }
  .card-body h3 {
    margin: 0 0 0.5rem 0;
    font-weight: 700;
  }
  .card-body p {
    font-size: 0.9rem;
    color: #ccc;
    margin-bottom: 1rem;
  }
  .btn {
    background: #ff2d55;
    border: none;
    padding: 0.6rem 1.2rem;
    color: white;
    font-weight: 700;
    cursor: pointer;
    border-radius: 4px;
    transition: background 0.3s;
    width: 100%;
  }
  .btn:hover {
    background: #e0224a;
  }
  footer {
    background: #222;
    text-align: center;
    padding: 1rem 0;
    margin-top: 3rem;
    color: #777;
    font-size: 0.9rem;
  }
  .cart {
    position: fixed;
    top: 20px;
    right: 20px;
    background: #ff2d55;
    color: white;
    padding: 0.6rem 1rem;
    border-radius: 25px;
    font-weight: 700;
    cursor: pointer;
    box-shadow: 0 0 10px #ff2d55aa;
    user-select: none;
  }
  .cart-count {
    background: #fff;
    color: #ff2d55;
    border-radius: 50%;
    padding: 0 7px;
    margin-left: 6px;
    font-size: 0.9rem;
  }

  /* Checkout modal */
  #checkoutModal {
    display:none; 
    position: fixed; 
    top:0; left:0; 
    width:100vw; height:100vh; 
    background: rgba(0,0,0,0.85); 
    color:#fff; 
    font-family: Arial, sans-serif; 
    z-index: 9999; 
    justify-content: center; 
    align-items: center;
  }
  #checkoutModal > div {
    background:#222; 
    padding: 2rem; 
    border-radius: 8px; 
    max-width: 400px; 
    width: 90%;
  }
  #checkoutModal h2 {
    margin-top: 0;
  }
  #checkoutModal label {
    display: block;
    margin-top: 1rem;
    font-weight: 600;
  }
  #checkoutModal input, #checkoutModal textarea {
    width: 100%; 
    padding: 0.5rem; 
    margin-top: 0.3rem;
    border-radius: 4px;
    border: none;
  }
  #checkoutModal button {
    margin-top: 1.5rem;
    padding: 0.6rem 1.2rem;
    font-weight: 700;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  #checkoutModal button.submitBtn {
    background:#ff2d55;
    color:#fff;
  }
  #checkoutModal button.cancelBtn {
    background:#444;
    color:#fff;
    margin-left: 1rem;
  }
</style>
</head>
<body>

<header>
  <h1>mxm</h1>
  <nav>
    <a href="#gallery">Shop</a>
    <a href="#about">About</a>
  </nav>
</header>

<div class="hero">Designs for the Bold</div>

<main>
  <h2 id="gallery">Gallery of Designs</h2>
  <div class="gallery" id="designs">
    <!-- Design Cards will be inserted here -->
  </div>
</main>

<div class="cart" id="cartBtn">
  Cart <span class="cart-count" id="cartCount">0</span>
</div>

<footer id="about">
  &copy; 2025 mxm. All rights reserved. Designed with passion.
</footer>

<!-- Checkout modal -->
<div id="checkoutModal">
  <div>
    <h2>Checkout - Submit Your Order</h2>
    <form id="checkoutForm">
      <label for="name">Name:</label>
      <input type="text" id="name" name="name" required />

      <label for="email">Email:</label>
      <input type="email" id="email" name="email" required />

      <label for="note">Additional Notes:</label>
      <textarea id="note" name="note" rows="3" placeholder="Any special requests?"></textarea>

      <button type="submit" class="submitBtn">Submit Order</button>
      <button type="button" id="cancelBtn" class="cancelBtn">Cancel</button>
    </form>
  </div>
</div>

<script>
  // Sample design data
  const designs = [
    {
      id: 1,
      name: "Velvet Seduction",
      desc: "A sultry velvet dress with bold lines and sleek fit.",
      img: "https://images.unsplash.com/photo-1520975912117-5d4c59d58d6a?auto=format&fit=crop&w=500&q=80"
    },
    {
      id: 2,
      name: "Crimson Edge",
      desc: "Daring red outfit designed for the fearless.",
      img: "https://images.unsplash.com/photo-1514996937319-344454492b37?auto=format&fit=crop&w=500&q=80"
    },
    {
      id: 3,
      name: "Midnight Glam",
      desc: "Elegant black dress perfect for night outs.",
      img: "https://images.unsplash.com/photo-1508214751196-bcfd4ca60f91?auto=format&fit=crop&w=500&q=80"
    },
    {
      id: 4,
      name: "Golden Hour",
      desc: "Shimmering gold dress that turns heads.",
      img: "https://images.unsplash.com/photo-1503342217505-b0a15ec3261c?auto=format&fit=crop&w=500&q=80"
    }
  ];

  const gallery = document.getElementById('designs');
  const cartBtn = document.getElementById('cartBtn');
  const cartCount = document.getElementById('cartCount');
  const checkoutModal = document.getElementById('checkoutModal');
  const checkoutForm = document.getElementById('checkoutForm');
  const cancelBtn = document.getElementById('cancelBtn');
  let cart = [];

  // Render designs
  function renderDesigns() {
    designs.forEach(d => {
      const card = document.createElement('div');
      card.className = 'card';
      card.innerHTML = `
        <img src="${d.img}" alt="${d.name}" />
        <div class="card-body">
          <h3>${d.name}</h3>
          <p>${d.desc}</p>
          <button class="btn" data-id="${d.id}">Add to Cart</button>
        </div>
      `;
      gallery.appendChild(card);
    });
  }

  // Update cart count
  function updateCartCount() {
    cartCount.textContent = cart.length;
  }

  // Add to cart handler
  gallery.addEventListener('click', e => {
    if(e.target.classList.contains('btn')){
      const id = parseInt(e.target.getAttribute('data-id'));
      const design = designs.find(d => d.id === id);
      if(design){
        cart.push(design);
        updateCartCount();
        alert(`${design.name} added to cart.`);
      }
    }
  });

  // Show checkout modal on cart click
  cartBtn.addEventListener('click', () => {
    if(cart.length === 0){
      alert("Your cart is empty.");
      return;
    }
    checkoutModal.style.display = 'flex';
  });

  // Cancel button in checkout
  cancelBtn.addEventListener('click', () => {
    checkoutModal.style.display = 'none';
  });

  // Handle form submit
  checkoutForm.addEventListener('submit', (e) => {
    e.preventDefault();
    const name = checkoutForm.name.value.trim();
    const email = checkoutForm.email.value.trim();
    const note = checkoutForm.note.value.trim();

    if(!name || !email){
      alert("Please fill in all required fields.");
      return;
    }

    alert(`Thank you, ${name}! Your order has been received.\nWe will contact you at ${email} soon.`);

    // Clear cart and update
    cart = [];
    updateCartCount();
    checkoutForm.reset();
    checkoutModal.style.display = 'none';
  });

  renderDesigns();
</script>

</body>
</html>
