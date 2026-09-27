<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>هاتلي</title>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: Arial, sans-serif;
    }

    body {
      background: #f5f6f8;
      color: #222;
      min-height: 100vh;
    }

    header {
      background: #111827;
      color: white;
      padding: 22px 18px;
      border-radius: 0 0 25px 25px;
    }

    header h1 {
      font-size: 30px;
      margin-bottom: 6px;
    }

    header p {
      color: #d1d5db;
      font-size: 15px;
    }

    .container {
      max-width: 600px;
      margin: auto;
      padding: 18px;
    }

    .welcome {
      margin: 15px 0;
    }

    .welcome h2 {
      font-size: 22px;
      margin-bottom: 5px;
    }

    .welcome p {
      color: #666;
    }

    .cards {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
      margin-top: 18px;
    }

    .card {
      background: white;
      border: none;
      border-radius: 18px;
      padding: 20px 12px;
      text-align: center;
      box-shadow: 0 4px 15px rgba(0,0,0,.06);
      cursor: pointer;
      transition: .2s;
    }

    .card:active {
      transform: scale(.97);
    }

    .icon {
      font-size: 38px;
      margin-bottom: 10px;
    }

    .card h3 {
      font-size: 16px;
    }

    .card p {
      font-size: 12px;
      color: #777;
      margin-top: 5px;
    }

    .section {
      background: white;
      border-radius: 20px;
      padding: 20px;
      margin-top: 18px;
      box-shadow: 0 4px 15px rgba(0,0,0,.05);
    }

    .section h2 {
      margin-bottom: 15px;
      font-size: 20px;
    }

    label {
      display: block;
      margin: 12px 0 6px;
      font-size: 14px;
      font-weight: bold;
    }

    input, textarea, select {
      width: 100%;
      padding: 13px;
      border: 1px solid #ddd;
      border-radius: 12px;
      font-size: 15px;
      outline: none;
      background: #fafafa;
    }

    textarea {
      min-height: 90px;
      resize: vertical;
    }

    .btn {
      width: 100%;
      border: none;
      border-radius: 14px;
      padding: 15px;
      margin-top: 16px;
      background: #16a34a;
      color: white;
      font-size: 17px;
      font-weight: bold;
      cursor: pointer;
    }

    .btn.secondary {
      background: #111827;
    }

    .price {
      background: #ecfdf5;
      border-radius: 15px;
      padding: 16px;
      margin-top: 15px;
      text-align: center;
    }

    .price strong {
      display: block;
      font-size: 28px;
      color: #15803d;
      margin-top: 5px;
    }

    .status {
      margin-top: 15px;
    }

    .status-item {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 12px 0;
      border-bottom: 1px solid #eee;
    }

    .status-item:last-child {
      border-bottom: none;
    }

    .dot {
      width: 14px;
      height: 14px;
      border-radius: 50%;
      background: #d1d5db;
    }

    .dot.active {
      background: #16a34a;
    }

    .hidden {
      display: none;
    }

    .bottom {
      text-align: center;
      color: #888;
      font-size: 12px;
      padding: 30px 0;
    }
  </style>
</head>

<body>

<header>
  <div class="container">
    <h1>هاتلي</h1>
    <p>اطلبها… هاتهالك</p>
  </div>
</header>

