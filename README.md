## Hi there 👋

<!--
**aipenrai/aipenrai** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>จองโต๊ะโรงอาหาร</title>
  <style>
    body {
      background-color: #e0f7fa;
      font-family: 'Segoe UI', sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .app-container {
      background-color: #ffffff;
      border-radius: 30px;
      padding: 30px 20px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
      width: 320px;
    }

    h2 {
      text-align: center;
      margin-bottom: 20px;
      color: #00796B;
    }

    input {
      width: 100%;
      padding: 10px;
      font-size: 16px;
      margin-bottom: 20px;
      border-radius: 10px;
      border: 1px solid #ccc;
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 10px;
    }

    .table-btn {
      padding: 20px;
      font-size: 16px;
      border: none;
      border-radius: 15px;
      cursor: pointer;
      color: white;
      font-weight: bold;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .available {
      background-color: #4CAF50;
    }

    .reserved {
      background-color: #D32F2F;
    }

    .disabled {
      opacity: 0.5;
      pointer-events: none;
    }

    #popup {
      margin-top: 20px;
      background-color: #e8f5e9;
      padding: 15px;
      border-radius: 12px;
      text-align: center;
      display: none;
      color: #388e3c;
      font-size: 16px;
      font-weight: bold;
    }

    #cancelBtn {
      margin-top: 15px;
      background-color: #ff8a65;
      color: white;
      padding: 8px 16px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
  </style>
</head>
<body>

<div class="app-container">
  <h2>ระบบจองโต๊ะ</h2>

  <input type="text" id="nameInput" placeholder="กรอกชื่อของคุณ...">

  <div class="grid" id="tableArea">
    <!-- ปุ่มโต๊ะจะถูกสร้างด้วย JS -->
  </div>

  <div id="popup">
    ✅ จองสำเร็จ<br>
    โต๊ะ: <span id="tableNum"></span><br>
    โดย: <span id="userName"></span><br>
    <button id="cancelBtn">ยกเลิกการจอง</button>
  </div>
</div>

<script>
  const tableArea = document.getElementById('tableArea');
  const popup = document.getElementById('popup');
  const tableNum = document.getElementById('tableNum');
  const userName = document.getElementById('userName');
  const cancelBtn = document.getElementById('cancelBtn');
  const nameInput = document.getElementById('nameInput');
  const total = 6;

  let alreadyBooked = false;
  let bookedBtn = null;

  for (let i = 1; i <= total; i++) {
    const btn = document.createElement('button');
    btn.innerText = `โต๊ะ ${i}`;
    btn.classList.add('table-btn', 'available');
    btn.dataset.id = i;

    btn.onclick = () => {
      const name = nameInput.value.trim();
      if (!name) {
        alert("กรุณากรอกชื่อก่อนจองโต๊ะนะครับ");
        return;
      }

      if (!alreadyBooked) {
        btn.classList.remove('available');
        btn.classList.add('reserved');
        btn.innerText = `จองแล้ว`;

        const allButtons = document.querySelectorAll('.table-btn');
        allButtons.forEach(b => {
          if (b !== btn) b.classList.add('disabled');
        });

        tableNum.innerText = i;
        userName.innerText = name;
        popup.style.display = 'block';

        alreadyBooked = true;
        bookedBtn = btn;
        nameInput.disabled = true;
      }
    };

    tableArea.appendChild(btn);
  }

  cancelBtn.onclick = () => {
    if (bookedBtn) {
      bookedBtn.classList.remove('reserved');
      bookedBtn.classList.add('available');
      bookedBtn.innerText = `โต๊ะ ${bookedBtn.dataset.id}`;
    }

    document.querySelectorAll('.table-btn').forEach(b => {
      b.classList.remove('disabled');
    });

    popup.style.display = 'none';
    nameInput.disabled = false;
    alreadyBooked = false;
    bookedBtn = null;
  };
</script>

</body>
</html>
