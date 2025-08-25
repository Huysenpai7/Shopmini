
<html lang="vi">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Shop Mini – Demo</title>
<style>
  /* Reset + base */
  *{box-sizing:border-box} html,body{margin:0;padding:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial,sans-serif}
  :root{
    --bg:#0f0f12; --card:#16181d; --muted:#a0a4ab; --text:#e9ecf1; --brand:#5b8cff; --brand-2:#7dffb3;
    --accent:#22252b; --line:#2a2f37; --danger:#ff6b6b;
  }
  body{background:linear-gradient(180deg,#0f1014, #0d0e12 200px) fixed;color:var(--text)}
  a{color:inherit}
  /* Header */
  header{
    position:sticky;top:0;z-index:20;
    backdrop-filter: blur(8px);
    background:rgba(13, 15, 20, .7);
    border-bottom:1px solid var(--line);
  }
  .wrap{max-width:1100px;margin:0 auto;padding:14px 16px}
  .row{display:flex;align-items:center;gap:12px}
  .row.space{justify-content:space-between}
  .logo{font-weight:700;letter-spacing:.3px}
  .logo b{background:linear-gradient(90deg,var(--brand),var(--brand-2));-webkit-background-clip:text;background-clip:text;color:transparent}
  .search{flex:1;display:flex;gap:8px}
  .search input{
    flex:1;border:1px solid var(--line);background:var(--card);color:var(--text);
    padding:10px 12px;border-radius:12px;outline:none
  }
  .search button,.btn{
    border:1px solid var(--line);background:var(--accent);color:var(--text);
    padding:10px 14px;border-radius:12px;cursor:pointer
  }
  .icon-btn{display:inline-flex;align-items:center;gap:8px}
  .pill{background:var(--brand);color:#081028;border:none}
  /* Hero */
  .hero{display:flex;gap:16px;flex-wrap:wrap;align-items:center;margin:16px 0}
  .hero .card{
    flex:1 1 260px;min-height:120px;background:radial-gradient(80% 120% at 100% 0%,rgba(93,140,255,.25),transparent),var(--card);
    border:1px solid var(--line);border-radius:16px;padding:16px
  }
  .hero h1{font-size:20px;margin:0 0 6px}
  .hero p{margin:0;color:var(--muted)}
  /* Products grid */
  .grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:14px}
  @media(min-width:720px){.grid{grid-template-columns:repeat(3,minmax(0,1fr))}}
  @media(min-width:980px){.grid{grid-template-columns:repeat(4,minmax(0,1fr))}}
  .product{
    background:var(--card);border:1px solid var(--line);border-radius:16px;overflow:hidden;display:flex;flex-direction:column
  }
  .thumb{
    aspect-ratio: 4/3; background:#0b0c10; display:grid; place-items:center; border-bottom:1px solid var(--line)
  }
  .thumb img{width:100%;height:100%;object-fit:cover;display:block}
  .p-body{padding:12px;display:flex;gap:10px;flex-direction:column}
  .title{margin:0;font-size:15px;line-height:1.2}
  .price{font-weight:700}
  .muted{color:var(--muted);font-size:13px}
  .qty{display:flex;align-items:center;gap:8px}
  .qty button{width:28px;height:28px;border-radius:8px;border:1px solid var(--line);background:var(--accent);color:var(--text);cursor:pointer}
  .full{width:100%}
  /* Cart drawer */
  .drawer{
    position:fixed;inset:0 0 0 auto;width:min(420px,100%);background:#0d0f14;border-left:1px solid var(--line);
    transform:translateX(100%);transition:transform .25s ease;z-index:50;display:flex;flex-direction:column
  }
  .drawer.open{transform:translateX(0)}
  .drawer header{position:sticky;top:0;background:#0d0f14;border-bottom:1px solid var(--line)}
  .drawer .items{padding:12px;display:flex;flex-direction:column;gap:12px;overflow:auto;flex:1}
  .cart-item{display:grid;grid-template-columns:64px 1fr auto;gap:10px;align-items:center;background:var(--card);border:1px solid var(--line);border-radius:12px;padding:8px}
  .cart-item img{width:64px;height:64px;object-fit:cover;border-radius:8px}
  .cart-item .name{font-size:14px;margin:0}
  .cart-item .sub{color:var(--muted);font-size:12px}
  .cart-footer{border-top:1px solid var(--line);padding:12px;display:flex;gap:10px;flex-direction:column}
  .row-between{display:flex;justify-content:space-between;align-items:center}
  .small{font-size:13px;color:var(--muted)}
  .danger{background:var(--danger);border-color:#b24444}
  /* Toast */
  .toast{position:fixed;left:50%;bottom:16px;transform:translateX(-50%);background:var(--card);border:1px solid var(--line);padding:10px 14px;border-radius:12px;opacity:0;transition:opacity .25s, transform .25s;z-index:60}
  .toast.show{opacity:1;transform:translateX(-50%) translateY(-4px)}
  /* Footer */
  footer{border-top:1px solid var(--line);margin-top:20px}
  footer .wrap{padding:20px 16px;color:var(--muted);font-size:13px}
</style>
</head>
<body>
  <header>
    <div class="wrap row space">
      <div class="row" style="gap:14px">
        <div class="logo">Shop <b>Mini</b></div>
        <div class="search">
          <input id="q" placeholder="Tìm sản phẩm... (ví dụ: áo, giày)" />
          <button id="clear">Xoá</button>
        </div>
      </div>
      <button id="openCart" class="btn icon-btn pill">🛒 <span id="cartCount">0</span></button>
    </div>
  </header>

  <main class="wrap">
    <section class="hero">
      <div class="card">
        <h1>Xin chào 👋</h1>
        <p>Đây là web bán hàng mini, tối ưu cho điện thoại. Bạn có thể tìm sản phẩm, thêm vào giỏ, tăng/giảm số lượng và xem tổng tiền (VND).</p>
      </div>
      <div class="card">
        <p class="muted" style="margin:0 0 8px">Mẹo bào code</p>
        <ul style="margin:0 0 0 18px;padding:0">
          <li>Lưu file này và chỉnh sửa danh sách sản phẩm trong phần <b>JS</b>.</li>
          <li>Dùng điện thoại: Acode / Textastic để sửa nhanh.</li>
          <li>Triển khai miễn phí: GitHub Pages / Netlify / Vercel.</li>
        </ul>
      </div>
    </section>

    <section>
      <h2 style="font-size:16px;margin:10px 0">Sản phẩm</h2>
      <div id="grid" class="grid"></div>
    </section>
  </main>

  <!-- Cart Drawer -->
  <aside id="drawer" class="drawer" aria-hidden="true">
    <header>
      <div class="wrap row space">
        <strong>Giỏ hàng</strong>
        <div class="row">
          <button id="clearCart" class="btn danger">Xoá giỏ</button>
          <button id="closeCart" class="btn">Đóng</button>
        </div>
      </div>
    </header>
    <div class="items" id="cartItems"></div>
    <div class="cart-footer">
      <div class="row-between small"><span>Tạm tính</span><strong id="subTotal">0₫</strong></div>
      <div class="row-between small"><span>Phí ship (ước tính)</span><span id="shipFee">25.000₫</span></div>
      <div class="row-between"><span><strong>Tổng</strong></span><strong id="grandTotal">0₫</strong></div>
      <button class="btn pill" id="checkout">Thanh toán (demo)</button>
      <span class="small">* Đây chỉ là bản demo. Không có thanh toán thật.</span>
    </div>
  </aside>

  <div id="toast" class="toast">Đã thêm vào giỏ</div>

<script>
  // ====== DATA ======
  const PRODUCTS = [
    {id:'p1', name:'Áo thun Basic', price: 99000, img:'https://picsum.photos/seed/shirt/600/450', desc:'Vải cotton 100%'},
    {id:'p2', name:'Quần jogger', price: 199000, img:'https://picsum.photos/seed/jogger/600/450', desc:'Thoải mái, co giãn'},
    {id:'p3', name:'Giày sneaker', price: 349000, img:'https://picsum.photos/seed/sneaker/600/450', desc:'Phong cách đường phố'},
    {id:'p4', name:'Balo canvas', price: 159000, img:'https://picsum.photos/seed/bag/600/450', desc:'Đi học, đi chơi'},
    {id:'p5', name:'Mũ lưỡi trai', price: 69000, img:'https://picsum.photos/seed/cap/600/450', desc:'Chống nắng nhẹ'},
    {id:'p6', name:'Áo khoác gió', price: 259000, img:'https://picsum.photos/seed/wind/600/450', desc:'Chống gió, nhẹ'},
    {id:'p7', name:'Tất cổ thấp', price: 19000, img:'https://picsum.photos/seed/sock/600/450', desc:'Thoáng mát'},
    {id:'p8', name:'Áo sơ mi Slim', price: 219000, img:'https://picsum.photos/seed/shirt2/600/450', desc:'Đi học/đi làm'},
  ];

  // ====== HELPERS ======
  const fmt = n => (n||0).toLocaleString('vi-VN') + '₫';
  const el = (sel,scope=document)=>scope.querySelector(sel);
  const els = (sel,scope=document)=>[...scope.querySelectorAll(sel)];
  const save = (k,v)=>localStorage.setItem(k,JSON.stringify(v));
  const load = (k,def)=>{try{return JSON.parse(localStorage.getItem(k)) ?? def}catch{ return def }};

  // ====== STATE ======
  let CART = load('mini_cart', {});

  // ====== UI RENDER ======
  function renderProducts(list){
    const grid = el('#grid');
    grid.innerHTML = '';
    list.forEach(p=>{
      const div = document.createElement('article');
      div.className = 'product';
      div.innerHTML = `
        <div class="thumb"><img src="${p.img}" alt="${p.name}"></div>
        <div class="p-body">
          <h3 class="title">${p.name}</h3>
          <div class="muted">${p.desc || ''}</div>
          <div class="row space">
            <div class="price">${fmt(p.price)}</div>
            <button class="btn pill" data-add="${p.id}">Thêm</button>
          </div>
        </div>`;
      grid.appendChild(div);
    });
  }

  function renderCart(){
    const items = el('#cartItems');
    items.innerHTML = '';
    const entries = Object.entries(CART);
    if(entries.length===0){
      items.innerHTML = '<p class="small" style="text-align:center;color:var(--muted)">Giỏ hàng trống.</p>';
    }else{
      entries.forEach(([id,qty])=>{
        const p = PRODUCTS.find(x=>x.id===id);
        if(!p) return;
        const row = document.createElement('div');
        row.className = 'cart-item';
        row.innerHTML = `
          <img src="${p.img}" alt="${p.name}">
          <div>
            <p class="name">${p.name}</p>
            <div class="sub">${fmt(p.price)} • <span class="small">x${qty}</span></div>
            <div class="qty" style="margin-top:6px">
              <button data-dec="${id}">−</button>
              <button data-inc="${id}">+</button>
              <button data-del="${id}" style="margin-left:auto">🗑️</button>
            </div>
          </div>
          <strong>${fmt(p.price*qty)}</strong>`;
        items.appendChild(row);
      });
    }
    const sub = entries.reduce((s,[id,qty])=>{
      const p = PRODUCTS.find(x=>x.id===id);
      return s + (p?p.price*qty:0);
    },0);
    el('#subTotal').textContent = fmt(sub);
    const ship = entries.length?25000:0;
    el('#shipFee').textContent = fmt(ship);
    el('#grandTotal').textContent = fmt(sub+ship);
    el('#cartCount').textContent = entries.reduce((s,[,q])=>s+q,0);
  }

  function toast(msg='Đã thêm vào giỏ'){
    const t = el('#toast');
    t.textContent = msg;
    t.classList.add('show');
    setTimeout(()=>t.classList.remove('show'), 1400);
  }

  // ====== EVENTS ======
  document.addEventListener('click', (e)=>{
    const add = e.target.closest('[data-add]');
    if(add){
      const id = add.getAttribute('data-add');
      CART[id] = (CART[id]||0) + 1;
      save('mini_cart', CART);
      renderCart();
      toast();
    }
    const inc = e.target.closest('[data-inc]');
    if(inc){
      const id = inc.getAttribute('data-inc');
      CART[id] = (CART[id]||0) + 1;
      save('mini_cart', CART);
      renderCart();
    }
    const dec = e.target.closest('[data-dec]');
    if(dec){
      const id = dec.getAttribute('data-dec');
      CART[id] = Math.max(0,(CART[id]||0)-1);
      if(CART[id]===0) delete CART[id];
      save('mini_cart', CART);
      renderCart();
    }
    const del = e.target.closest('[data-del]');
    if(del){
      const id = del.getAttribute('data-del');
      delete CART[id];
      save('mini_cart', CART);
      renderCart();
    }
    if(e.target.id==='openCart'){ el('#drawer').classList.add('open'); el('#drawer').setAttribute('aria-hidden','false')}
    if(e.target.id==='closeCart'){ el('#drawer').classList.remove('open'); el('#drawer').setAttribute('aria-hidden','true')}
    if(e.target.id==='clearCart'){ CART={}; save('mini_cart', CART); renderCart(); }
    if(e.target.id==='checkout'){
      alert('Đây là bản demo. Bạn có thể thay alert này bằng quy trình thanh toán thật (VNPAY, Momo, v.v.).');
    }
    if(e.target.id==='clear'){
      el('#q').value=''; renderProducts(PRODUCTS);
    }
  });

  // Search
  el('#q').addEventListener('input', (e)=>{
    const key = e.target.value.toLowerCase().trim();
    const list = PRODUCTS.filter(p=>
      p.name.toLowerCase().includes(key) || (p.desc||'').toLowerCase().includes(key)
    );
    renderProducts(list);
  });

  // ====== INIT ======
  renderProducts(PRODUCTS);
  renderCart();
</script>
</body>
<footer>
  <div class="wrap">© 2025 Shop Mini – Bản demo by duc huy </div>
</footer>
</html>
