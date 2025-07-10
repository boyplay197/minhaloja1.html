<!DOCTYPE html>
<html lang="pt-BR">
<head> 
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1"/>
<title>Loja de Grife Futurista - Espaço & Luxo</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@500&family=Rajdhani:wght@400;700&display=swap');
  :root {
    --color-primary: #7ef9ff;
    --color-secondary: #ff6ff8;
    --color-accent: #ff3dff;
    --color-dark: #0a001a;
    --color-light: #fff6ff;
  }
  * { box-sizing: border-box; margin:0; padding:0; }
  body {
    background: #0a001a;
    color: var(--color-light);
    font-family: 'Rajdhani', sans-serif;
    overflow-x: hidden;
    min-height: 100vh;
    position: relative;
  }
  header {
    padding: 1rem 2rem;
    text-align: center;
    font-size: 2.5rem;
    color: var(--color-primary);
    text-shadow: 0 0 8px var(--color-primary), 0 0 20px var(--color-secondary);
    position: relative; z-index:10;
  }
  main {
    max-width: 1280px;
    margin: 0 auto;
    padding: 2rem 1rem 4rem;
    position: relative;
    z-index: 10;
  }
  .filters { display: none; } /* oculto, pois não estamos focando nos filtros */
  .products {
    display: grid;
    grid-template-columns: repeat(auto-fill,minmax(300px,1fr));
    gap: 2rem;
  }
  .product-card {
    background: linear-gradient(145deg, #11002f, #220048);
    border-radius: 16px;
    box-shadow: 0 0 20px var(--color-primary), inset 0 0 10px var(--color-secondary);
    overflow: hidden;
    display: flex;
    flex-direction: column;
    transition: transform .3s, box-shadow .3s;
    cursor: pointer;
  }
  .product-card:hover {
    transform: translateY(-10px) scale(1.05);
    box-shadow: 0 0 40px var(--color-primary), 0 0 60px var(--color-accent), inset 0 0 20px var(--color-secondary);
    z-index: 5;
  }
  .product-card img {
    width: 100%;
    aspect-ratio: 4/5;
    object-fit: cover;
    border-bottom: 2px solid var(--color-accent);
    filter: drop-shadow(0 0 10px var(--color-primary));
  }
  .product-info {
    padding: 1rem 1.5rem 1.5rem;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  .product-category {
    font-size: 0.9rem;
    text-transform: uppercase;
    color: var(--color-secondary);
    letter-spacing: .15em;
    margin-bottom: .3rem;
  }
  .product-title {
    font-size: 1.6rem;
    color: var(--color-primary);
    text-shadow: 0 0 6px var(--color-primary), 0 0 12px var(--color-accent);
    margin-bottom: .4rem;
  }
  .product-desc {
    flex-grow: 1;
    font-size: 1rem;
    margin-bottom: 1rem;
    color: #d4bbff;
    text-shadow: 0 0 4px #a97fff;
  }
  .product-price {
    font-weight: 700;
    font-size: 1.3rem;
    color: var(--color-accent);
    margin-bottom: 1rem;
    text-shadow: 0 0 10px var(--color-accent);
  }
  .btn-buy {
    background: linear-gradient(135deg, var(--color-primary), var(--color-accent));
    color: var(--color-dark);
    border: none;
    border-radius: 40px;
    padding: .8rem 1.8rem;
    font-weight:700;
    font-size:1.1rem;
    letter-spacing:.1em;
    cursor: pointer;
    box-shadow:0 0 20px var(--color-primary), 0 0 40px var(--color-accent);
    transition: background .3s, transform .2s;
  }
  .btn-buy:hover {
    background: linear-gradient(135deg, var(--color-accent), var(--color-primary));
    transform: scale(1.1);
  }
  #cartToggle {
    position: fixed;
    bottom:2rem; right:2rem;
    background: var(--color-accent);
    color: var(--color-dark);
    border:none;border-radius:50%;
    width:60px;height:60px;
    font-size:1.8rem;
    box-shadow:0 0 20px var(--color-accent);
    cursor:pointer;
    z-index:50;
  }
  #cartPanel {
    position:fixed;
    top:0; right:-400px;
    width:380px; height:100vh;
    background: rgba(10,0,26,.95);
    box-shadow:-5px 0 20px rgba(255,0,255,.7);
    backdrop-filter: blur(12px);
    padding:1.5rem 2rem 2rem;
    display:flex;flex-direction:column;
    transition: right .35s;
    z-index:60;
  }
  #cartPanel header {
    display:flex; justify-content:space-between; align-items:center;
    font-family:'Orbitron',sans-serif;
    letter-spacing:.1em;
    font-size:1.5rem;
    color:var(--color-primary);
    margin-bottom:1.5rem;
  }
  #cartPanel header button {
    background:transparent;
    border:none;
    color:var(--color-accent);
    font-size:2rem;
    cursor:pointer;
  }
  #cartItems {
    flex-grow:1;
    overflow-y:auto;
    list-style:none;
    padding:0; margin:0;
  }
  #cartItems li {
    margin-bottom:1rem;
    padding-bottom:.8rem;
    border-bottom:1px solid var(--color-accent);
  }
  #cartItems li strong {
    color:var(--color-primary);
    font-size:1.1rem;
  }
  #cartItems li button.remove {
    background:transparent;
    border:none;
    color:var(--color-accent);
    font-size:1.4rem;
    cursor:pointer;
    float:right;
  }
  #cartItems li .controls {
    display:flex; justify-content:space-between; align-items:center; margin-top:.3rem;
  }
  #cartItems li input[type=number] {
    width:50px;
    border:none;
    border-radius:8px;
    background:#220044;
    color:var(--color-light);
    padding:.2rem;
    text-align:center;
  }
  #cartItems li .price {
    color:var(--color-accent);
    font-weight:700;
  }
  #cartPanel footer {
    margin-top:1rem;
    border-top:1px solid var(--color-accent);
    padding-top:1rem;
    display:flex;
    justify-content:space-between;
    font-size:1.3rem;
    font-weight:700;
    color:var(--color-primary);
  }
  #bgCanvas {
    position:fixed; top:0; left:0;
    width:100vw; height:100vh;
    z-index:0;
    pointer-events:none;
  }
  @media(max-width:700px){
    #cartPanel { width:100%; }
  }
