# culture_match-appfrom pathlib import Path

# สร้าง HTML เว็บจำลอง Culture Match App
html_content = """
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <title>Culture Match App</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body { font-family: 'Prompt', sans-serif; margin: 0; padding: 0; background-color: #f4f4f4; }
        .page { display: none; padding: 40px; text-align: center; }
        .page.active { display: block; }
        button { padding: 15px 30px; font-size: 16px; border: none; background-color: #4CAF50; color: white; border-radius: 5px; margin-top: 20px; }
        .option { margin: 15px 0; }
    </style>
</head>
<body>

<div class="page active" id="welcome">
    <h2>ยินดีต้อนรับสู่โรงแรม Group 3 Hotel</h2>
    <p>ระบบจะช่วยจับคู่พนักงานที่เหมาะสมกับคุณภายใน 2 นาที</p>
    <button onclick="nextPage('guestType')">เริ่มใช้งาน</button>
</div>

<div class="page" id="guestType">
    <h2>กรุณาเลือกประเภทของแขก</h2>
    <div class="option"><button onclick="selectGuest('ญี่ปุ่น')">แขกชาวญี่ปุ่น</button></div>
    <div class="option"><button onclick="selectGuest('จีน')">แขกชาวจีน</button></div>
    <div class="option"><button onclick="selectGuest('ฝรั่ง')">แขกชาวตะวันตก</button></div>
</div>

<div class="page" id="matchResult">
    <h2>พนักงานที่เหมาะสมกับแขกชาว <span id="guestTypeText"></span></h2>
    <p id="staffTrait"></p>
    <button onclick="nextPage('confirmation')">ยืนยันการเลือก</button>
</div>

<div class="page" id="confirmation">
    <h2>พนักงานจะเข้าพบคุณภายใน 2 นาที</h2>
    <p id="languageMessage"></p>
</div>

<script>
    let selectedGuest = '';

    function nextPage(pageId) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.getElementById(pageId).classList.add('active');
    }

    function selectGuest(guestType) {
        selectedGuest = guestType;
        document.getElementById('guestTypeText').textContent = guestType;

        let trait = '';
        if (guestType === 'ญี่ปุ่น') {
            trait = 'พนักงานที่สุภาพ ตรงเวลา และสามารถสื่อสารภาษาญี่ปุ่นได้';
        } else if (guestType === 'จีน') {
            trait = 'พนักงานที่เข้าใจวัฒนธรรมจีน และสามารถพูดภาษาจีนกลางได้';
        } else if (guestType === 'ฝรั่ง') {
            trait = 'พนักงานที่เป็นกันเอง และสามารถพูดภาษาอังกฤษได้คล่อง';
        }
        document.getElementById('staffTrait').textContent = trait;

        nextPage('matchResult');
    }

    document.querySelector("#matchResult button").addEventListener("click", function() {
        let message = '';
        if (selectedGuest === 'ญี่ปุ่น') {
            message = 'ภาษาที่ใช้ในการสื่อสาร: ภาษาญี่ปุ่น (日本語)';
        } else if (selectedGuest === 'จีน') {
            message = 'ภาษาที่ใช้ในการสื่อสาร: ภาษาจีนกลาง (中文)';
        } else if (selectedGuest === 'ฝรั่ง') {
            message = 'Language used for communication: English';
        }
        document.getElementById('languageMessage').textContent = message;
    });
</script>

</body>
</html>
"""

# บันทึกเป็นไฟล์ HTML
output_path = Path("/mnt/data/culture_match_app.html")
output_path.write_text(html_content, encoding="utf-8")

output_path.name
