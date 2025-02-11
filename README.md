<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>إدارة بنوك الدم - الهيئة العامة للرعاية الصحية</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 0;
            direction: rtl;
        }
        h1, h2 {
            text-align: center;
        }
        form {
            max-width: 600px;
            margin: 20px auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        label {
            display: block;
            margin-bottom: 8px;
        }
        input[type="text"], select, textarea {
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .alert {
            padding: 10px;
            background-color: #f44336;
            color: white;
            margin-bottom: 15px;
            border-radius: 4px;
        }
        .message {
            padding: 10px;
            background-color: #2196F3;
            color: white;
            margin-bottom: 15px;
            border-radius: 4px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: center;
        }
        th {
            background-color: #f4f4f4;
        }
    </style>
</head>
<body>

<h1>إدارة بنوك الدم - الهيئة العامة للرعاية الصحية</h1>

<h2>تسجيل المستخدمين</h2>

<form id="userRegistrationForm">
    <label for="role">الدور:</label>
    <select id="role" name="role" required>
        <option value="patient">مريض</option>
        <option value="doctor">طبيب</option>
        <option value="donor">متبرع</option>
    </select>

    <label for="name">الاسم الكامل:</label>
    <input type="text" id="name" name="name" required>

    <label for="bloodType">فصيلة الدم:</label>
    <select id="bloodType" name="bloodType">
        <option value="A+">A+</option>
        <option value="B+">B+</option>
        <option value="AB+">AB+</option>
        <option value="O+">O+</option>
        <option value="A-">A-</option>
        <option value="B-">B-</option>
        <option value="AB-">AB-</option>
        <option value="O-">O-</option>
    </select>

    <label for="rarity">ندرة الفصيلة:</label>
    <select id="rarity" name="rarity">
        <option value="عادية">عادية</option>
        <option value="نادرة">نادرة</option>
        <option value="عالية الندرة">عالية الندرة</option>
    </select>

    <button type="submit">تسجيل</button>
</form>

<h2>حجز أكياس الدم</h2>

<form id="bloodReservationForm">
    <label for="governorate">اسم المحافظة:</label>
    <select id="governorate" name="governorate" required>
        <option value="Cairo">القاهرة</option>
        <option value="Alexandria">الإسكندرية</option>
        <option value="Giza">الجيزة</option>
        <option value="PortSaid">بورسعيد</option>
    </select>

    <label for="hospital">المستشفى:</label>
    <select id="hospital" name="hospital" required>
        <option value="CairoHospital">مستشفى القاهرة التخصصي</option>
        <option value="AlexandriaHospital">مستشفى الإسكندرية العام</option>
        <option value="GizaHospital">مستشفى الجيزة المركزي</option>
        <option value="PortSaidHospital">مستشفى بورسعيد التعليمي</option>
    </select>

    <label for="bloodBank">بنك الدم التابع للمستشفى:</label>
    <select id="bloodBank" name="bloodBank" required>
        <option value="CairoBloodBank">بنك دم مستشفى القاهرة</option>
        <option value="AlexandriaBloodBank">بنك دم مستشفى الإسكندرية</option>
        <option value="GizaBloodBank">بنك دم مستشفى الجيزة</option>
        <option value="PortSaidBloodBank">بنك دم مستشفى بورسعيد</option>
    </select>

    <label for="bloodTypeReservation">فصيلة الدم المطلوبة:</label>
    <select id="bloodTypeReservation" name="bloodTypeReservation" required>
        <option value="A+">A+</option>
        <option value="B+">B+</option>
        <option value="AB+">AB+</option>
        <option value="O+">O+</option>
        <option value="A-">A-</option>
        <option value="B-">B-</option>
        <option value="AB-">AB-</option>
        <option value="O-">O-</option>
    </select>

    <label for="date">تاريخ العملية:</label>
    <input type="date" id="date" name="date" required>

    <button type="submit">حجز</button>
</form>

<h2>إدارة المخزون</h2>

<table id="inventoryTable">
    <thead>
        <tr>
            <th>المستشفى</th>
            <th>فصيلة الدم</th>
            <th>الندرة</th>
            <th>الكمية المتاحة</th>
        </tr>
    </thead>
    <tbody>
        <!-- Inventory data will be dynamically added here -->
    </tbody>
</table>

<div id="alerts"></div>

<script>
    const usersData = [];
    const reservationsData = [];
    const inventoryData = [
        { hospital: "مستشفى القاهرة التخصصي", bloodType: "A+", rarity: "عادية", quantity: 50 },
        { hospital: "مستشفى القاهرة التخصصي", bloodType: "O-", rarity: "عالية الندرة", quantity: 5 },
        { hospital: "مستشفى الإسكندرية العام", bloodType: "AB-", rarity: "نادرة", quantity: 3 },
        { hospital: "مستشفى الإسكندرية العام", bloodType: "B+", rarity: "عادية", quantity: 40 },
        { hospital: "مستشفى الجيزة المركزي", bloodType: "O+", rarity: "عادية", quantity: 60 },
        { hospital: "مستشفى بورسعيد التعليمي", bloodType: "A-", rarity: "نادرة", quantity: 7 }
    ];
    const alertsDiv = document.getElementById('alerts');
    const inventoryTableBody = document.querySelector('#inventoryTable tbody');

    // Display inventory data
    function displayInventory() {
        inventoryTableBody.innerHTML = '';
        inventoryData.forEach(item => {
            const row = document.createElement('tr');
            row.innerHTML = `
                <td>${item.hospital}</td>
                <td>${item.bloodType}</td>
                <td>${item.rarity}</td>
                <td>${item.quantity}</td>
            `;
            inventoryTableBody.appendChild(row);
        });
    }

    displayInventory();

    // Check inventory levels
    function checkInventoryLevels() {
        const criticalItems = inventoryData.filter(item => item.rarity === "عالية الندرة" && item.quantity < 10);
        if (criticalItems.length > 0) {
            showAlert(`تحذير: نقص في فصائل الدم عالية الندرة!`, 'warning');
        }
    }

    checkInventoryLevels();

    // User registration form submission
    document.getElementById('userRegistrationForm').addEventListener('submit', function(event) {
        event.preventDefault();
        const formData = {
            role: document.getElementById('role').value,
            name: document.getElementById('name').value,
            bloodType: document.getElementById('bloodType').value,
            rarity: document.getElementById('rarity').value
        };
        usersData.push(formData);
        event.target.reset();
        showAlert(`تم التسجيل بنجاح!`, 'success');
    });

    // Blood reservation form submission
    document.getElementById('bloodReservationForm').addEventListener('submit', function(event) {
        event.preventDefault();
        const formData = {
            hospital: document.getElementById('hospital').value,
            bloodType: document.getElementById('bloodTypeReservation').value,
            date: document.getElementById('date').value
        };

        const availableStock = inventoryData.find(item => 
            item.hospital === formData.hospital && 
            item.bloodType === formData.bloodType && 
            item.quantity > 0
        );

        if (availableStock) {
            availableStock.quantity--;
            reservationsData.push(formData);
            displayInventory();
            checkInventoryLevels();
            showAlert(`تم الحجز بنجاح!`, 'success');
        } else {
            showAlert(`لا يوجد مخزون كافٍ من فصيلة الدم المطلوبة.`, 'warning');
        }

        event.target.reset();
    });

    // Show alert messages
    function showAlert(message, type) {
        const alertDiv = document.createElement('div');
        alertDiv.className = type === 'success' ? 'message' : 'alert';
        alertDiv.textContent = message;
        alertsDiv.appendChild(alertDiv);

        setTimeout(() => {
            alertDiv.remove();
        }, 5000);
    }
</script>

</body>
</html>
