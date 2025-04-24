<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>سابوريتا | Saborita</title>
  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Open+Sans&display=swap" rel="stylesheet">
  <style>
    /* Reset & Base */
    * { margin:0; padding:0; box-sizing: border-box; }
    body { font-family: 'Open Sans', sans-serif; background: #f9f9f9; color: #333; line-height:1.6; }
    img { max-width:100%; display:block; }
    a { text-decoration:none; color:inherit; }

    /* Container */
    .container { width:90%; max-width:1200px; margin:auto; padding:2rem 0; }

    /* Header */
    header { background:#222831; color:#eeeeee; padding:1rem 0; position: relative; }
    .logo { font-family:'Playfair Display'; font-size:2rem; text-align:center; }
    .lang-switch { position:absolute; top:1rem; left:1rem; background:#393e46; border:none; padding:0.5rem 1rem; cursor:pointer; border-radius:4px; color:#eeeeee; }

    /* Sections */
    section { margin:3rem 0; }
    h2 { font-family:'Playfair Display'; margin-bottom:1rem; font-size:2rem; border-bottom:2px solid #00adb5; display:inline-block; padding-bottom:0.3rem; }

    /* Grid for menu */
    .grid { display:grid; grid-template-columns: repeat(auto-fit, minmax(280px,1fr)); gap:1.5rem; }
    .card { background:#fff; border-radius:8px; overflow:hidden; box-shadow:0 4px 8px rgba(0,0,0,0.1); transition: transform .2s; }
    .card:hover { transform: translateY(-5px); }
    .card img { height:250px; object-fit: cover; }
    .card-body { padding:1rem; }
    .card-title { font-size:1.2rem; margin-bottom:0.5rem; }
    .card-price { font-weight:bold; font-size:1rem; color:#00adb5; }

    /* Footer */
    footer { text-align:center; padding:1rem 0; background:#222831; color:#eeeeee; margin-top:3rem; font-size:0.9rem; }

    /* Responsive RTL/LTR */
    [dir="ltr"] { direction:ltr; }
  </style>
</head>
<body>
  <button class="lang-switch" onclick="toggleLang()">English</button>
  <header>
    <div class="container">
      <div class="logo" data-key="siteName">سابوريتا</div>
    </div>
  </header>

  <main class="container">
    <!-- Dishes Section -->
    <section>
      <h2 data-key="dishesTitle">قائمة الأكلات الإيطالية</h2>
      <div class="grid" id="dishes">
        <!-- Cards injected by JavaScript -->
      </div>
    </section>

    <!-- Drinks Section -->
    <section>
      <h2 data-key="drinksTitle">المشروبات</h2>
      <div class="grid" id="drinks">
        <!-- Cards injected by JavaScript -->
      </div>
    </section>
  </main>

  <footer>
    <div data-key="footerText">© 2025 سابوريتا. جميع الحقوق محفوظة.</div>
  </footer>

  <script>
    // Data for items
    const data = {
      dishes: [
        { key: 'pizzaMargherita', ar: 'بيتزا مارغريتا', en: 'Pizza Margherita', price: '400' },
        { key: 'pizzaPepperoni', ar: 'بيتزا ببروني', en: 'Pizza Pepperoni', price: '500' },
        { key: 'pastaCarbonara', ar: 'باستا كاربونارا', en: 'Pasta Carbonara', price: '450' },
        { key: 'lasagna', ar: 'لازانيا', en: 'Lasagna', price: '550' },
        { key: 'risotto', ar: 'ريزوتو', en: 'Risotto', price: '600' },
        { key: 'gnocchi', ar: 'جنوتشي', en: 'Gnocchi', price: '500' },
        { key: 'fettuccine', ar: 'فيتوتشيني', en: 'Fettuccine Alfredo', price: '650' },
        { key: 'bruschetta', ar: 'بروشيتا', en: 'Bruschetta', price: '400' },
        { key: 'calzone', ar: 'كالزوني', en: 'Calzone', price: '550' },
        { key: 'ravioli', ar: 'رافيولي', en: 'Ravioli', price: '700' }
      ],
      drinks: [
        { key: 'espresso', ar: 'إسبريسو', en: 'Espresso', price: '30' },
        { key: 'latte', ar: 'لاتيه', en: 'Latte', price: '40' },
        { key: 'cappuccino', ar: 'كابتشينو', en: 'Cappuccino', price: '50' },
        { key: 'americano', ar: 'أميريكانو', en: 'Americano', price: '35' },
        { key: 'mocha', ar: 'موكا', en: 'Mocha', price: '60' },
        { key: 'tea', ar: 'شاي', en: 'Tea', price: '30' },
        { key: 'cola', ar: 'كولا', en: 'Cola', price: '20' },
        { key: 'lemonade', ar: 'ليمونادة', en: 'Lemonade', price: '25' },
        { key: 'smoothie', ar: 'سموذي', en: 'Smoothie', price: '80' },
        { key: 'juice', ar: 'عصير طبيعي', en: 'Fresh Juice', price: '100' }
      ],
      texts: {
        siteName: { ar: 'سابوريتا', en: 'Saborita' },
        dishesTitle: { ar: 'قائمة الأكلات الإيطالية', en: 'Italian Dishes' },
        drinksTitle: { ar: 'المشروبات', en: 'Drinks' },
        footerText: { ar: '© 2025 سابوريتا. جميع الحقوق محفوظة.', en: '© 2025 Saborita. All rights reserved.' }
      }
    };

    // Render cards with clearer images
    function renderItems(sectionId, items) {
      const container = document.getElementById(sectionId);
      container.innerHTML = '';
      items.forEach(item => {
        const card = document.createElement('div');
        card.className = 'card';
        card.innerHTML = `
          <img src="https://source.unsplash.com/600x400/?${encodeURIComponent(item.en)}" alt="${item.ar}">
          <div class="card-body">
            <div class="card-title" data-key="${item.key}">${item.ar}</div>
            <div class="card-price">${item.price} ج.م</div>
          </div>
        `;
        container.appendChild(card);
      });
    }

    // Language toggle logic
    let currentLang = 'ar';
    function updateLanguage() {
      document.documentElement.lang = currentLang;
      document.documentElement.dir = currentLang === 'ar' ? 'rtl' : 'ltr';
      document.querySelector('.lang-switch').textContent = currentLang === 'ar' ? 'English' : 'العربية';
      // Translate static texts
      Object.keys(data.texts).forEach(key => {
        document.querySelector(`[data-key="${key}"]`).textContent = data.texts[key][currentLang];
      });
      // Translate dynamic items
      data.dishes.concat(data.drinks).forEach(item => {
        const el = document.querySelector(`[data-key="${item.key}"]`);
        if (el) el.textContent = item[currentLang];
      });
    }

    function toggleLang() {
      currentLang = currentLang === 'ar' ? 'en' : 'ar';
      updateLanguage();
      renderItems('dishes', data.dishes);
      renderItems('drinks', data.drinks);
    }

    // Initialize
    document.addEventListener('DOMContentLoaded', () => {
      renderItems('dishes', data.dishes);
      renderItems('drinks', data.drinks);
      updateLanguage();
    });
  </script>
</body>
</html>
