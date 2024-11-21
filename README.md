<!DOCTYPE html>
<html lang="th">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ค้นหาข้อมูลนักศึกษา</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        background-color: #f3f3f3;
        margin: 0;
        padding: 20px;
      }
      h1 {
        color: #4e73df;
        text-align: center;
      }
      input, button {
        padding: 12px;
        margin: 10px 0;
        width: 100%;
        font-size: 16px;
        border-radius: 5px;
        border: 1px solid #ccc;
      }
      button {
        background-color: #4e73df;
        color: white;
        border: none;
        cursor: pointer;
        transition: background-color 0.3s ease;
      }
      button:hover {
        background-color: #2e59d9;
      }
      .result {
        margin-top: 20px;
        padding: 20px;
        background-color: #fff;
        border-radius: 5px;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      }
      .view-photo-btn {
        padding: 10px 20px;
        background-color: #28a745;
        color: white;
        text-decoration: none;
        border-radius: 5px;
        display: inline-block;
        text-align: center;
        transition: background-color 0.3s ease;
      }
      .view-photo-btn:hover {
        background-color: #218838;
      }
      .details p {
        font-size: 18px;
        margin: 5px 0;
      }
    </style>
  </head>
  <body>
    <h1>ค้นหาข้อมูลนักศึกษา</h1>
    
    <label for="studentId">กรอกรหัสนักศึกษา:</label>
    <input type="text" id="studentId" placeholder="กรอกรหัสนักศึกษา" maxlength="50">
    
    <button onclick="searchStudent()">ค้นหา</button>
    <div id="result" class="result"></div>

    <script>
      function searchStudent() {
        const studentId = document.getElementById('studentId').value;
        
        // ส่งรหัสนักศึกษาไปยัง Google Apps Script
        google.script.run.withSuccessHandler(showResult).getStudentData(studentId);
      }
      
      function showResult(data) {
        const resultDiv = document.getElementById('result');
        if (data) {
          resultDiv.innerHTML = `
            <div class="details">
              <p><strong>รหัสนักศึกษา:</strong> ${data.id}</p>
              <p><strong>ชื่อ-นามสกุล:</strong> ${data.name}</p>
              <p><strong>คณะ:</strong> ${data.faculty}</p>
              <p><strong>สาขา:</strong> ${data.department}</p>
              <p><strong>ชั้นปี:</strong> ${data.year}</p>
              <p><strong>ชั่วโมงกิจกรรม:</strong> ${data.activityHours} ชั่วโมง</p>
              <p><strong>กิจกรรมที่เข้าร่วม:</strong> ${data.activities}</p>
              <p><strong>วันและเวลาที่เข้าร่วมกิจกรรม:</strong> ${data.activityDateTime}</p>
              <a href="${data.photo}" target="_blank" class="view-photo-btn">ดูรูปภาพกิจกรรม</a>
            </div>
          `;
        } else {
          resultDiv.innerHTML = '<p>ไม่พบข้อมูลนักศึกษา</p>';
        }
      }
    </script>
  </body>
</html>
