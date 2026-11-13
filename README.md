<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مضيف أهل العباء - تسجيل التقرير</title>
    <style>
        :root {
            --primary-color: #0d5c3d;
            --secondary-color: #148f5a;
            --bg-color: #f4f7f6;
            --text-color: #333;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        .container {
            background: #fff;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            width: 100%;
            max-width: 600px;
        }
        h2 {
            text-align: center;
            color: var(--primary-color);
            margin-bottom: 25px;
        }
        .form-group {
            margin-bottom: 20px;
        }
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #555;
        }
        input[type="text"], input[type="tel"], textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 16px;
            box-sizing: border-box;
            transition: border-color 0.3s;
            font-family: inherit;
        }
        input[type="text"]:focus, input[type="tel"]:focus, textarea:focus {
            border-color: var(--primary-color);
            outline: none;
        }
        textarea {
            resize: vertical;
            height: 100px;
        }
        .datetime-display {
            background: #eef2f1;
            padding: 10px;
            border-radius: 6px;
            font-weight: bold;
            color: var(--secondary-color);
            text-align: center;
            margin-bottom: 20px;
        }
        .btn-container {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin-top: 25px;
        }
        button {
            flex: 1;
            padding: 12px;
            border: none;
            border-radius: 6px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: background 0.3s;
        }
        .btn-submit { background-color: var(--primary-color); color: white; }
        .btn-submit:hover { background-color: #09452e; }
        
        .btn-print { background-color: #34495e; color: white; }
        .btn-print:hover { background-color: #2c3e50; }
        
        .btn-toggle { background-color: #e67e22; color: white; }
        .btn-toggle:hover { background-color: #d35400; }

        .success-msg {
            background-color: #d4edda;
            color: #155724;
            padding: 10px;
            border-radius: 6px;
            text-align: center;
            margin-bottom: 15px;
            display: none;
        }

        @media print {
            body { background: #fff; padding: 0; }
            .container { box-shadow: none; padding: 0; max-width: 100%; }
            .btn-container, .success-msg, hr { display: none; }
        }
    </style>
</head>
<body>

<div class="container" id="reportSection">
    <h2>مضيف أهل العباء - تسجيل التقرير</h2>
    
    <div id="successMsg" class="success-msg">تم إرسال وحفظ التقرير بنجاح!</div>

    <div class="datetime-display" id="datetimeDisplay">
        التاريخ والوقت: جاري التحميل...
    </div>

    <form id="reportForm">
        <div class="form-group">
            <label for="clientName">اسم الكريم:</label>
            <input type="text" id="clientName" required placeholder="أدخل اسم الكريم هنا">
        </div>

        <div class="form-group">
            <label for="clientPhone">رقم الهاتف:</label>
            <input type="tel" id="clientPhone" required placeholder="أدخل رقم الهاتف">
        </div>

        <div class="form-group">
            <label for="clientNotes">الملاحظات:</label>
            <textarea id="clientNotes" placeholder="اكتب الملاحظات أو التفاصيل هنا..."></textarea>
        </div>

        <div class="btn-container">
            <button type="submit" class="btn-submit">إرسال وحفظ</button>
            <button type="button" class="btn-print" onclick="window.print()">طباعة</button>
            <button type="button" class="btn-toggle" onclick="toggleView()">إخفاء / عرض النموذج</button>
        </div>
    </form>
</div>

<script>
    // تحديث التاريخ والوقت تلقائياً
    function updateDateTime() {
        const now = new Date();
        const optionsDate = { year: 'numeric', month: '2-digit', day: '2-digit' };
        const optionsTime = { hour: '2-digit', minute: '2-digit', second: '2-digit', hour12: true };
        
        const dateStr = now.toLocaleDateString('ar-BH', optionsDate);
        const timeStr = now.toLocaleTimeString('ar-BH', optionsTime);
        
        document.getElementById('datetimeDisplay').innerText = `التاريخ: ${dateStr} | الساعة: ${timeStr}`;
    }
    setInterval(updateDateTime, 1000);
    updateDateTime();

    // حفظ البيانات في التخزين المحلي (LocalStorage)
    document.getElementById('reportForm').addEventListener('submit', function(e) {
        e.preventDefault();
        
        const name = document.getElementById('clientName').value;
        const phone = document.getElementById('clientPhone').value;
        const notes = document.getElementById('clientNotes').value;
        const now = new Date();
        const dateTimeStr = now.toLocaleString('ar-BH');

        const newReport = {
            id: Date.now(),
            name: name,
            phone: phone,
            datetime: dateTimeStr,
            status: 'قيد المراجعة',
            notes: notes
        };

        let reports = JSON.parse(localStorage.getItem('abha_reports')) || [];
        reports.push(newReport);
        localStorage.setItem('abha_reports', JSON.stringify(reports));

        const msg = document.getElementById('successMsg');
        msg.style.display = 'block';
        document.getElementById('reportForm').reset();

        setTimeout(() => {
            msg.style.display = 'none';
        }, 3000);
    });

    // إخفاء وعرض محتوى النموذج
    function toggleView() {
        const section = document.getElementById('reportSection');
        const formElements = section.querySelectorAll('form, .datetime-display, h2');
        formElements.forEach(el => {
            el.style.display = el.style.display === 'none' ? '' : 'none';
        });
    }
</script>

</body>
</html>