<main class="container">

  <!-- الصفحة الرئيسية -->
  <section id="home">

    <div class="welcome">
      <h2>أهلاً بيك 👋</h2>
      <p>محتاج حد يجيبلك حاجة؟ إحنا هنا.</p>
    </div>

    <div class="cards">

      <button class="card" onclick="openOrder()">
        <div class="icon">📦</div>
        <h3>هاتلي حاجة</h3>
        <p>اطلب أي حاجة من مكان معين</p>
      </button>

      <button class="card" onclick="openOrder()">
        <div class="icon">📍</div>
        <h3>ابعت حاجة</h3>
        <p>ابعت طرد لشخص آخر</p>
      </button>

      <button class="card" onclick="openOrder()">
        <div class="icon">📄</div>
        <h3>استلملي حاجة</h3>
        <p>خلي مندوب يستلمها لك</p>
      </button>

      <button class="card" onclick="openOrder()">
        <div class="icon">✏️</div>
        <h3>طلب خاص</h3>
        <p>اكتب لنا اللي محتاجه</p>
      </button>

    </div>

    <div class="section">
      <h2>📦 طلباتي</h2>
      <p id="noOrders">لا يوجد لديك طلبات حالياً.</p>

      <div id="orderInfo" class="hidden">
        <p><strong>رقم الطلب:</strong> <span id="orderNumber"></span></p>
        <p style="margin-top:8px">
          <strong>الحالة:</strong>
          <span id="orderStatus">جاري البحث عن مندوب</span>
        </p>

        <button class="btn secondary" onclick="showTracking()">
          متابعة الطلب
        </button>
      </div>
    </div>

  </section>


  <!-- إنشاء الطلب -->
  <section id="orderPage" class="hidden">

    <div class="section">

      <h2>📦 تفاصيل الطلب</h2>

      <label>مكان الاستلام</label>
      <input id="pickup" type="text" placeholder="مثال: محل أو عنوان الاستلام">

      <label>مكان التسليم</label>
      <input id="delivery" type="text" placeholder="عنوان الشخص المستلم">

      <label>وصف الحاجة</label>
      <textarea id="description"
        placeholder="اكتب بالتفصيل إيه اللي عايز المندوب يجيبه"></textarea>

      <label>رقم هاتف المستلم</label>
      <input id="phone" type="tel" placeholder="01xxxxxxxxx">

      <label>طريقة التوصيل</label>
      <select id="vehicle">
        <option value="walk">🚶 مشي</option>
        <option value="bike">🚲 عجلة</option>
        <option value="motorcycle">🛵 موتوسيكل</option>
        <option value="car">🚗 سيارة</option>
      </select>

      <label>طريقة الدفع</label>
      <select id="payment">
        <option>💵 كاش</option>
        <option>💳 بطاقة</option>
        <option>📱 محفظة إلكترونية</option>
      </select>

      <div class="price">
        السعر التجريبي
        <strong id="price">25 جنيه</strong>
      </div>

      <button class="btn" onclick="createOrder()">
        تأكيد الطلب
      </button>

      <button class="btn secondary" onclick="goHome()">
        رجوع
      </button>

    </div>

  </section>


  <!-- التتبع -->
  <section id="trackingPage" class="hidden">

    <div class="section">

      <h2>📍 متابعة الطلب</h2>

      <p>
        رقم الطلب:
        <strong id="trackingNumber"></strong>
      </p>

      <div class="status">

        <div class="status-item">
          <span class="dot active"></span>
          <span>تم إنشاء الطلب</span>
        </div>

        <div class="status-item">
          <span class="dot" id="dot2"></span>
          <span>جاري البحث عن مندوب</span>
        </div>

        <div class="status-item">
          <span class="dot" id="dot3"></span>
          <span>تم قبول الطلب</span>
        </div>

        <div class="status-item">
          <span class="dot" id="dot4"></span>
          <span>المندوب في الطريق</span>
        </div>

        <div class="status-item">
          <span class="dot" id="dot5"></span>
          <span>تم التسليم</span>
        </div>

      </div>

      <button class="btn secondary" onclick="goHome()">
        الرئيسية
      </button>

    </div>

  </section>

  <div class="bottom">
    هاتلي © 2026
  </div>

</main>


<script>

  let orderNumber = null;

  function openOrder() {
    document.getElementById("home").classList.add("hidden");
    document.getElementById("trackingPage").classList.add("hidden");
    document.getElementById("orderPage").classList.remove("hidden");
  }

  function goHome() {
    document.getElementById("orderPage").classList.add("hidden");
    document.getElementById("trackingPage").classList.add("hidden");
    document.getElementById("home").classList.remove("hidden");
  }

  function createOrder() {

    const pickup = document.getElementById("pickup").value;
    const delivery = document.getElementById("delivery").value;
    const description = document.getElementById("description").value;
    const phone = document.getElementById("phone").value;

    if (!pickup || !delivery || !description || !phone) {
      alert("من فضلك املأ كل البيانات المطلوبة.");
      return;
    }

    orderNumber =
      "HT" + Math.floor(100000 + Math.random() * 900000);

    document.getElementById("orderNumber").textContent = orderNumber;
    document.getElementById("trackingNumber").textContent = orderNumber;

    document.getElementById("noOrders").classList.add("hidden");
    document.getElementById("orderInfo").classList.remove("hidden");

    document.getElementById("orderPage").classList.add("hidden");
    document.getElementById("home").classList.remove("hidden");

    alert("تم إرسال طلبك بنجاح ✅");

    simulateOrder();
  }

  function showTracking() {

    document.getElementById("home").classList.add("hidden");
    document.getElementById("trackingPage").classList.remove("hidden");

  }

  function simulateOrder() {

    setTimeout(() => {
      document.getElementById("dot2").classList.add("active");
      document.getElementById("orderStatus").textContent =
        "جاري البحث عن مندوب";
    }, 1500);

    setTimeout(() => {
      document.getElementById("dot3").classList.add("active");
      document.getElementById("orderStatus").textContent =
        "تم قبول الطلب";
    }, 5000);

    setTimeout(() => {
      document.getElementById("dot4").classList.add("active");
      document.getElementById("orderStatus").textContent =
        "المندوب في الطريق";
    }, 9000);

    setTimeout(() => {
      document.getElementById("dot5").classList.add("active");
      document.getElementById("orderStatus").textContent =
        "تم التسليم ✅";
    }, 14000);
  }

</script>

</body>
</html>