</style>
</head>
<body>

<header>GALAXY ELITE FASHION</header>
  <nav class="nav-buttons">
    <button class="nav-btn">Início</button>
    <button class="nav-btn">Cadastrar</button>
    <button class="nav-btn">Sair</button>
  </nav>
  GALAXY ELITE FASHION
</header>

<style>
  /* Só adicionando estilo para os botões no header */
  .nav-buttons {
    position: absolute;
    top: 1rem;
    right: 2rem;
    display: flex;
    gap: 1rem;
    z-index: 20;
  }
  .nav-btn {
    background: linear-gradient(135deg, var(--color-primary), var(--color-accent));
    border: none;
    border-radius: 30px;
    padding: 0.5rem 1.2rem;
    font-family: 'Rajdhani', sans-serif;
    font-weight: 700;
    font-size: 1rem;
    color: var(--color-dark);
    cursor: pointer;
    box-shadow: 0 0 15px var(--color-primary), 0 0 30px var(--color-accent);
    transition: background 0.3s, transform 0.2s;
  }
  .nav-btn:hover {
    background: linear-gradient(135deg, var(--color-accent), var(--color-primary));
    transform: scale(1.1);
  }
</style>
<main>
  <section class="products" aria-live="polite" aria-label="Produtos disponíveis">
    <!-- Produto 1 -->
    <article class="product-card" data-id="1">
      <img src="https://images.unsplash.com/photo-1491553895911-0055eca6402d?auto=format&fit=crop&w=600&q=80" alt="Capa Neon Nebula"/>
      <div class="product-info">
        <div class="product-category">Neon Nebula</div>
        <h2 class="product-title">Jaqueta Neon Nova</h2>
        <p class="product-desc">Luz intensa e brilho cósmico.</p>
        <div class="product-price">₡12300</div>
        <button class="btn-buy">Comprar</button>
      </div>
    </article>
    <!-- Produto 2 -->
    <article class="product-card" data-id="2">
      <img src="https://images.unsplash.com/photo-1494790108377-be9c29b29330?auto=format&fit=crop&w=600&q=90" alt="Mulher sensual sob luz neon rosa e azul" />"
      <div class="product-info">
        <div class="product-category">Neon Nebula</div>
        <h2 class="product-title">Capa Neon Nebula</h2>
        <p class="product-desc">Brilha nas noites mais escuras.</p>
        <div class="product-price">₡14500</div>
        <button class="btn-buy">Comprar</button>
      </div>
    </article>
    <!-- Produto 3 -->
    <article class="product-card" data-id="3">
      <img src="https://images.unsplash.com/photo-1524504388940-b1c1722653e1?auto=format&fit=crop&w=600&q=90" alt="Mulher com biquíni neon rosa na praia à noite" />
      <div class="product-info">
        <div class="product-category">Quantum Eclipse</div>
        <h2 class="product-title">Casaco Quantum Eclipse</h2>
        <p class="product-desc">Tecido antimagnético avançado.</p>
        <div class="product-price">₡20000</div>
        <button class="btn-buy">Comprar</button>
      </div>
    </article>
    <!-- Produto 4 -->
    <article class="product-card" data-id="4">
      <img src="https://images.unsplash.com/photo-1544005313-94ddf0286df2?auto=format&fit=crop&w=600&q=80" alt="Modelo Isabella usando vestido vermelho" />
      <div class="product-info">
        <div class="product-category">Antimatéria</div>
        <h2 class="product-title">Veste Antimatéria</h2>
        <p class="product-desc">Repele matéria indesejada.</p>
        <div class="product-price">₡18750</div>
        <button class="btn-buy">Comprar</button>
      </div>
    </article>
    <!-- Produto 5 -->
    <article class="product-card" data-id="5">
      <img src="https://images.pexels.com/photos/1231234/pexels-photo-1231234.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260" alt="Mulher em ambiente urbano com óculos">
      <div class="product-info">
        <div class="product-category">Nova Starline</div>
        <h2 class="product-title">Vestido Nova Starline</h2>
        <p class="product-desc">Elegância que pulsa como estrela.</p>
        <div class="product-price">₡22800</div>
        <button class="btn-buy">Comprar</button>
      </div>
    </article>

	<!-- Produto 5 -->
    <article class="product-card" data-id="5">
      <img src="https://images.unsplash.com/photo-1550547660-d9450f859349?auto=format&fit=crop&w=600&q=80" alt="Hambúrguer clássico" />
      <div class="product-info">
        <div class="product-category">Nova Starline</div>
        <h2 class="product-title">Vestido Nova Starline</h2>
        <p class="product-desc">Elegância que pulsa como estrela.</p>
        <div class="product-price">₡22800</div>
        <button class="btn-buy">Comprar</button>
      </div>
    </article>

	 <!-- Produto 2 -->
    <article class="product-card" data-id="2">
      <img src="https://images.unsplash.com/photo-1491553895911-0055eca6402d?auto=format&fit=crop&w=600&q=80" alt="Capa Neon Nebula"/>
      <div class="product-info">
        <div class="product-category">Neon Nebula</div>
        <h2 class="product-title">Capa Neon Nebula</h2>
        <p class="product-desc">Brilha nas noites mais escuras.</p>
        <div class="product-price">₡14500</div>
        <button class="btn-buy">Comprar</button>
      </div>
    </article>

	 <!-- Produto 2 -->
    <article class="product-card" data-id="2">
      <img src="https://upload.wikimedia.org/wikipedia/commons/8/8c/Cristiano_Ronaldo_2018.jpg" alt="Capa Neon Nebula"/>
      <div class="product-info">
        <div class="product-category">Neon Nebula</div>
        <h2 class="product-title">Capa Neon Nebula</h2>
        <p class="product-desc">Brilha nas noites mais escuras.</p>
        <div class="product-price">₡14500</div>
        <button class="btn-buy">Comprar</button>
      </div>
    </article>

	 <!-- Produto 2 -->
    <article class="product-card" data-id="2">
      <img src="https://images.unsplash.com/photo-1508214751196-bcfd4ca60f91" alt="Mulher bonita" width="300" />
      <div class="product-info">
        <div class="product-category">Neon Nebula</div>
        <h2 class="product-title">Capa Neon Nebula</h2>
        <p class="product-desc">Brilha nas noites mais escuras.</p>
        <div class="product-price">₡14500</div>
        <button class="btn-buy">Comprar</button>
      </div>
    </article>
  </section>
