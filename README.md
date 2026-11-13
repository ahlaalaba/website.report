<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تقرير مضيف أهل العباء</title>
    <style>
        :root {
            --primary-color: #1b4332;
            --secondary-color: #2d6a4f;
            --accent-color: #d8f3dc;
            --bg-color: #f4f6f4;
            --text-color: #2b2b2b;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 20px;
        }

        .container {
            max-width: 850px;
            margin: 0 auto;
            background: #ffffff;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
            border-top: 6px solid var(--primary-color);
        }

        h2 {
            text-align: center;
            color: var(--primary-color);
            margin-bottom: 5px;
            font-size: 26px;
        }

        .subtitle {
            text-align: center;
            color: #666;
            margin-bottom: 25px;
            font-size: 14px;
        }

        .info-bar {
            display: flex;
            justify-content: space-between;
            background: var(--accent-color);
            padding: 12px 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            font-size: 14px;
            font-weight: bold;
            color: var(--secondary-color);
        }

        .form-group {
            margin-bottom: 18px;
        }

        label {
            display: block;
            margin-bottom: 6px;
            font-weight: 600;
            color: var(--primary-color);
        }

        input[type="text"],
        input[type="email"],
        select {
            width: 100%;
            padding: 10px 12px;
            border: 1px solid #ccc;
            border-radius: 6px;
            font-size: 14px;
            box-sizing: border-box;
            transition: border-color 0.3s;
        }

        input:focus, select:focus {
            border-color: var(--primary-color);
            outline: none;
            box-shadow: 0 0 5px rgba(27, 67, 50, 0.2);
        }

        /* تنسيق جدول الاستشارات */
        .consult-table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            background: #fff;
        }

        .consult-table th, .consult-table td {
            border: 1px solid #dcdcdc;
            padding: 12px;
            text-align: right;
            vertical-align: middle;
        }

        .consult-table th {
            background-color: var(--primary-color);
            color: white;
            font-size: 15px;
        }

        .consult-table textarea {
            width: 100%;
            height: 70px;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            resize: vertical;
            font-family: inherit;
            box-sizing: border-box;
        }

        .consult-table textarea:focus {
            border-color: var(--primary-color);
            outline: none;
        }

        .actions-container {
            display: flex;
            gap: 15px;
            margin-top: 25px;
        }

        button {
            flex: 1;
            padding: 12px 20px;
            font-size: 15px;
            font-weight: bold;
            border-radius: 6px;
            cursor: pointer;
            border: none;
            transition: background 0.3s, transform 0.1s;
        }

        .btn-email {
            background-color: var(--primary-color);
            color: white;
        }

        .btn-email:hover {
            background-color: var(--secondary-color);
        }

        .btn-print {
            background-color: #495057;
            color: white;
        }

        .btn-print:hover {
            background-color: #343a40;
        }

        button:active {
            transform: scale(0.98);
        }

        /* إعدادات خاصة عند الطباعة */
        @media print {
            body {
                background: white;
                padding: 0;
            }
            .container {
                box-shadow: none;
                border: none;
                padding: 0;
                max-width: 100%;
            }
            .actions-container, input, select {
                display: none !important;
            }
            .consult-table textarea {
                border: none;
                background: transparent;
                resize: none;
                height: auto;
                font-size: 14px;
            }
        }

        @media (max-width: 600px) {
            .info-bar {
                flex-direction: column;
                gap: 8px;
                text-align: center;
            }
            .actions-container {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>

<div class="container">
    <h2>تقرير مضيف أهل العباء</h2>
    <div class="subtitle">نموذج تقرير رسمي للإدارة والمتابعة</div>

    <form id="reportForm">
        
        <!-- شريط المعلومات التلقائية -->
        <div class="info-bar">
            <span id="currentDate">التاريخ: جاري التحميل...</span>
            <span id="currentTime">الساعة: جاري التحميل...</span>
        </div>

        <!-- الاسم واللجنة -->
        <div class="form-group">
            <label for="fullName">الاسم الكريم:</label>
            <input type="text" id="fullName" required placeholder="أدخل الاسم الكريم هنا...">
        </div>

        <div class="form-group">
            <label for="committee">اللجنة / المنصب:</label>
            <select id="committee" required>
                <option value="" disabled selected>-- اختر اللجنة أو المنصب --</option>
                <option value="الرئيس">الرئيس</option>
                <option value="نائب الرئيس">نائب الرئيس</option>
                <option value="اللجنة الإعلامية">اللجنة الإعلامية</option>
                <option value="لجنة العزاء">لجنة العزاء</option>
            </select>
        </div>

        <!-- إيميل الإدارة -->
        <div class="form-group">
            <label for="adminEmail">بريد الإدارة (المرسل إليه):</label>
            <input type="email" id="adminEmail" required placeholder="admin@example.com" value="management@ahlelabaa.com">
        </div>

        <!-- جدول الاستشارات والملاحظات -->
        <label>جدول الاستشارات والملاحظات:</label>
        <table class="consult-table">
            <thead>
                <tr>
                    <th style="width: 25%;">القسم / البند</th>
                    <th style="width: 75%;">التفاصيل والملاحظات</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td><strong>الاستشارة الأولى والملاحظات</strong></td>
                    <td>
                        <textarea id="consultation1" placeholder="اكتب الاستشارة الأولى والملاحظات التابعة لها..."></textarea>
                    </td>
                </tr>
                <tr>
                    <td><strong>الاستشارة الثانية</strong></td>
                    <td>
                        <textarea id="consultation2" placeholder="اكتب تفاصيل الاستشارة الثانية..."></textarea>
                    </td>
                </tr>
                <tr>
                    <td><strong>الاستشارة الثالثة</strong></td>
                    <td>
                        <textarea id="consultation3" placeholder="اكتب تفاصيل الاستشارة الثالثة..."></textarea>
                    </td>
                </tr>
            </tbody>
        </table>

        <!-- أزرار الإجراءات -->
        <div class="actions-container">
            <button type="button" class="btn-email" onclick="sendReport()">إرسال التقرير للإدارة 📨</button>
            <button type="button" class="btn-print" onclick="window.print()">طباعة التقرير / حفظ PDF 🖨️</button>
        </div>

    </form>
</div>

<script>
    // تعيين التاريخ والوقت تلقائياً عند فتح الصفحة
    function updateDateTime() {
        const now = new Date();
        const optionsDate = { year: 'numeric', month: '2-digit', day: '2-digit' };
        document.getElementById('currentDate').innerText = 'التاريخ: ' + now.toLocaleDateString('ar-BH', optionsDate);
        
        const optionsTime = { hour: '2-digit', minute: '2-digit', second: '2-digit', hour12: true };
        document.getElementById('currentTime').innerText = 'الساعة: ' + now.toLocaleTimeString('ar-BH', optionsTime);
    }

    updateDateTime();
    setInterval(updateDateTime, 1000);

    // دالة إرسال التقرير عبر البريد الإلكتروني
    function sendReport() {
        const name = document.getElementById('fullName').value;
        const committee = document.getElementById('committee').value;
        const email = document.getElementById('adminEmail').value;
        const c1 = document.getElementById('consultation1').value || 'لا يوجد';
        const c2 = document.getElementById('consultation2').value || 'لا يوجد';
        const c3 = document.getElementById('consultation3').value || 'لا يوجد';
        const dateStr = document.getElementById('currentDate').innerText;
        const timeStr = document.getElementById('currentTime').innerText;

        if (!name || !committee) {
            alert('الرجاء إدخال الاسم الكريم واختيار اللجنة قبل الإرسال.');
            return;
        }

        const subject = encodeURIComponent(`تقرير رسمي - ${committee} - ${name}`);
        const body = encodeURIComponent(
            `السلام عليكم ورحمة الله وبركاته،\n\n` +
            `إليك تفاصيل تقرير "مضيف أهل العباء":\n\n` +
            `👤 الاسم الكريم: ${name}\n` +
            `🏛️ اللجنة / المنصب: ${committee}\n` +
            `📅 ${dateStr} | ⏰ ${timeStr}\n\n` +
            `----------------------------------------\n` +
            `1️⃣ الاستشارة الأولى والملاحظات:\n${c1}\n\n` +
            `2️⃣ الاستشارة الثانية:\n${c2}\n\n` +
            `3️⃣ الاستشارة الثالثة:\n${c3}\n` +
            `----------------------------------------\n\n` +
            `مع تحيات إدارة مضيف أهل العباء.`
        );

        window.location.href = `mailto:${email}?subject=${subject}&body=${body}`;
    }
</script>

</body>
</html>
