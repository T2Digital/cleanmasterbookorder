<html lang="ar">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>طلب خدمة تنظيف - كلين ماستر</title>
  <meta name="description" content="احجز خدمة تنظيف احترافية من شركة كلين ماستر في ثوانٍ عبر واتساب – شقق، سجاد، ستائر والمزيد بأسعار مميزة!" />
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      direction: rtl;
      background: url('https://your-image-link.com/cleaning-animation.gif') no-repeat center center fixed;
      background-size: cover;
      animation: fadeIn 2s ease-in-out;
    }
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }
    .container {
      width: 350px;
      margin: auto;
      padding: 20px;
      border: 1px solid #ccc;
      border-radius: 10px;
      background: #e0f7fa;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    select, input, button, textarea {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      border-radius: 6px;
      border: 1px solid #aaa;
      font-size: 16px;
    }
    .logo {
      width: 120px;
      height: auto;
      margin-bottom: 10px;
    }
    button {
      background-color: #007BFF;
      color: white;
      border: none;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #0056b3;
    }
    @media (max-width: 500px) {
      .container {
        width: 90%;
      }
      select, input, button, textarea {
        font-size: 14px;
      }
    }
    .payment-box {
      font-weight: bold;
      background-color: #ffeeba;
      padding: 10px;
      border-radius: 6px;
      border: 1px solid #f5c518;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div class="container">
    <img src="https://i.imgur.com/ZKn7xDn.png" alt="شعار الشركة" class="logo" />
    <h2>طلب خدمة تنظيف - شركة كلين ماستر</h2>

    <div id="servicesContainer">
      <div class="serviceItem">
        <label>اختر الخدمة</label>
        <select class="service" onchange="calculatePrice()">
          <option value="14">تنظيف شقه بعد التشطيب (سعر المتر 14ج)</option>
          <option value="7">تنظيف سجاد المسجد (سعر المتر 7ج)</option>
          <option value="100">تنظيف السجاد (صغيرة 100ج)</option>
          <option value="150">تنظيف السجاد (كبيرة 150ج)</option>
          <option value="150">تنظيف ستائر (صغيرة 150ج)</option>
          <option value="200">تنظيف ستائر (كبيرة 200ج)</option>
          <option value="450">تنظيف الأنتريهات (450ج)</option>
          <option value="450">تنظيف الركن (صغيرة 450ج)</option>
          <option value="70">تنظيف الركن (كبيرة سعر المتر 70ج)</option>
          <option value="350">تنظيف مراتب (صغيرة 350ج)</option>
          <option value="550">تنظيف مراتب (كبيرة 550ج)</option>
          <option value="250">تنظيف ليزي بوي (250ج)</option>
          <option value="75">تنظيف كرسي سفرة (75ج)</option>
          <option value="0">دهان وش نضافة (السعر بعد المعاينة)</option>
        </select>
        <input type="number" class="area" placeholder="المساحة أو العدد" oninput="calculatePrice()" required />
        <button onclick="removeService(this)">❌ حذف</button>
      </div>
    </div>

    <button onclick="addService()">إضافة خدمة أخرى</button>
    <p>السعر الإجمالي: <span id="totalPrice">0</span> جنيه</p>

    <input type="text" id="name" placeholder="الاسم" required />
    <input type="tel" id="phone" placeholder="رقم الهاتف" required />
    <input type="text" id="address" placeholder="العنوان بالتفصيل" required />
    <input type="date" id="date" placeholder="حدد تاريخ الحجز" required />
    <textarea id="notes" placeholder="ملاحظات إضافية"></textarea>
    <button id="locationBtn" onclick="getLocation()">📍 مشاركة الموقع</button>
    <input type="text" id="location" placeholder="موقعك" readonly />

    <div class="payment-box">
      برجاء دفع ربع اجمالى مبلغ الحجز مقدما لتأكيد الحجز<br>
      <strong>لن يتم تأكيد الحجز إلا بعد رفع صورة إثبات الدفع</strong><br>
      فودافون كاش أو انستا باي على رقم: <strong>01013373634</strong><br>
      💰 ربع المبلغ المستحق: <span id="quarterPrice">0</span> جنيه
    </div>
    <input type="file" id="paymentProof" accept="image/*" required>

    <button onclick="confirmAndSend()">تأكيد الحجز</button>
  </div>

  <script>
    function calculatePrice() {
      let totalPrice = 0;
      let anyFilled = false;
      document.querySelectorAll('.serviceItem').forEach(item => {
        let servicePrice = parseFloat(item.querySelector(".service").value);
        let quantityInput = item.querySelector(".area").value;
        if (quantityInput) {
          let quantity = parseFloat(quantityInput);
          if (!isNaN(quantity)) {
            totalPrice += servicePrice * quantity;
            anyFilled = true;
          }
        }
      });
      document.getElementById("totalPrice").innerText = anyFilled ? totalPrice : 0;
    }

    function addService() {
      let serviceOptions = document.querySelector(".service").innerHTML;
      let container = document.getElementById("servicesContainer");
      let newService = document.createElement("div");
      newService.classList.add("serviceItem");
      newService.innerHTML = `
        <label>اختر الخدمة</label>
        <select class="service" onchange="calculatePrice()">` + serviceOptions + `</select>
        <input type="number" class="area" placeholder="المساحة أو العدد" oninput="calculatePrice()" required>
        <button onclick="removeService(this)">❌ حذف</button>
      `;
      container.appendChild(newService);
    }

    function removeService(button) {
      button.parentElement.remove();
      calculatePrice();
    }

    function getLocation() {
      const locationBtn = document.getElementById("locationBtn");
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(function(position) {
          let latitude = position.coords.latitude;
          let longitude = position.coords.longitude;
          let locationUrl = `https://www.google.com/maps?q=${latitude},${longitude}`;
          document.getElementById("location").value = locationUrl;
          locationBtn.textContent = "✅ تم تحديد الموقع";
        }, function(error) {
          alert("لا يمكن تحديد موقعك، يرجى السماح بالوصول إلى الموقع.");
        });
      } else {
        alert("المتصفح لا يدعم تحديد الموقع الجغرافي.");
      }
    }

    async function uploadImageToImgbb(file) {
      const formData = new FormData();
      formData.append("image", file);
      const response = await fetch("https://api.imgbb.com/1/upload?key=bde613bd4475de5e00274a795091ba04", {
        method: "POST",
        body: formData
      });
      const data = await response.json();
      return data.success ? data.data.url : "لم يتم رفع صورة";
    }

    async function confirmAndSend() {
      const proofInput = document.getElementById("paymentProof");
      if (proofInput.files.length === 0) {
        alert("يرجى رفع صورة إثبات الدفع أولاً لتأكيد الحجز.");
        return;
      }

      if (confirm("هل أنت متأكد من إرسال الطلب؟")) {
        const proofUrl = await uploadImageToImgbb(proofInput.files[0]);
        sendWhatsApp(proofUrl);
      }
    }

    function sendWhatsApp(proofUrl) {
      let phoneNumber = "201013373634";
      let name = document.getElementById("name").value.trim();
      let phone = document.getElementById("phone").value.trim();
      let address = document.getElementById("address").value.trim();
      let date = document.getElementById("date").value.trim();
      let notes = document.getElementById("notes").value.trim() || "لا يوجد";
      let location = document.getElementById("location").value.trim() || "لم يتم مشاركة الموقع";
      let totalPrice = document.getElementById("totalPrice").innerText;

      let services = [];
      document.querySelectorAll(".serviceItem").forEach(item => {
        let serviceText = item.querySelector(".service").selectedOptions[0].text;
        let quantity = item.querySelector(".area").value || 1;
        services.push(`🔹 ${serviceText} - ${quantity}`);
      });

      let message = `👤 الاسم: ${name}
📞 الهاتف: ${phone}
📍 الموقع: ${location}
📍 العنوان: ${address}
📅 التاريخ: ${date}
📝 ملاحظات: ${notes}
💰 السعر الإجمالي: ${totalPrice} جنيه
💳 إثبات الدفع: ${proofUrl}
🧹 الخدمات:
${services.join("\\n")}`;

      let waUrl = `https://wa.me/${phoneNumber}?text=${encodeURIComponent(message)}`;
      window.open(waUrl, "_blank");
    }

    function updateQuarterPrice() {
      const total = parseFloat(document.getElementById("totalPrice").innerText) || 0;
      const quarter = Math.ceil(total * 0.25);
      document.getElementById("quarterPrice").innerText = quarter;
    }

    const observer = new MutationObserver(updateQuarterPrice);
    observer.observe(document.getElementById("totalPrice"), { childList: true });
    updateQuarterPrice();
  </script>
</body>
</html>
