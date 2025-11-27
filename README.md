<html lang="th">
<head>
    <meta charset="UTF-8" />
    <title>ระบบบริหารจัดการการเบิกพัสดุ - โรงเรียนวัดสังเวช</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <style>
        :root {
            --primary: #2563eb;
            --primary-dark: #1d4ed8;
            --bg: #f3f4f6;
            --card-bg: #ffffff;
            --text-main: #111827;
            --text-muted: #6b7280;
            --border: #e5e7eb;
            --danger: #dc2626;
            --success: #16a34a;
            --warning: #f59e0b;
            --radius-lg: 16px;
            --transition: 0.2s ease-in-out;
        }

        * {
            box-sizing: border-box;
            font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
        }

        body {
            margin: 0;
            background: var(--bg);
            color: var(--text-main);
        }

        .layout {
            display: grid;
            grid-template-columns: 260px 1fr;
            min-height: 100vh;
        }

        /* Sidebar */
        .sidebar {
            background: #0f172a;
            color: white;
            padding: 24px 16px;
            display: flex;
            flex-direction: column;
            gap: 24px;
        }

        .brand {
            display: flex;
            flex-direction: column;
            gap: 4px;
        }

        .brand-title {
            font-size: 1.2rem;
            font-weight: 700;
        }

        .brand-subtitle {
            font-size: 0.85rem;
            color: #9ca3af;
        }

        .nav-section-title {
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 0.08em;
            color: #6b7280;
            margin-bottom: 8px;
        }

        .nav {
            display: flex;
            flex-direction: column;
            gap: 4px;
        }

        .nav button {
            border: none;
            background: transparent;
            color: #e5e7eb;
            text-align: left;
            padding: 10px 12px;
            border-radius: 999px;
            cursor: pointer;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: background var(--transition), color var(--transition), transform var(--transition);
        }

        .nav button span.icon {
            font-size: 1rem;
        }

        .nav button.active {
            background: #1d4ed8;
            color: #ffffff;
            transform: translateX(4px);
        }

        .nav button:hover:not(.active) {
            background: rgba(148, 163, 184, 0.25);
        }

        .sidebar-footer {
            margin-top: auto;
            font-size: 0.75rem;
            color: #6b7280;
        }

        /* Main content */
        .main {
            padding: 20px;
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .topbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .topbar-title {
            font-size: 1.4rem;
            font-weight: 600;
        }

        .topbar-right {
            display: flex;
            gap: 8px;
            align-items: center;
            font-size: 0.9rem;
            color: var(--text-muted);
        }

        .badge {
            background: rgba(37, 99, 235, 0.1);
            color: var(--primary-dark);
            padding: 4px 10px;
            border-radius: 999px;
            font-size: 0.75rem;
            font-weight: 500;
        }

        .content {
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .card {
            background: var(--card-bg);
            border-radius: var(--radius-lg);
            padding: 16px 18px;
            box-shadow: 0 10px 25px rgba(15, 23, 42, 0.08);
            border: 1px solid var(--border);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            margin-bottom: 12px;
        }

        .card-title {
            font-size: 1rem;
            font-weight: 600;
        }

        .card-subtitle {
            font-size: 0.8rem;
            color: var(--text-muted);
        }

        .grid {
            display: grid;
            gap: 16px;
        }

        @media (min-width: 900px) {
            .grid-2 {
                grid-template-columns: 2fr 1.4fr;
            }
        }

        @media (max-width: 800px) {
            .layout {
                grid-template-columns: 1fr;
            }
            .sidebar {
                flex-direction: row;
                align-items: center;
                justify-content: space-between;
                position: sticky;
                top: 0;
                z-index: 10;
            }
            .nav {
                flex-direction: row;
                overflow-x: auto;
                max-width: 100%;
            }
            .nav button {
                white-space: nowrap;
                font-size: 0.75rem;
            }
            .sidebar-footer {
                display: none;
            }
        }

        /* Tables */
        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.85rem;
        }

        th, td {
            padding: 8px 6px;
            border-bottom: 1px solid var(--border);
            text-align: left;
        }

        th {
            background: #f9fafb;
            font-weight: 600;
            font-size: 0.8rem;
            color: #4b5563;
        }

        tr:hover td {
            background: #f3f4ff;
        }

        .tag {
            display: inline-flex;
            padding: 2px 8px;
            border-radius: 999px;
            font-size: 0.75rem;
            background: #e5e7eb;
            color: #374151;
        }

        .tag.low {
            background: rgba(239, 68, 68, 0.12);
            color: var(--danger);
        }

        .tag.ok {
            background: rgba(16, 185, 129, 0.12);
            color: var(--success);
        }

        /* Form */
        .form-grid {
            display: grid;
            gap: 10px;
        }

        @media (min-width: 800px) {
            .form-grid-2 {
                grid-template-columns: repeat(2, minmax(0, 1fr));
            }
        }

        label {
            font-size: 0.8rem;
            font-weight: 500;
            display: block;
            margin-bottom: 2px;
        }

        input, select, textarea {
            width: 100%;
            padding: 7px 8px;
            border-radius: 10px;
            border: 1px solid var(--border);
            font-size: 0.85rem;
            outline: none;
            transition: border var(--transition), box-shadow var(--transition), background var(--transition);
            background: #f9fafb;
        }

        input:focus, select:focus, textarea:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 1px rgba(37, 99, 235, 0.2);
            background: white;
        }

        textarea {
            resize: vertical;
            min-height: 70px;
        }

        .btn {
            border-radius: 999px;
            border: none;
            padding: 8px 16px;
            font-size: 0.85rem;
            cursor: pointer;
            display: inline-flex;
            gap: 6px;
            align-items: center;
            justify-content: center;
            transition: background var(--transition), transform var(--transition), box-shadow var(--transition);
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            color: white;
            box-shadow: 0 8px 20px rgba(37, 99, 235, 0.35);
        }

        .btn-primary:hover {
            transform: translateY(-1px);
            box-shadow: 0 12px 26px rgba(37, 99, 235, 0.45);
        }

        .btn-outline {
            background: white;
            border: 1px solid var(--border);
            color: #374151;
        }

        .btn-outline:hover {
            background: #f3f4f6;
        }

        .btn-danger {
            background: rgba(239, 68, 68, 0.1);
            color: var(--danger);
        }

        .btn-danger:hover {
            background: rgba(239, 68, 68, 0.2);
        }

        .btn-xs {
            padding: 3px 8px;
            font-size: 0.7rem;
            border-radius: 999px;
        }

        .actions {
            display: flex;
            gap: 4px;
        }

        /* Dashboard cards */
        .kpi-grid {
            display: grid;
            gap: 10px;
        }

        @media (min-width: 700px) {
            .kpi-grid {
                grid-template-columns: repeat(4, minmax(0, 1fr));
            }
        }

        .kpi-card {
            background: linear-gradient(135deg, #eff6ff, #eef2ff);
            border-radius: 16px;
            padding: 10px 12px;
            border: 1px solid #dbeafe;
        }

        .kpi-label {
            font-size: 0.75rem;
            color: #4b5563;
        }

        .kpi-value {
            font-size: 1.1rem;
            font-weight: 600;
            margin-top: 4px;
        }

        .kpi-caption {
            font-size: 0.75rem;
            color: #6b7280;
        }

        .progress-bar {
            width: 100%;
            height: 6px;
            border-radius: 999px;
            background: #e5e7eb;
            overflow: hidden;
            margin-top: 6px;
        }
        .progress-inner {
            height: 100%;
            width: 40%;
            border-radius: inherit;
            background: linear-gradient(90deg, var(--primary), #22c55e);
            transition: width var(--transition);
        }

        .filter-row {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            align-items: center;
            margin-bottom: 8px;
        }

        .filter-row > * {
            flex: 0 0 auto;
        }

        .filter-row select {
            width: auto;
            min-width: 150px;
        }

        .muted {
            color: var(--text-muted);
            font-size: 0.8rem;
        }

        .pill {
            border-radius: 999px;
            background: #e5e7eb;
            padding: 2px 10px;
            font-size: 0.75rem;
        }

        .print-hint {
            font-size: 0.8rem;
            color: var(--text-muted);
            margin-top: 4px;
        }
    </style>
</head>
<body>
<div class="layout">
    <!-- SIDEBAR -->
    <aside class="sidebar">
        <div class="brand">
            <div class="brand-title">ระบบเบิกพัสดุ</div>
            <div class="brand-subtitle">โรงเรียนวัดสังเวช</div>
        </div>

        <div>
            <div class="nav-section-title">เมนูหลัก</div>
            <div class="nav">
                <button class="nav-link active" data-target="dashboard">
                    <span class="icon">📊</span> แดชบอร์ดภาพรวม
                </button>
                <button class="nav-link" data-target="inventory">
                    <span class="icon">📦</span> พัสดุ (แยกหมวดหมู่)
                </button>
                <button class="nav-link" data-target="request">
                    <span class="icon">📝</span> แบบฟอร์มขอเบิกพัสดุ
                </button>
                <button class="nav-link" data-target="reports">
                    <span class="icon">🖨️</span> พิมพ์รายงาน
                </button>
            </div>
        </div>

        <div>
            <div class="nav-section-title">การจัดการข้อมูล</div>
            <div class="nav">
                <button class="nav-link" data-target="manageItems">
                    <span class="icon">⚙️</span> เพิ่ม-ลบรายการพัสดุ
                </button>
                <button class="nav-link" data-target="manageStaff">
                    <span class="icon">👤</span> ข้อมูลบุคลากร
                </button>
                <button class="nav-link" data-target="settings">
                    <span class="icon">🔧</span> ตั้งค่าเพิ่มเติม
                </button>
            </div>
        </div>

        <div class="sidebar-footer">
            © <span id="year"></span> โรงเรียนวัดสังเวช<br />
            เวอร์ชันตัวอย่างสำหรับพัฒนาเพิ่มเติม
        </div>
    </aside>

    <!-- MAIN -->
    <main class="main">
        <header class="topbar">
            <div class="topbar-title" id="sectionTitle">แดชบอร์ดภาพรวม</div>
            <div class="topbar-right">
                <span class="badge">Demo Prototype</span>
                <span>สถานะ: <strong>ทดสอบระบบ</strong></span>
            </div>
        </header>

        <section class="content">
            <!-- DASHBOARD -->
            <section id="dashboard" class="card">
                <div class="card-header">
                    <div>
                        <div class="card-title">แดชบอร์ดภาพรวมพัสดุ</div>
                        <div class="card-subtitle">สรุปปริมาณพัสดุและคำขอเบิกเบื้องต้น</div>
                    </div>
                </div>

                <div class="kpi-grid" id="kpiGrid">
                    <!-- เติมข้อมูลด้วย JS -->
                </div>

                <div class="grid grid-2" style="margin-top:16px;">
                    <div class="card" style="box-shadow:none;border-style:dashed;">
                        <div class="card-header" style="margin-bottom:6px;">
                            <div class="card-title">รายการพัสดุใกล้ถึงจุดสั่งซื้อ</div>
                        </div>
                        <div class="card-subtitle">
                            แสดงพัสดุที่มีปริมาณน้อยกว่าระดับขั้นต่ำที่กำหนด
                        </div>
                        <div id="lowStockList" style="margin-top:8px;font-size:0.85rem;"></div>
                    </div>

                    <div class="card" style="box-shadow:none;border-style:dashed;">
                        <div class="card-header" style="margin-bottom:6px;">
                            <div class="card-title">สรุปคำขอเบิกล่าสุด</div>
                        </div>
                        <div class="card-subtitle">คำขอที่ถูกบันทึกผ่านระบบ</div>
                        <div id="recentRequests" style="margin-top:8px;font-size:0.85rem;"></div>
                    </div>
                </div>
            </section>

            <!-- INVENTORY -->
            <section id="inventory" class="card" style="display:none;">
                <div class="card-header">
                    <div>
                        <div class="card-title">รายการพัสดุ (แยกตามหมวดหมู่)</div>
                        <div class="card-subtitle">ดูรายการพัสดุทั้งหมด พร้อมหมวดหมู่และสถานะสต็อก</div>
                    </div>
                </div>

                <div class="filter-row">
                    <label for="categoryFilter">หมวดหมู่:</label>
                    <select id="categoryFilter">
                        <option value="all">ทั้งหมด</option>
                    </select>
                    <span class="muted">คลิกหัวตารางเพื่อจัดเรียงได้ (ตัวอย่าง)</span>
                </div>

                <div style="overflow-x:auto;">
                    <table id="inventoryTable">
                        <thead>
                        <tr>
                            <th>รหัส</th>
                            <th>รายการพัสดุ</th>
                            <th>หมวดหมู่</th>
                            <th>หน่วย</th>
                            <th>คงเหลือ</th>
                            <th>ขั้นต่ำ</th>
                            <th>สถานะ</th>
                        </tr>
                        </thead>
                        <tbody>
                        <!-- เติมด้วย JS -->
                        </tbody>
                    </table>
                </div>
            </section>

            <!-- REQUEST FORM -->
            <section id="request" class="card" style="display:none;">
                <div class="card-header">
                    <div>
                        <div class="card-title">แบบฟอร์มขอเบิกพัสดุ</div>
                        <div class="card-subtitle">สำหรับบุคลากรภายในโรงเรียนวัดสังเวช</div>
                    </div>
                </div>

                <form id="requestForm">
                    <div class="form-grid form-grid-2">
                        <div>
                            <label for="requestStaff">ผู้ขอเบิก</label>
                            <select id="requestStaff" required></select>
                        </div>
                        <div>
                            <label for="requestDepartment">กลุ่มงาน / ฝ่าย</label>
                            <input id="requestDepartment" type="text" placeholder="เช่น งานวิชาการ, งานธุรการ" required />
                        </div>
                        <div>
                            <label for="requestItem">รายการพัสดุ</label>
                            <select id="requestItem" required></select>
                        </div>
                        <div>
                            <label for="requestQty">จำนวนที่ขอเบิก</label>
                            <input id="requestQty" type="number" min="1" required />
                        </div>
                        <div>
                            <label for="requestDate">วันที่ขอเบิก</label>
                            <input id="requestDate" type="date" required />
                        </div>
                        <div>
                            <label for="requestRemark">วัตถุประสงค์ / หมายเหตุ</label>
                            <textarea id="requestRemark" placeholder="ระบุรายละเอียดเพิ่มเติม (ถ้ามี)"></textarea>
                        </div>
                    </div>
                    <div style="margin-top:12px;display:flex;gap:8px;align-items:center;">
                        <button type="submit" class="btn btn-primary">
                            ✅ บันทึกคำขอเบิก
                        </button>
                        <span class="muted">เมื่อบันทึกแล้ว ระบบจะตัดสต็อก (ตัวอย่างใน Demo)</span>
                    </div>
                </form>
            </section>

            <!-- REPORTS -->
            <section id="reports" class="card" style="display:none;">
                <div class="card-header">
                    <div>
                        <div class="card-title">เมนูพิมพ์รายงาน</div>
                        <div class="card-subtitle">เลือกรูปแบบรายงาน และใช้คำสั่งพิมพ์ของเบราว์เซอร์</div>
                    </div>
                    <button class="btn btn-outline" id="btnPrint">
                        🖨️ พิมพ์ (Ctrl + P)
                    </button>
                </div>

                <div class="form-grid form-grid-2">
                    <div>
                        <label for="reportType">ประเภทรายงาน</label>
                        <select id="reportType">
                            <option value="stock">รายงานคงคลังพัสดุ</option>
                            <option value="low">พัสดุใกล้หมด / ต่ำกว่าขั้นต่ำ</option>
                            <option value="history">ประวัติการขอเบิก (ล่าสุด)</option>
                        </select>
                    </div>
                    <div>
                        <label>ช่วงเวลา (ตัวอย่างการกรอง)</label>
                        <div style="display:flex;gap:4px;">
                            <input type="date" id="reportFrom" />
                            <input type="date" id="reportTo" />
                        </div>
                        <div class="print-hint">
                            หากไม่ระบุวันที่ ระบบจะแสดงข้อมูลทั้งหมดตามประเภทที่เลือก
                        </div>
                    </div>
                </div>

                <div class="card" style="margin-top:12px;box-shadow:none;border-style:dashed;">
                    <div class="card-header" style="margin-bottom:4px;">
                        <div class="card-title" style="font-size:0.95rem;">ตัวอย่างหน้ารายงาน</div>
                    </div>
                    <div id="reportPreview" style="font-size:0.85rem;">
                        <!-- สร้างตัวอย่างรายงานด้วย JS -->
                    </div>
                </div>
            </section>

            <!-- MANAGE ITEMS -->
            <section id="manageItems" class="card" style="display:none;">
                <div class="card-header">
                    <div>
                        <div class="card-title">จัดการรายการพัสดุ</div>
                        <div class="card-subtitle">เพิ่ม-ลบรายการ และกำหนดจุดสั่งซื้อขั้นต่ำ</div>
                    </div>
                </div>

                <div class="grid grid-2">
                    <div>
                        <form id="itemForm">
                            <div class="form-grid">
                                <div>
                                    <label for="itemCode">รหัสพัสดุ</label>
                                    <input id="itemCode" required />
                                </div>
                                <div>
                                    <label for="itemName">ชื่อรายการพัสดุ</label>
                                    <input id="itemName" required />
                                </div>
                                <div>
                                    <label for="itemCategory">หมวดหมู่</label>
                                    <input id="itemCategory" placeholder="เช่น เครื่องเขียน, ทำความสะอาด" required />
                                </div>
                                <div>
                                    <label for="itemUnit">หน่วยนับ</label>
                                    <input id="itemUnit" placeholder="เช่น กล่อง, แพ็ค, ชิ้น" required />
                                </div>
                                <div>
                                    <label for="itemQty">จำนวนคงเหลือเริ่มต้น</label>
                                    <input id="itemQty" type="number" min="0" required />
                                </div>
                                <div>
                                    <label for="itemMin">ระดับขั้นต่ำ</label>
                                    <input id="itemMin" type="number" min="0" required />
                                </div>
                            </div>
                            <div style="margin-top:10px;">
                                <button type="submit" class="btn btn-primary">➕ เพิ่มรายการพัสดุ</button>
                            </div>
                        </form>
                    </div>
                    <div>
                        <div class="card-subtitle" style="margin-bottom:4px;">รายการพัสดุทั้งหมด</div>
                        <div style="overflow-x:auto;">
                            <table id="manageItemsTable">
                                <thead>
                                <tr>
                                    <th>รหัส</th>
                                    <th>ชื่อรายการ</th>
                                    <th>หมวดหมู่</th>
                                    <th>คงเหลือ</th>
                                    <th>จัดการ</th>
                                </tr>
                                </thead>
                                <tbody>
                                <!-- JS เติม -->
                                </tbody>
                            </table>
                        </div>
                        <div class="muted" style="margin-top:4px;">
                            * การลบรายการใน Demo นี้จะลบออกจากหน่วยความจำบนหน้าเว็บเท่านั้น
                        </div>
                    </div>
                </div>
            </section>

            <!-- MANAGE STAFF -->
            <section id="manageStaff" class="card" style="display:none;">
                <div class="card-header">
                    <div>
                        <div class="card-title">จัดการข้อมูลบุคลากร</div>
                        <div class="card-subtitle">เพิ่ม-ลบ-แก้ไขข้อมูลบุคลากรภายในโรงเรียน</div>
                    </div>
                </div>

                <div class="grid grid-2">
                    <div>
                        <form id="staffForm">
                            <input type="hidden" id="staffIdEditing" />
                            <div class="form-grid">
                                <div>
                                    <label for="staffName">ชื่อ-สกุล</label>
                                    <input id="staffName" required />
                                </div>
                                <div>
                                    <label for="staffPosition">ตำแหน่ง</label>
                                    <input id="staffPosition" placeholder="เช่น ครู, เจ้าหน้าที่ธุรการ" required />
                                </div>
                                <div>
                                    <label for="staffDept">กลุ่มงาน / ฝ่าย</label>
                                    <input id="staffDept" placeholder="เช่น งานวิชาการ, งานบุคคล" required />
                                </div>
                                <div>
                                    <label for="staffCode">รหัสบุคลากร / Username</label>
                                    <input id="staffCode" required />
                                </div>
                            </div>
                            <div style="margin-top:10px;display:flex;gap:6px;">
                                <button type="submit" class="btn btn-primary" id="btnSaveStaff">
                                    💾 บันทึกข้อมูล
                                </button>
                                <button type="button" class="btn btn-outline" id="btnCancelEditStaff" style="display:none;">
                                    ❌ ยกเลิกแก้ไข
                                </button>
                            </div>
                        </form>
                    </div>
                    <div>
                        <div class="card-subtitle" style="margin-bottom:4px;">รายชื่อบุคลากร</div>
                        <div style="overflow-x:auto;">
                            <table id="staffTable">
                                <thead>
                                <tr>
                                    <th>ชื่อ-สกุล</th>
                                    <th>ตำแหน่ง</th>
                                    <th>กลุ่มงาน</th>
                                    <th>รหัส / Username</th>
                                    <th>จัดการ</th>
                                </tr>
                                </thead>
                                <tbody>
                                <!-- JS เติม -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </section>

            <!-- SETTINGS / EXTRA -->
            <section id="settings" class="card" style="display:none;">
                <div class="card-header">
                    <div>
                        <div class="card-title">ตั้งค่าเพิ่มเติม (แนวคิดระบบจริง)</div>
                        <div class="card-subtitle">
                            ส่วนนี้สำหรับออกแบบการเชื่อมต่อฐานข้อมูล, สิทธิ์การใช้งาน, การล็อกอิน ฯลฯ
                        </div>
                    </div>
                </div>

                <ul style="font-size:0.9rem;line-height:1.6;">
                    <li>กำหนดสิทธิ์ผู้ใช้: ผู้ดูแลระบบ / เจ้าหน้าที่พัสดุ / บุคลากรทั่วไป</li>
                    <li>เชื่อมต่อฐานข้อมูลจริง (เช่น MySQL, PostgreSQL) แทนข้อมูลตัวอย่างในหน้านี้</li>
                    <li>บันทึกประวัติการทำรายการทุกครั้ง เพื่อใช้ตรวจสอบย้อนหลัง</li>
                    <li>รองรับการนำเข้าข้อมูลจากไฟล์ Excel / CSV</li>
                    <li>เชื่อมต่อระบบล็อกอินของโรงเรียน (Single Sign-On) หากมี</li>
                </ul>
                <p class="muted">
                    * โค้ดชุดนี้เป็นตัวอย่าง Front-End สามารถนำไปต่อยอดพัฒนาเป็นระบบเต็มรูปแบบ
                    (เชื่อมกับ Back-End / API / Database) ได้ตามต้องการ
                </p>
            </section>
        </section>
    </main>
</div>

<script>
    // ข้อมูลตัวอย่างเบื้องต้น
    let items = [
        { id: 1, code: "ST-001", name: "ดินสอดำ 2B", category: "เครื่องเขียน", unit: "แท่ง", qty: 120, min: 50 },
        { id: 2, code: "ST-002", name: "ปากกาน้ำเงิน", category: "เครื่องเขียน", unit: "ด้าม", qty: 45, min: 50 },
        { id: 3, code: "PP-001", name: "กระดาษ A4 80 แกรม", category: "งานพิมพ์", unit: "รีม", qty: 15, min: 10 },
        { id: 4, code: "CL-001", name: "น้ำยาถูพื้น", category: "ทำความสะอาด", unit: "แกลลอน", qty: 8, min: 5 },
        { id: 5, code: "IT-001", name: "สาย HDMI", category: "อุปกรณ์ไอที", unit: "เส้น", qty: 6, min: 3 }
    ];

    let staff = [
        { id: 1, name: "ครูสมชาย ใจดี", position: "ครูผู้สอน", department: "งานวิชาการ", code: "T001" },
        { id: 2, name: "ครูสมหญิง สายทอง", position: "ครูผู้สอน", department: "งานวิชาการ", code: "T002" },
        { id: 3, name: "นางสาววิภา พัสดุ", position: "เจ้าหน้าที่พัสดุ", department: "งานธุรการ", code: "A001" }
    ];

    let requests = [];

    // === Navigation ===
    const navLinks = document.querySelectorAll(".nav-link");
    const sections = document.querySelectorAll("section.card");
    const sectionTitle = document.getElementById("sectionTitle");

    navLinks.forEach(btn => {
        btn.addEventListener("click", () => {
            navLinks.forEach(b => b.classList.remove("active"));
            btn.classList.add("active");
            const target = btn.getAttribute("data-target");
            sections.forEach(sec => {
                sec.style.display = (sec.id === target) ? "block" : "none";
            });
            sectionTitle.textContent = btn.textContent.trim();
        });
    });

    // ปีปัจจุบัน
    document.getElementById("year").textContent = new Date().getFullYear();

    // === Inventory Rendering ===
    const categoryFilter = document.getElementById("categoryFilter");
    const inventoryTableBody = document.querySelector("#inventoryTable tbody");

    function getCategories() {
        return [...new Set(items.map(i => i.category))];
    }

    function isLowStock(item) {
        return item.qty <= item.min;
    }

    function renderCategoryFilter() {
        const categories = getCategories();
        categoryFilter.innerHTML = '<option value="all">ทั้งหมด</option>';
        categories.forEach(cat => {
            const opt = document.createElement("option");
            opt.value = cat;
            opt.textContent = cat;
            categoryFilter.appendChild(opt);
        });
    }

    function renderInventoryTable() {
        const selectedCat = categoryFilter.value || "all";
        inventoryTableBody.innerHTML = "";
        items.forEach(item => {
            if (selectedCat !== "all" && item.category !== selectedCat) return;
            const tr = document.createElement("tr");
            tr.innerHTML = `
                <td>${item.code}</td>
                <td>${item.name}</td>
                <td><span class="pill">${item.category}</span></td>
                <td>${item.unit}</td>
                <td>${item.qty}</td>
                <td>${item.min}</td>
                <td><span class="tag ${isLowStock(item) ? "low" : "ok"}">
                    ${isLowStock(item) ? "ต่ำกว่าขั้นต่ำ" : "ปกติ"}
                </span></td>
            `;
            inventoryTableBody.appendChild(tr);
        });
    }

    categoryFilter.addEventListener("change", renderInventoryTable);

    // === Request Form ===
    const requestStaffSelect = document.getElementById("requestStaff");
    const requestItemSelect = document.getElementById("requestItem");
    const requestForm = document.getElementById("requestForm");

    function renderStaffOptions() {
        requestStaffSelect.innerHTML = '<option value="">เลือกผู้ขอเบิก</option>';
        staff.forEach(s => {
            const opt = document.createElement("option");
            opt.value = s.id;
            opt.textContent = `${s.name} (${s.department})`;
            requestStaffSelect.appendChild(opt);
        });
    }

    function renderItemOptions() {
        requestItemSelect.innerHTML = '<option value="">เลือกรายการพัสดุ</option>';
        items.forEach(i => {
            const opt = document.createElement("option");
            opt.value = i.id;
            opt.textContent = `${i.name} [${i.category}] (คงเหลือ ${i.qty} ${i.unit})`;
            requestItemSelect.appendChild(opt);
        });
    }

    requestForm.addEventListener("submit", e => {
        e.preventDefault();
        const staffId = parseInt(requestStaffSelect.value);
        const staffObj = staff.find(s => s.id === staffId);
        const itemId = parseInt(requestItemSelect.value);
        const itemObj = items.find(i => i.id === itemId);
        const qty = parseInt(document.getElementById("requestQty").value);
        const department = document.getElementById("requestDepartment").value.trim();
        const date = document.getElementById("requestDate").value;
        const remark = document.getElementById("requestRemark").value.trim();

        if (!staffObj || !itemObj || !qty || qty <= 0) {
            alert("กรุณากรอกข้อมูลให้ครบถ้วน");
            return;
        }
        if (qty > itemObj.qty) {
            if (!confirm("จำนวนที่ขอเบิกมากกว่าคงเหลือ ต้องการดำเนินการต่อหรือไม่? (Demo)")) {
                return;
            }
        }

        const request = {
            id: Date.now(),
            staffName: staffObj.name,
            staffDepartment: department || staffObj.department,
            itemName: itemObj.name,
            itemId: itemObj.id,
            qty,
            date,
            remark
        };
        requests.unshift(request);

        // ตัดสต็อก (Demo)
        itemObj.qty = Math.max(0, itemObj.qty - qty);

        alert("บันทึกคำขอเบิกเรียบร้อย (Demo)");
        requestForm.reset();
        document.getElementById("requestDate").valueAsDate = new Date();

        // อัปเดตส่วนต่าง ๆ
        renderInventoryTable();
        renderItemOptions();
        renderDashboard();
        renderReportPreview();
    });

    // ตั้งค่า default วันที่
    document.getElementById("requestDate").valueAsDate = new Date();

    // === Dashboard ===
    const kpiGrid = document.getElementById("kpiGrid");
    const lowStockList = document.getElementById("lowStockList");
    const recentRequestsDiv = document.getElementById("recentRequests");

    function renderDashboard() {
        const totalItems = items.length;
        const totalQty = items.reduce((sum, i) => sum + i.qty, 0);
        const lowCount = items.filter(isLowStock).length;
        const requestCount = requests.length;

        kpiGrid.innerHTML = "";
        const kpis = [
            { label: "จำนวนรายการพัสดุทั้งหมด", value: totalItems, caption: "รายการ" },
            { label: "จำนวนพัสดุคงเหลือรวม", value: totalQty, caption: "ตามหน่วยนับ" },
            { label: "รายการที่ต่ำกว่าขั้นต่ำ", value: lowCount, caption: "ควรพิจารณาจัดซื้อ" },
            { label: "จำนวนคำขอเบิก (ในระบบ)", value: requestCount, caption: "นับจากการบันทึกใน Demo" }
        ];

        kpis.forEach((k, idx) => {
            const div = document.createElement("div");
            div.className = "kpi-card";
            const percent = totalItems ? Math.min(100, (k.value / (idx === 1 ? totalQty || 1 : totalItems || 1)) * 100) : 0;
            div.innerHTML = `
                <div class="kpi-label">${k.label}</div>
                <div class="kpi-value">${k.value.toLocaleString()}</div>
                <div class="kpi-caption">${k.caption}</div>
                <div class="progress-bar">
                    <div class="progress-inner" style="width:${Math.max(8, percent)}%;"></div>
                </div>
            `;
            kpiGrid.appendChild(div);
        });

        // Low stock list
        const lows = items.filter(isLowStock);
        if (lows.length === 0) {
            lowStockList.innerHTML = `<span class="muted">ยังไม่มีรายการที่ต่ำกว่าขั้นต่ำ</span>`;
        } else {
            const ul = document.createElement("ul");
            ul.style.paddingLeft = "18px";
            lows.forEach(i => {
                const li = document.createElement("li");
                li.innerHTML = `
                    <strong>${i.name}</strong> (${i.category}) - คงเหลือ ${i.qty} ${i.unit}
                    <span class="muted"> | ขั้นต่ำ ${i.min}</span>
                `;
                ul.appendChild(li);
            });
            lowStockList.innerHTML = "";
            lowStockList.appendChild(ul);
        }

        // Recent requests
        if (requests.length === 0) {
            recentRequestsDiv.innerHTML = `<span class="muted">ยังไม่มีคำขอเบิกที่บันทึกในระบบ</span>`;
        } else {
            const ul = document.createElement("ul");
            ul.style.paddingLeft = "18px";
            requests.slice(0, 5).forEach(r => {
                const li = document.createElement("li");
                li.innerHTML = `
                    <strong>${r.staffName}</strong> ขอเบิก <strong>${r.itemName}</strong>
                    จำนวน ${r.qty} ชิ้น วันที่ ${r.date || "-"}
                    <div class="muted">${r.remark || ""}</div>
                `;
                ul.appendChild(li);
            });
            recentRequestsDiv.innerHTML = "";
            recentRequestsDiv.appendChild(ul);
        }
    }

    // === Manage Items ===
    const itemForm = document.getElementById("itemForm");
    const manageItemsTableBody = document.querySelector("#manageItemsTable tbody");

    itemForm.addEventListener("submit", e => {
        e.preventDefault();
        const code = document.getElementById("itemCode").value.trim();
        const name = document.getElementById("itemName").value.trim();
        const category = document.getElementById("itemCategory").value.trim();
        const unit = document.getElementById("itemUnit").value.trim();
        const qty = parseInt(document.getElementById("itemQty").value);
        const min = parseInt(document.getElementById("itemMin").value);

        if (!code || !name || !category || !unit) {
            alert("กรุณากรอกข้อมูลให้ครบ");
            return;
        }

        items.push({
            id: Date.now(),
            code,
            name,
            category,
            unit,
            qty: isNaN(qty) ? 0 : qty,
            min: isNaN(min) ? 0 : min
        });

        alert("เพิ่มรายการพัสดุเรียบร้อย (Demo)");
        itemForm.reset();
        renderInventoryTable();
        renderCategoryFilter();
        renderItemOptions();
        renderManageItemsTable();
        renderDashboard();
        renderReportPreview();
    });

    function renderManageItemsTable() {
        manageItemsTableBody.innerHTML = "";
        items.forEach(item => {
            const tr = document.createElement("tr");
            tr.innerHTML = `
                <td>${item.code}</td>
                <td>${item.name}</td>
                <td>${item.category}</td>
                <td>${item.qty}</td>
                <td>
                    <div class="actions">
                        <button class="btn btn-xs btn-danger" data-delete-item="${item.id}">ลบ</button>
                    </div>
                </td>
            `;
            manageItemsTableBody.appendChild(tr);
        });
    }

    manageItemsTableBody.addEventListener("click", e => {
        const btn = e.target.closest("[data-delete-item]");
        if (!btn) return;
        const id = parseInt(btn.getAttribute("data-delete-item"));
        if (confirm("ต้องการลบรายการนี้หรือไม่?")) {
            items = items.filter(i => i.id !== id);
            renderInventoryTable();
            renderCategoryFilter();
            renderItemOptions();
            renderManageItemsTable();
            renderDashboard();
            renderReportPreview();
        }
    });

    // === Manage Staff ===
    const staffForm = document.getElementById("staffForm");
    const staffTableBody = document.querySelector("#staffTable tbody");
    const staffIdEditing = document.getElementById("staffIdEditing");
    const btnSaveStaff = document.getElementById("btnSaveStaff");
    const btnCancelEditStaff = document.getElementById("btnCancelEditStaff");

    function renderStaffTable() {
        staffTableBody.innerHTML = "";
        staff.forEach(s => {
            const tr = document.createElement("tr");
            tr.innerHTML = `
                <td>${s.name}</td>
                <td>${s.position}</td>
                <td>${s.department}</td>
                <td>${s.code}</td>
                <td>
                    <div class="actions">
                        <button class="btn btn-xs btn-outline" data-edit-staff="${s.id}">แก้ไข</button>
                        <button class="btn btn-xs btn-danger" data-delete-staff="${s.id}">ลบ</button>
                    </div>
                </td>
            `;
            staffTableBody.appendChild(tr);
        });
    }

    staffTableBody.addEventListener("click", e => {
        const editBtn = e.target.closest("[data-edit-staff]");
        const deleteBtn = e.target.closest("[data-delete-staff]");
        if (editBtn) {
            const id = parseInt(editBtn.getAttribute("data-edit-staff"));
            const s = staff.find(x => x.id === id);
            if (!s) return;
            staffIdEditing.value = s.id;
            document.getElementById("staffName").value = s.name;
            document.getElementById("staffPosition").value = s.position;
            document.getElementById("staffDept").value = s.department;
            document.getElementById("staffCode").value = s.code;
            btnSaveStaff.textContent = "💾 บันทึกการแก้ไข";
            btnCancelEditStaff.style.display = "inline-flex";
        }
        if (deleteBtn) {
            const id = parseInt(deleteBtn.getAttribute("data-delete-staff"));
            if (confirm("ต้องการลบบุคลากรคนนี้หรือไม่?")) {
                staff = staff.filter(x => x.id !== id);
                renderStaffTable();
                renderStaffOptions();
            }
        }
    });

    staffForm.addEventListener("submit", e => {
        e.preventDefault();
        const idEditing = staffIdEditing.value;
        const name = document.getElementById("staffName").value.trim();
        const position = document.getElementById("staffPosition").value.trim();
        const department = document.getElementById("staffDept").value.trim();
        const code = document.getElementById("staffCode").value.trim();

        if (!name || !position || !department || !code) {
            alert("กรุณากรอกข้อมูลบุคลากรให้ครบ");
            return;
        }

        if (idEditing) {
            // แก้ไข
            const s = staff.find(x => x.id === parseInt(idEditing));
            if (s) {
                s.name = name;
                s.position = position;
                s.department = department;
                s.code = code;
            }
            alert("แก้ไขข้อมูลบุคลากรเรียบร้อย");
        } else {
            // เพิ่มใหม่
            staff.push({
                id: Date.now(),
                name,
                position,
                department,
                code
            });
            alert("เพิ่มบุคลากรเรียบร้อย");
        }

        staffForm.reset();
        staffIdEditing.value = "";
        btnSaveStaff.textContent = "💾 บันทึกข้อมูล";
        btnCancelEditStaff.style.display = "none";

        renderStaffTable();
        renderStaffOptions();
    });

    btnCancelEditStaff.addEventListener("click", () => {
        staffForm.reset();
        staffIdEditing.value = "";
        btnSaveStaff.textContent = "💾 บันทึกข้อมูล";
        btnCancelEditStaff.style.display = "none";
    });

    // === Reports ===
    const reportTypeSelect = document.getElementById("reportType");
    const reportPreview = document.getElementById("reportPreview");
    const btnPrint = document.getElementById("btnPrint");

    function renderReportPreview() {
        const type = reportTypeSelect.value;
        let html = "";

        if (type === "stock") {
            html += `<h3>รายงานคงคลังพัสดุ (ตัวอย่าง)</h3>`;
            html += `<p class="muted">โรงเรียนวัดสังเวช</p>`;
            html += `<table style="width:100%;border-collapse:collapse;font-size:0.8rem;margin-top:8px;">`;
            html += `
                <thead>
                    <tr>
                        <th style="border-bottom:1px solid #ccc;padding:4px 2px;text-align:left;">รหัส</th>
                        <th style="border-bottom:1px solid #ccc;padding:4px 2px;text-align:left;">รายการ</th>
                        <th style="border-bottom:1px solid #ccc;padding:4px 2px;text-align:left;">หมวดหมู่</th>
                        <th style="border-bottom:1px solid #ccc;padding:4px 2px;text-align:right;">คงเหลือ</th>
                        <th style="border-bottom:1px solid #ccc;padding:4px 2px;text-align:right;">ขั้นต่ำ</th>
                    </tr>
                </thead><tbody>
            `;
            items.forEach(i => {
                html += `
                    <tr>
                        <td style="border-bottom:1px solid #eee;padding:4px 2px;">${i.code}</td>
                        <td style="border-bottom:1px solid #eee;padding:4px 2px;">${i.name}</td>
                        <td style="border-bottom:1px solid #eee;padding:4px 2px;">${i.category}</td>
                        <td style="border-bottom:1px solid #eee;padding:4px 2px;text-align:right;">${i.qty}</td>
                        <td style="border-bottom:1px solid #eee;padding:4px 2px;text-align:right;">${i.min}</td>
                    </tr>
                `;
            });
            html += `</tbody></table>`;
        } else if (type === "low") {
            html += `<h3>รายงานพัสดุใกล้หมด / ต่ำกว่าขั้นต่ำ</h3>`;
            const lows = items.filter(isLowStock);
            if (lows.length === 0) {
                html += `<p class="muted">ไม่พบรายการที่ต่ำกว่าขั้นต่ำ</p>`;
            } else {
                html += `<ul style="font-size:0.85rem;">`;
                lows.forEach(i => {
                    html += `<li><strong>${i.name}</strong> (${i.category}) คงเหลือ ${i.qty} ${i.unit} ขั้นต่ำ ${i.min}</li>`;
                });
                html += `</ul>`;
            }
        } else if (type === "history") {
            html += `<h3>ประวัติการขอเบิก (ล่าสุด)</h3>`;
            if (requests.length === 0) {
                html += `<p class="muted">ยังไม่มีข้อมูลคำขอเบิก</p>`;
            } else {
                html += `<table style="width:100%;border-collapse:collapse;font-size:0.8rem;margin-top:8px;">`;
                html += `
                    <thead>
                        <tr>
                            <th style="border-bottom:1px solid #ccc;padding:4px 2px;text-align:left;">วันที่</th>
                            <th style="border-bottom:1px solid #ccc;padding:4px 2px;text-align:left;">ผู้ขอเบิก</th>
                            <th style="border-bottom:1px solid #ccc;padding:4px 2px;text-align:left;">รายการพัสดุ</th>
                            <th style="border-bottom:1px solid #ccc;padding:4px 2px;text-align:right;">จำนวน</th>
                        </tr>
                    </thead><tbody>
                `;
                requests.slice(0, 20).forEach(r => {
                    html += `
                        <tr>
                            <td style="border-bottom:1px solid #eee;padding:4px 2px;">${r.date || "-"}</td>
                            <td style="border-bottom:1px solid #eee;padding:4px 2px;">${r.staffName}</td>
                            <td style="border-bottom:1px solid #eee;padding:4px 2px;">${r.itemName}</td>
                            <td style="border-bottom:1px solid #eee;padding:4px 2px;text-align:right;">${r.qty}</td>
                        </tr>
                    `;
                });
                html += `</tbody></table>`;
            }
        }

        reportPreview.innerHTML = html;
    }

    reportTypeSelect.addEventListener("change", renderReportPreview);
    btnPrint.addEventListener("click", () => window.print());

    // === Initial Render ===
    function init() {
        renderCategoryFilter();
        renderInventoryTable();
        renderStaffOptions();
        renderItemOptions();
        renderDashboard();
        renderManageItemsTable();
        renderStaffTable();
        renderReportPreview();
    }

    init();
</script>
</body>
</html>