</main>

<!-- Carrinho -->
<button id="cartToggle">🛒</button>
<aside id="cartPanel">
  <header>
    <span>Seu Carrinho</span>
    <button id="cartClose">&times;</button>
  </header>
  <ul id="cartItems"></ul>
  <footer><span>Total:</span><span id="cartTotal">₡0</span></footer>
</aside>

<canvas id="bgCanvas"></canvas>

<script>
  // Carrinho em JS puro
  const cart = [];
  const cartToggle = document.getElementById('cartToggle');
  const cartPanel = document.getElementById('cartPanel');
  const cartClose = document.getElementById('cartClose');
  const cartItems = document.getElementById('cartItems');
  const cartTotal = document.getElementById('cartTotal');

  function updateCart(){
    cartItems.innerHTML = '';
    let total = 0;
    cart.forEach((item, i) => {
      total += item.price * item.qty;
      const li = document.createElement('li');
      li.innerHTML = `
        <strong>${item.title}</strong>
        <button class="remove" data-index="${i}">&times;</button>
        <div class="controls">
          <label>Qtd:</label>
          <input type="number" min="1" max="99" value="${item.qty}" data-index="${i}">
          <div class="price">₡${(item.price * item.qty).toLocaleString('pt-BR')}</div>
        </div>`;
      cartItems.appendChild(li);
    });
    cartTotal.textContent = `₡${total.toLocaleString('pt-BR')}`;
  }

  document.querySelectorAll('.btn-buy').forEach((btn, idx) => {
    btn.addEventListener('click', () => {
      const card = btn.closest('.product-card');
      const title = card.querySelector('.product-title').textContent;
      const price = parseInt(card.querySelector('.product-price').textContent.replace(/[^\d]/g,''));
      const existing = cart.find(i => i.title === title);
      if(existing) existing.qty++;
      else cart.push({ title, price, qty:1 });
      updateCart();
      cartPanel.style.right = '0';
    });
  });

  cartToggle.addEventListener('click', () => { cartPanel.style.right = '0'; });
  cartClose.addEventListener('click', () => { cartPanel.style.right = '-400px'; });

  cartItems.addEventListener('click', e => {
    if(e.target.classList.contains('remove')){
      const i = e.target.dataset.index;
      cart.splice(i,1);
      updateCart();
    }
  });

  cartItems.addEventListener('input', e => {
    if(e.target.type === 'number'){
      const i = e.target.dataset.index;
      let val = parseInt(e.target.value);
      if(isNaN(val) || val<1) val=1;
      if(val>99) val=99;
      cart[i].qty = val;
      e.target.value = val;
      updateCart();
    }
  });

  // Mantém fundo animado sem alteração
  const canvas = document.getElementById('bgCanvas'),
        ctx = canvas.getContext('2d');
  let w, h;
  function resize(){ w=canvas.width=window.innerWidth; h=canvas.height=window.innerHeight; }
  window.addEventListener('resize', resize);
  resize();

  const stars=[], shootingStars=[], lasers=[], fireworks=[];
  const laserColors = ['#7ef9ff','#ff6ff8','#ff3dff','#00fff7','#e600ff'];
  let auroraOffset=0;

  function cSS(c){return c;}
  function createShootingStar(){ shootingStars.push({ x:Math.random()*w, y:Math.random()*h*0.5, length:150+Math.random()*100, speed:12+Math.random()*12, angle:Math.PI/4, opacity:1, life:0, maxLife:20+Math.random()*25 });}
  function createLaser(){ lasers.push({ x:Math.random()*w, y:Math.random()*h, length:100+Math.random()*200, width:1+Math.random()*2, speed:15+Math.random()*20, opacity:0.7+Math.random()*0.3, color:laserColors[Math.floor(Math.random()*laserColors.length)], life:0, maxLife:40+Math.random()*50, angle:Math.random()*Math.PI*2 });}
  function createFirework(){
    const x=Math.random()*w, y=Math.random()*h*0.5+h*0.1;
    fireworks.push({ x, y, particles:[], exploded:false, life:0, maxLife:60+Math.random()*40 });
  }
  function createParticles(fw){
    for(let i=0;i<20+Math.random()*30;i++){
      fw.particles.push({ x:fw.x, y:fw.y, angle:Math.random()*Math.PI*2, speed:2+Math.random()*4, radius:1+Math.random()*2, color: laserColors[Math.floor(Math.random()*laserColors.length)], life:0, maxLife:20+Math.random()*30, opacity:1 });
    }
  }

  for(let i=0;i<180;i++) stars.push({ x:Math.random()*w, y:Math.random()*h, radius:Math.random()*1.5+0.3, opacity:Math.random() });
  setInterval(() => { if(shootingStars.length<7) createShootingStar(); }, 1000);
  setInterval(() => { if(lasers.length<15) createLaser(); }, 400);
  setInterval(() => { if(fireworks.length<6) createFirework(); }, 2500);

  function draw(){
    ctx.clearRect(0,0,w,h);
    const grad=ctx.createLinearGradient(0,0,0,h);
    grad.addColorStop(0,'#0a001a');
    grad.addColorStop(0.5,'#1a0040');
    grad.addColorStop(1,'#300055');
    ctx.fillStyle=grad;
    ctx.fillRect(0,0,w,h);

    auroraOffset += 0.02;
    for(let i=0;i<5;i++){
      ctx.beginPath();
      for(let x=0;x<=w;x+=10){
        const y = h*0.3 + Math.sin(x*(0.02+0.008*i)+auroraOffset+i)* (60+15*i);
        ctx.lineTo(x,y);
      }
      ctx.lineTo(w,h);
      ctx.lineTo(0,h);
      ctx.closePath();
      ctx.fillStyle = ['rgba(126,249,255,0.4)','rgba(255,111,248,0.3)','rgba(255,61,255,0.25)','rgba(0,255,247,0.2)','rgba(230,0,255,0.15)'][i];
      ctx.fill();
    }

    stars.forEach(st => {
      ctx.beginPath();
      ctx.arc(st.x,st.y,st.radius,0,2*Math.PI);
      ctx.fillStyle = `rgba(255,255,255,${st.opacity})`;
      ctx.shadowColor='white';
      ctx.shadowBlur=8;
      ctx.fill();
    });

    shootingStars.forEach((s,i)=>{
      ctx.save();
      ctx.translate(s.x,s.y);
      ctx.rotate(-s.angle);
      const g=ctx.createLinearGradient(0,0,s.length,0);
      g.addColorStop(0,`rgba(255,255,255,${s.opacity})`);
      g.addColorStop(1,'rgba(255,255,255,0)');
      ctx.fillStyle=g;
      ctx.fillRect(0,-1.5,s.length,3);
      ctx.restore();
      s.x += Math.cos(s.angle)*s.speed;
      s.y += Math.sin(s.angle)*s.speed;
      s.life++;
      s.opacity -=0.02;
      if(s.life> s.maxLife) shootingStars.splice(i,1);
    });

    lasers.forEach((l,i)=>{
      ctx.save();
      ctx.translate(l.x,l.y);
      ctx.rotate(l.angle);
      const g=ctx.createLinearGradient(0,0,l.length,0);
      g.addColorStop(0, l.color);
      g.addColorStop(1,'rgba(0,0,0,0)');
      ctx.fillStyle=g;
      ctx.fillRect(0,0,l.length,l.width);
      ctx.restore();
      l.life++;
      if(l.life>l.maxLife) lasers.splice(i,1);
    });

    fireworks.forEach((fw,i)=>{
      if(!fw.exploded){
        fw.y -=4;
        fw.life++;
        if(fw.life>fw.maxLife/2){
          fw.exploded = true;
          createParticles(fw);
        }
      } else {
        fw.particles.forEach((p,j) => {
          p.x+=Math.cos(p.angle)*p.speed;
          p.y+=Math.sin(p.angle)*p.speed;
          p.life++;
          p.opacity=1-p.life/p.maxLife;
        });
        fw.particles = fw.particles.filter(p=>p.life<p.maxLife);
        if(fw.particles.length===0) fireworks.splice(i,1);
      }
    });
    requestAnimationFrame(draw);
  }
  draw();
  
</script>

</body>
</html>
