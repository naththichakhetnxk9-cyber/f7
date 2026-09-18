<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Adaptive Assessment & Learning Analytics Platform</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- FontAwesome CDN -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter & Sarabun -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Sarabun:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f0fdf4',
                            100: '#dcfce7',
                            500: '#22c55e',
                            600: '#16a34a',
                            700: '#15803d',
                        },
                        accent: {
                            50: '#eff6ff',
                            500: '#3b82f6',
                            600: '#2563eb',
                        }
                    },
                    fontFamily: {
                        sans: ['Sarabun', 'Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Sarabun', 'Inter', sans-serif;
            background-color: #f8fafc;
        }
        .tab-active {
            border-bottom: 3px solid #2563eb;
            color: #2563eb;
            font-weight: 600;
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
    </style>
</head>
<body class="text-slate-800 antialiased flex flex-col min-h-screen">

    <!-- Navigation Header -->
    <header class="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-16">
                <!-- Logo & Title -->
                <div class="flex items-center space-x-3">
                    <div class="p-2.5 bg-gradient-to-tr from-blue-600 to-indigo-600 rounded-xl text-white shadow-md">
                        <i class="fa-solid fa-brain text-xl"></i>
                    </div>
                    <div>
                        <h1 class="text-lg font-bold text-slate-900 leading-tight">Smart Adaptive Assessment</h1>
                        <p class="text-xs text-slate-500 font-medium hidden sm:block">Learning Analytics & Evaluation Platform (ยุคดิจิทัล)</p>
                    </div>
                </div>

                <!-- Right Menu User Badge -->
                <div class="flex items-center space-x-4">
                    <div class="hidden md:flex items-center bg-slate-100 rounded-lg p-1 text-xs font-medium">
                        <span class="px-2.5 py-1 bg-white text-slate-800 rounded-md shadow-sm">ปีการศึกษา 2569</span>
                        <span class="px-2.5 py-1 text-slate-500">ห้อง ม.4/1 (40 คน)</span>
                    </div>
                    <div class="flex items-center space-x-2 border-l border-slate-200 pl-4">
                        <div class="w-9 h-9 rounded-full bg-blue-100 border border-blue-300 flex items-center justify-center text-blue-700 font-bold text-sm">
                            ครู
                        </div>
                        <div class="hidden lg:block text-left">
                            <div class="text-xs font-semibold text-slate-800">อ.สมศักดิ์ นวัตกรรม</div>
                            <div class="text-[10px] text-slate-500">ครูผู้สอน / แอดมิน</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Navigation View Switcher Tabs -->
        <div class="bg-slate-50 border-t border-slate-200 px-4 sm:px-6 lg:px-8">
            <div class="max-w-7xl mx-auto flex space-x-8 text-sm overflow-x-auto">
                <button onclick="switchTab('teacher')" id="tab-teacher" class="py-3 px-2 flex items-center space-x-2 tab-active whitespace-nowrap transition-colors">
                    <i class="fa-solid fa-chart-line text-base"></i>
                    <span>Teacher Dashboard (สำหรับครู)</span>
                    <span class="ml-1 bg-blue-100 text-blue-700 text-xs px-2 py-0.5 rounded-full font-bold">40 คน</span>
                </button>
                <button onclick="switchTab('student')" id="tab-student" class="py-3 px-2 flex items-center space-x-2 text-slate-500 hover:text-slate-700 whitespace-nowrap transition-colors">
                    <i class="fa-solid fa-user-graduate text-base"></i>
                    <span>Student Dashboard (รายบุคคล)</span>
                </button>
                <button onclick="switchTab('simulator')" id="tab-simulator" class="py-3 px-2 flex items-center space-x-2 text-slate-500 hover:text-slate-700 whitespace-nowrap transition-colors">
                    <i class="fa-solid fa-sliders text-base"></i>
                    <span>Adaptive Quiz Simulator (ทดลองสอบ)</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content Container -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6">

        <!-- ========================================== -->
        <!-- 1. TEACHER DASHBOARD VIEW -->
        <!-- ========================================== -->
        <div id="view-teacher" class="space-y-6">
            
            <!-- Summary KPI Cards -->
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                <!-- Total Students -->
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex items-center justify-between">
                    <div>
                        <p class="text-xs font-semibold text-slate-500 uppercase tracking-wider">นักเรียนทั้งหมด</p>
                        <h3 class="text-3xl font-extrabold text-slate-900 mt-1">40 <span class="text-base font-normal text-slate-500">คน</span></h3>
                        <p class="text-xs text-slate-500 mt-1"><i class="fa-solid fa-users text-blue-500"></i> ห้องเรียน ม.4/1</p>
                    </div>
                    <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-xl flex items-center justify-center text-xl">
                        <i class="fa-solid fa-graduation-cap"></i>
                    </div>
                </div>

                <!-- Passed Threshold -->
                <div class="bg-white p-5 rounded-2xl border border-emerald-200 bg-emerald-50/20 shadow-sm flex items-center justify-between">
                    <div>
                        <p class="text-xs font-semibold text-emerald-600 uppercase tracking-wider">ผ่านเกณฑ์การประเมิน</p>
                        <h3 class="text-3xl font-extrabold text-emerald-600 mt-1">32 <span class="text-base font-normal text-emerald-600">คน</span></h3>
                        <p class="text-xs text-emerald-600 font-medium mt-1"><i class="fa-solid fa-circle-check"></i> คิดเป็น 80.0% ของห้อง</p>
                    </div>
                    <div class="w-12 h-12 bg-emerald-100 text-emerald-600 rounded-xl flex items-center justify-center text-xl">
                        <i class="fa-solid fa-circle-check"></i>
                    </div>
                </div>

                <!-- Needs Remediation -->
                <div class="bg-white p-5 rounded-2xl border border-rose-200 bg-rose-50/20 shadow-sm flex items-center justify-between">
                    <div>
                        <p class="text-xs font-semibold text-rose-600 uppercase tracking-wider">ต้องพัฒนา / ซ่อมเสริม</p>
                        <h3 class="text-3xl font-extrabold text-rose-600 mt-1">8 <span class="text-base font-normal text-rose-600">คน</span></h3>
                        <p class="text-xs text-rose-600 font-medium mt-1"><i class="fa-solid fa-triangle-exclamation"></i> คิดเป็น 20.0% ของห้อง</p>
                    </div>
                    <div class="w-12 h-12 bg-rose-100 text-rose-600 rounded-xl flex items-center justify-center text-xl">
                        <i class="fa-solid fa-user-ninja"></i>
                    </div>
                </div>

                <!-- Class Accuracy Avg -->
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex items-center justify-between">
                    <div>
                        <p class="text-xs font-semibold text-slate-500 uppercase tracking-wider">ความถูกต้องเฉลี่ย</p>
                        <h3 class="text-3xl font-extrabold text-slate-900 mt-1">78.5%</h3>
                        <p class="text-xs text-slate-500 mt-1"><i class="fa-solid fa-clock text-amber-500"></i> เวลาเฉลี่ย 18 นาที/แบบทดสอบ</p>
                    </div>
                    <div class="w-12 h-12 bg-indigo-50 text-indigo-600 rounded-xl flex items-center justify-center text-xl">
                        <i class="fa-solid fa-bullseye"></i>
                    </div>
                </div>
            </div>

            <!-- Action Alert Banner for 8 Students Needs Improvement -->
            <div class="bg-amber-50 border border-amber-200 rounded-2xl p-4 sm:p-5 flex flex-col md:flex-row items-start md:items-center justify-between gap-4">
                <div class="flex items-start space-x-3">
                    <div class="p-2 bg-amber-500 text-white rounded-xl shadow-sm mt-0.5">
                        <i class="fa-solid fa-bell text-lg"></i>
                    </div>
                    <div>
                        <h4 class="text-sm font-bold text-amber-900">แจ้งเตือนระบบวิเคราะห์วิกฤต (Remediation Alert)</h4>
                        <p class="text-xs text-amber-800 mt-0.5">
                            พบนักเรียน <strong class="underline">8 คน</strong> มีคะแนนต่ำกว่าเกณฑ์ 60% และทำข้อสอบสถิติ/สมการผิดซ้ำเกิน 2 ครั้ง ควรจัดกิจกรรมสอนซ่อมเสริมกลุ่มย่อย
                        </p>
                    </div>
                </div>
                <button onclick="filterTable('needs_improvement')" class="bg-amber-600 hover:bg-amber-700 text-white text-xs font-bold px-4 py-2.5 rounded-xl transition shadow-sm whitespace-nowrap self-end md:self-auto">
                    <i class="fa-solid fa-filter mr-1"></i> กรองดู 8 คนนี้ทันที
                </button>
            </div>

            <!-- Charts Section -->
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <!-- Donut Chart: Student Mastery Distribution -->
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex flex-col">
                    <div class="flex justify-between items-center mb-4">
                        <h3 class="text-base font-bold text-slate-800 flex items-center gap-2">
                            <i class="fa-solid fa-chart-pie text-blue-600"></i>
                            สัดส่วนความสำเร็จรายชั้นเรียน
                        </h3>
                    </div>
                    <div class="relative flex-grow flex items-center justify-center min-h-[220px]">
                        <canvas id="masteryPieChart"></canvas>
                    </div>
                    <div class="grid grid-cols-2 gap-2 text-center text-xs mt-4 pt-4 border-t border-slate-100">
                        <div class="bg-emerald-50 p-2 rounded-lg">
                            <span class="block font-bold text-emerald-700">32 คน (80%)</span>
                            <span class="text-slate-500 text-[11px]">เข้าใจดี / ผ่านเกณฑ์</span>
                        </div>
                        <div class="bg-rose-50 p-2 rounded-lg">
                            <span class="block font-bold text-rose-700">8 คน (20%)</span>
                            <span class="text-slate-500 text-[11px]">ต้องได้รับการช่วยเหลือ</span>
                        </div>
                    </div>
                </div>

                <!-- Radar/Bar Chart: Misconception & Topic Weaknesses -->
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm lg:col-span-2 flex flex-col">
                    <div class="flex justify-between items-center mb-4">
                        <div>
                            <h3 class="text-base font-bold text-slate-800 flex items-center gap-2">
                                <i class="fa-solid fa-diagram-project text-indigo-600"></i>
                                วิเคราะห์จุดอ่อนตามหัวข้อ (Topic Mastery & Misconceptions)
                            </h3>
                            <p class="text-xs text-slate-500">แสดงเปอร์เซ็นต์ความเข้าใจเฉลี่ยของทั้งห้องแยกตามตัวชี้วัด</p>
                        </div>
                        <span class="text-xs bg-indigo-50 text-indigo-700 px-2.5 py-1 rounded-full font-medium">4 หัวข้อหลัก</span>
                    </div>
                    <div class="relative flex-grow min-h-[220px]">
                        <canvas id="topicRadarChart"></canvas>
                    </div>
                </div>
            </div>

            <!-- Student Roster Table -->
            <div class="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden">
                <!-- Table Controls Header -->
                <div class="p-5 border-b border-slate-200 flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <h3 class="text-base font-bold text-slate-800">รายชื่อและผลการเรียนรู้นักเรียนทั้งหมด (40 คน)</h3>
                        <p class="text-xs text-slate-500">ข้อมูลอัปเดตแบบ Real-time จากระบบ Adaptive Assessment</p>
                    </div>

                    <!-- Search & Filter Controls -->
                    <div class="flex flex-wrap items-center gap-2">
                        <!-- Search Box -->
                        <div class="relative">
                            <i class="fa-solid fa-magnifying-glass absolute left-3 top-1/2 -translate-y-1/2 text-slate-400 text-xs"></i>
                            <input type="text" id="searchInput" onkeyup="searchStudent()" placeholder="ค้นหาชื่อนักเรียน..." class="pl-8 pr-3 py-1.5 text-xs bg-slate-50 border border-slate-300 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-500 w-40 sm:w-48">
                        </div>

                        <!-- Filter Buttons -->
                        <div class="inline-flex rounded-xl bg-slate-100 p-1 text-xs font-medium">
                            <button onclick="filterTable('all')" id="btn-filter-all" class="px-3 py-1 rounded-lg bg-white shadow-sm text-slate-800 font-bold">ทั้งหมด (40)</button>
                            <button onclick="filterTable('passed')" id="btn-filter-passed" class="px-3 py-1 rounded-lg text-slate-600 hover:text-slate-900">ผ่าน (32)</button>
                            <button onclick="filterTable('needs_improvement')" id="btn-filter-needs" class="px-3 py-1 rounded-lg text-slate-600 hover:text-slate-900">ต้องพัฒนา (8)</button>
                        </div>
                    </div>
                </div>

                <!-- Table Content -->
                <div class="overflow-x-auto custom-scrollbar">
                    <table class="w-full text-left border-collapse text-xs">
                        <thead>
                            <tr class="bg-slate-50 border-b border-slate-200 text-slate-600 font-bold">
                                <th class="p-3.5 pl-5">นักเรียน</th>
                                <th class="p-3.5">คะแนน Adaptive (100)</th>
                                <th class="p-3.5">ความถูกต้อง (Accuracy)</th>
                                <th class="p-3.5">เวลาที่ใช้</th>
                                <th class="p-3.5">จุดอ่อนที่พบ (Weakness)</th>
                                <th class="p-3.5">สถานะ</th>
                                <th class="p-3.5 text-center">จัดการ</th>
                            </tr>
                        </thead>
                        <tbody id="studentTableBody" class="divide-y divide-slate-100">
                            <!-- JS populated rows -->
                        </tbody>
                    </table>
                </div>

                <!-- Table Footer Pagination/Summary -->
                <div class="p-4 bg-slate-50 border-t border-slate-200 flex justify-between items-center text-xs text-slate-500">
                    <span>แสดงข้อมูลนักเรียน <span id="showing-count">40</span> จากทั้งหมด 40 คน</span>
                    <span class="font-medium">เกณฑ์การผ่าน: คะแนน >= 65 และ ความถูกต้อง >= 65%</span>
                </div>
            </div>

        </div>

        <!-- ========================================== -->
        <!-- 2. STUDENT DASHBOARD VIEW -->
        <!-- ========================================== -->
        <div id="view-student" class="space-y-6 hidden">
            
            <!-- Student Header Profile Card -->
            <div class="bg-gradient-to-r from-blue-700 via-indigo-700 to-slate-800 rounded-3xl p-6 text-white shadow-md relative overflow-hidden">
                <div class="absolute -right-10 -bottom-10 w-48 h-48 bg-white/10 rounded-full blur-2xl"></div>
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-6 relative z-10">
                    <div class="flex items-center space-x-4">
                        <div class="w-16 h-16 rounded-2xl bg-white/10 border border-white/20 flex items-center justify-center text-3xl shadow-inner">
                            <i class="fa-solid fa-user-astronaut text-cyan-300"></i>
                        </div>
                        <div>
                            <div class="flex items-center space-x-2">
                                <h2 class="text-xl font-extrabold">นายสมนึก เรียนดี</h2>
                                <span class="bg-emerald-400/20 border border-emerald-400 text-emerald-300 text-[10px] font-bold px-2 py-0.5 rounded-full">กลุ่มพัฒนาดีเด่น</span>
                            </div>
                            <p class="text-xs text-blue-200 mt-1">รหัสนักเรียน: STU-008 | ชั้นมัธยมศึกษาปีที่ 4/1</p>
                            <p class="text-xs text-slate-300 mt-0.5"><i class="fa-solid fa-award text-amber-400 mr-1"></i> Adaptive Ability Score: <strong class="text-white font-bold">78/100 (ระดับกลางสูง - Medium High)</strong></p>
                        </div>
                    </div>

                    <div class="flex items-center gap-3 bg-white/10 p-3 rounded-2xl border border-white/10 backdrop-blur-sm self-start md:self-auto">
                        <div class="text-center px-3 border-r border-white/10">
                            <span class="text-[10px] text-blue-200 uppercase block">แบบทดสอบที่ทำ</span>
                            <span class="text-lg font-bold">12 ชุด</span>
                        </div>
                        <div class="text-center px-3 border-r border-white/10">
                            <span class="text-[10px] text-blue-200 uppercase block">ตอบถูกต้อง</span>
                            <span class="text-lg font-bold text-emerald-300">82%</span>
                        </div>
                        <div class="text-center px-3">
                            <span class="text-[10px] text-blue-200 uppercase block">เหรียญรางวัล</span>
                            <span class="text-lg font-bold text-amber-300"><i class="fa-solid fa-medal"></i> 5</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Student Content Grid -->
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <!-- Personal Learning Skill Radar Chart -->
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex flex-col">
                    <h3 class="text-base font-bold text-slate-800 flex items-center gap-2 mb-2">
                        <i class="fa-solid fa-chart-radar text-blue-600"></i>
                        สมรรถนะการเรียนรู้ส่วนบุคคล
                    </h3>
                    <p class="text-xs text-slate-500 mb-4">ประเมินจากระบบ Adaptive Assessment ล่าสุด</p>
                    <div class="relative flex-grow min-h-[240px]">
                        <canvas id="studentRadarChart"></canvas>
                    </div>
                </div>

                <!-- Strengths & Weaknesses Breakdown -->
                <div class="lg:col-span-2 space-y-4">
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <!-- Strengths Card -->
                        <div class="bg-emerald-50/50 border border-emerald-200 p-5 rounded-2xl shadow-sm">
                            <div class="flex items-center space-x-2 text-emerald-700 font-bold text-sm mb-3">
                                <i class="fa-solid fa-shield-halved text-base"></i>
                                <span>จุดแข็งของคุณ (My Strengths)</span>
                            </div>
                            <ul class="space-y-2 text-xs text-slate-700">
                                <li class="flex items-center justify-between bg-white p-2.5 rounded-xl border border-emerald-100 shadow-2xs">
                                    <span class="flex items-center"><i class="fa-solid fa-check text-emerald-500 mr-2"></i> การคำนวณพีชคณิตเบื้องต้น</span>
                                    <span class="font-bold text-emerald-600">92%</span>
                                </li>
                                <li class="flex items-center justify-between bg-white p-2.5 rounded-xl border border-emerald-100 shadow-2xs">
                                    <span class="flex items-center"><i class="fa-solid fa-check text-emerald-500 mr-2"></i> ความเร็วในการแก้โจทย์พื้นฐาน</span>
                                    <span class="font-bold text-emerald-600">88%</span>
                                </li>
                                <li class="flex items-center justify-between bg-white p-2.5 rounded-xl border border-emerald-100 shadow-2xs">
                                    <span class="flex items-center"><i class="fa-solid fa-check text-emerald-500 mr-2"></i> การวิเคราะห์ตรรกศาสตร์</span>
                                    <span class="font-bold text-emerald-600">80%</span>
                                </li>
                            </ul>
                        </div>

                        <!-- Weaknesses Card -->
                        <div class="bg-rose-50/50 border border-rose-200 p-5 rounded-2xl shadow-sm">
                            <div class="flex items-center space-x-2 text-rose-700 font-bold text-sm mb-3">
                                <i class="fa-solid fa-triangle-exclamation text-base"></i>
                                <span>จุดที่ต้องพัฒนา (My Weaknesses)</span>
                            </div>
                            <ul class="space-y-2 text-xs text-slate-700">
                                <li class="flex items-center justify-between bg-white p-2.5 rounded-xl border border-rose-100 shadow-2xs">
                                    <span class="flex items-center"><i class="fa-solid fa-xmark text-rose-500 mr-2"></i> โจทย์ปัญหาประยุกต์หลายขั้นตอน</span>
                                    <span class="font-bold text-rose-600">54%</span>
                                </li>
                                <li class="flex items-center justify-between bg-white p-2.5 rounded-xl border border-rose-100 shadow-2xs">
                                    <span class="flex items-center"><i class="fa-solid fa-xmark text-rose-500 mr-2"></i> การตีความกราฟและสถิติวิเคราะห์</span>
                                    <span class="font-bold text-rose-600">60%</span>
                                </li>
                            </ul>
                        </div>
                    </div>

                    <!-- Personalized Learning Recommendations -->
                    <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm">
                        <h3 class="text-base font-bold text-slate-800 flex items-center gap-2 mb-3">
                            <i class="fa-solid fa-route text-indigo-600"></i>
                            เส้นทางการเรียนรู้แนะนำสำหรับคุณ (Personalized Learning Path)
                        </h3>
                        
                        <div class="space-y-3">
                            <!-- Module Item 1 -->
                            <div class="flex items-center justify-between p-3.5 bg-slate-50 hover:bg-blue-50/50 rounded-xl border border-slate-200 transition">
                                <div class="flex items-center space-x-3">
                                    <div class="w-10 h-10 rounded-xl bg-indigo-100 text-indigo-600 flex items-center justify-center font-bold text-sm">
                                        01
                                    </div>
                                    <div>
                                        <h4 class="text-xs font-bold text-slate-800">ชุดบทเรียนซ่อมเสริม: การแก้โจทย์ปัญหาสถิติ</h4>
                                        <p class="text-[11px] text-slate-500">คลิปสั้น 8 นาที + แบบฝึกหัดปรับระดับ 5 ข้อ</p>
                                    </div>
                                </div>
                                <button onclick="alert('กำลังเปิดบทเรียนซ่อมเสริมสถิติ...')" class="bg-indigo-600 hover:bg-indigo-700 text-white text-xs px-3.5 py-1.5 rounded-lg font-medium shadow-sm transition">
                                    เริ่มเรียนทันที
                                </button>
                            </div>

                            <!-- Module Item 2 -->
                            <div class="flex items-center justify-between p-3.5 bg-slate-50 hover:bg-blue-50/50 rounded-xl border border-slate-200 transition">
                                <div class="flex items-center space-x-3">
                                    <div class="w-10 h-10 rounded-xl bg-blue-100 text-blue-600 flex items-center justify-center font-bold text-sm">
                                        02
                                    </div>
                                    <div>
                                        <h4 class="text-xs font-bold text-slate-800">แบบทดสอบ Adaptive ครั้งถัดไป: สมการเชิงเส้นและฟังก์ชัน</h4>
                                        <p class="text-[11px] text-slate-500">ระบบจะปรับความยากตามระดับสมรรถนะของคุณ</p>
                                    </div>
                                </div>
                                <button onclick="switchTab('simulator')" class="bg-blue-600 hover:bg-blue-700 text-white text-xs px-3.5 py-1.5 rounded-lg font-medium shadow-sm transition">
                                    ทดสอบปรับระดับ
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

        </div>

        <!-- ========================================== -->
        <!-- 3. ADAPTIVE QUIZ SIMULATOR VIEW -->
        <!-- ========================================== -->
        <div id="view-simulator" class="space-y-6 hidden">
            <div class="bg-white p-6 rounded-3xl border border-slate-200 shadow-sm max-w-3xl mx-auto">
                <div class="flex justify-between items-center pb-4 border-b border-slate-100 mb-6">
                    <div>
                        <span class="bg-indigo-100 text-indigo-700 text-xs font-bold px-3 py-1 rounded-full uppercase tracking-wider">Interactive Assessment Engine</span>
                        <h2 class="text-xl font-extrabold text-slate-800 mt-1">ระบบจำลองแบบทดสอบปรับระดับความยาก (Adaptive Engine)</h2>
                    </div>
                    <div class="text-right">
                        <span class="text-xs text-slate-400 block">ระดับความยากปัจจุบัน</span>
                        <span id="current-difficulty" class="text-sm font-bold text-amber-600 bg-amber-50 px-2.5 py-0.5 rounded-md border border-amber-200">ปานกลาง (Medium)</span>
                    </div>
                </div>

                <!-- Live Indicator -->
                <div class="bg-slate-50 p-4 rounded-2xl mb-6 flex items-center justify-between text-xs">
                    <div class="flex items-center space-x-2">
                        <span class="w-2.5 h-2.5 bg-emerald-500 rounded-full animate-pulse"></span>
                        <span class="font-medium text-slate-600">คะแนนความสามารถสะสม (Theta Level): <strong id="theta-score" class="text-slate-900 font-bold">0.50</strong></span>
                    </div>
                    <div class="text-slate-500">
                        ข้อที่ตอบแล้ว: <span id="quiz-count" class="font-bold text-blue-600">0</span> ข้อ
                    </div>
                </div>

                <!-- Quiz Card Container -->
                <div id="quiz-card" class="bg-slate-50 border border-slate-200 p-6 rounded-2xl">
                    <div class="flex justify-between items-center text-xs font-bold text-slate-500 mb-2">
                        <span id="question-category">หมวดหมู่: การวิเคราะห์สถิติ</span>
                        <span id="question-points">คะแนนน้ำหนัก: 10 คะแนน</span>
                    </div>
                    <h3 id="question-text" class="text-base font-bold text-slate-800 mb-6">
                        โจทย์จะแสดงที่นี่ตามระดับความยากของผู้เรียน...
                    </h3>

                    <!-- Choices Container -->
                    <div id="choices-container" class="space-y-3">
                        <!-- Choices injected dynamically -->
                    </div>

                    <!-- Hint / Feedback Box -->
                    <div id="feedback-box" class="mt-4 p-3.5 rounded-xl text-xs hidden"></div>
                </div>

                <!-- Mechanics Explanation -->
                <div class="mt-6 border-t border-slate-100 pt-4 text-xs text-slate-500 leading-relaxed">
                    <p class="font-bold text-slate-700 mb-1"><i class="fa-solid fa-circle-info text-blue-500"></i> หลักการทำงานของ Smart Adaptive Assessment:</p>
                    <ul class="list-disc pl-5 space-y-1">
                        <li><strong>ตอบถูก:</strong> ระบบจะเพิ่มระดับความยากของข้อถัดไปเพื่อวัดขีดขอบเขตความรู้จริง (IRT Model)</li>
                        <li><strong>ตอบผิด:</strong> ระบบจะปรับลดความยากลงมา พร้อมแสดงคำแนะนำ (Hint) ซ่อมเสริมความเข้าใจผิด</li>
                    </ul>
                </div>
            </div>
        </div>

    </main>

    <!-- Remediation Action Modal -->
    <div id="remediationModal" class="fixed inset-0 bg-slate-900/40 backdrop-blur-xs flex items-center justify-center p-4 z-50 hidden">
        <div class="bg-white rounded-3xl max-w-md w-full p-6 shadow-xl border border-slate-100 space-y-4">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="font-bold text-slate-800 text-base">มอบหมายแบบเรียนซ่อมเสริม</h3>
                <button onclick="closeModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <div>
                <p class="text-xs text-slate-500 mb-1">ส่งถึงนักเรียน:</p>
                <div id="modalStudentName" class="font-bold text-sm text-slate-800 bg-slate-50 p-2.5 rounded-xl border border-slate-200">
                    -
                </div>
            </div>
            <div>
                <label class="block text-xs font-semibold text-slate-700 mb-1">เลือกชุดเนื้อหาซ่อมเสริมที่แนะนำโดย AI:</label>
                <select class="w-full text-xs p-2.5 bg-slate-50 border border-slate-300 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-500">
                    <option>ชุดที่ 1: คลิปและแบบฝึกหัดทบทวน "สมการและโจทย์ปัญหา"</option>
                    <option>ชุดที่ 2: บทเรียนปฏิสัมพันธ์ "การอ่านกราฟและสถิติพื้นฐาน"</option>
                    <option>ชุดที่ 3: แบบฝึกหัดปรับพื้นฐานตรรกศาสตร์รายบุคคล</option>
                </select>
            </div>
            <div>
                <label class="block text-xs font-semibold text-slate-700 mb-1">ข้อความจากครูผู้สอนถึงนักเรียน:</label>
                <textarea rows="3" class="w-full text-xs p-2.5 bg-slate-50 border border-slate-300 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="ครูเห็นว่าหนูยังสับสนเรื่องแก้โจทย์ ลองทำคลิปชุดนี้ดูนะครับ..."></textarea>
            </div>
            <div class="flex justify-end space-x-2 pt-2">
                <button onclick="closeModal()" class="px-4 py-2 text-xs font-bold text-slate-600 bg-slate-100 hover:bg-slate-200 rounded-xl transition">ยกเลิก</button>
                <button onclick="confirmRemediation()" class="px-4 py-2 text-xs font-bold text-white bg-blue-600 hover:bg-blue-700 rounded-xl shadow-sm transition">ยืนยันส่งข้อมูล</button>
            </div>
        </div>
    </div>

    <!-- JavaScript Application Logic -->
    <script>
        // Mock Data for 40 Students
        const mockStudents = [
            { id: 1, name: "นายสมชาย ใจดี", score: 88, accuracy: 90, time: "14 นาที", attempts: 1, weakness: "ไม่มี", status: "passed" },
            { id: 2, name: "นางสาวสมหญิง รักเรียน", score: 92, accuracy: 95, time: "12 นาที", attempts: 1, weakness: "ไม่มี", status: "passed" },
            { id: 3, name: "นายกิตติศักดิ์ มั่นคง", score: 52, accuracy: 50, time: "25 นาที", attempts: 3, weakness: "การแก้โจทย์ปัญหาสถิติ", status: "needs_improvement" },
            { id: 4, name: "นางสาวปรียาพร ดีเลิศ", score: 85, accuracy: 88, time: "16 นาที", attempts: 1, weakness: "ตรรกศาสตร์เชิงซ้อน", status: "passed" },
            { id: 5, name: "นายธนกฤต ชัยชนะ", score: 48, accuracy: 45, time: "28 นาที", attempts: 4, weakness: "สมการกำลังสอง", status: "needs_improvement" },
            { id: 6, name: "นางสาวเกศินี มีสุข", score: 78, accuracy: 80, time: "18 นาที", attempts: 2, weakness: "พีชคณิตพื้นฐาน", status: "passed" },
            { id: 7, name: "นายอนันต์ สายตรง", score: 58, accuracy: 55, time: "22 นาที", attempts: 3, weakness: "การตีความกราฟ", status: "needs_improvement" },
            { id: 8, name: "นายสมนึก เรียนดี", score: 78, accuracy: 82, time: "15 นาที", attempts: 1, weakness: "โจทย์ปัญหาประยุกต์", status: "passed" },
            { id: 9, name: "นางสาววิภาดา พรหมดี", score: 95, accuracy: 98, time: "11 นาที", attempts: 1, weakness: "ไม่มี", status: "passed" },
            { id: 10, name: "นายชยพล สุขสันต์", score: 42, accuracy: 40, time: "30 นาที", attempts: 4, weakness: "สมการและสถิติ", status: "needs_improvement" },
        ];

        // Generate remaining 30 students dynamically to complete 40 count
        const firstNames = ["ชูเกียรติ", "ณิชา", "พงศธร", "กัญญา", "ธีรภัทร", "ศิริพร", "วรวุฒิ", "อรอนงค์", "ภาณุพงศ์", "นภัสสร"];
        const lastNames = ["วงค์ใหญ่", "ศรีสุข", "เจริญผล", "บุญมี", "จันทร์หอม", "ทองแท้", "มีมาก", "สมบูรณ์", "แก้วมณี", "รัตนตรัย"];

        for (let i = 11; i <= 40; i++) {
            const fn = firstNames[i % firstNames.length];
            const ln = lastNames[(i * 3) % lastNames.length];
            
            // Ensure exact 32 passed, 8 needs_improvement balance (4 already added above, add 4 more)
            const isNeedsImprovement = (i === 15 || i === 22 || i === 28 || i === 35);
            
            mockStudents.push({
                id: i,
                name: `นาย/นางสาว${fn} ${ln}`,
                score: isNeedsImprovement ? Math.floor(Math.random() * 15) + 40 : Math.floor(Math.random() * 25) + 70,
                accuracy: isNeedsImprovement ? Math.floor(Math.random() * 15) + 40 : Math.floor(Math.random() * 20) + 75,
                time: `${Math.floor(Math.random() * 15) + 12} นาที`,
                attempts: isNeedsImprovement ? Math.floor(Math.random() * 2) + 3 : 1,
                weakness: isNeedsImprovement ? "วิเคราะห์โจทย์ประยุกต์" : "ไม่มี",
                status: isNeedsImprovement ? "needs_improvement" : "passed"
            });
        }

        let currentFilter = 'all';

        // Render Table Rows
        function renderTable(data) {
            const tbody = document.getElementById('studentTableBody');
            tbody.innerHTML = '';

            data.forEach(s => {
                const isPassed = s.status === 'passed';
                const row = document.createElement('tr');
                row.className = "hover:bg-slate-50/80 transition text-xs";
                row.innerHTML = `
                    <td class="p-3.5 pl-5 font-semibold text-slate-800">${s.name}</td>
                    <td class="p-3.5"><span class="font-bold ${isPassed ? 'text-slate-800' : 'text-rose-600'}">${s.score}</span> / 100</td>
                    <td class="p-3.5">
                        <div class="flex items-center space-x-2">
                            <div class="w-16 bg-slate-200 h-2 rounded-full overflow-hidden">
                                <div class="h-full ${isPassed ? 'bg-emerald-500' : 'bg-rose-500'}" style="width: ${s.accuracy}%"></div>
                            </div>
                            <span class="font-medium text-slate-600">${s.accuracy}%</span>
                        </div>
                    </td>
                    <td class="p-3.5 text-slate-500">${s.time}</td>
                    <td class="p-3.5"><span class="${s.weakness !== 'ไม่มี' ? 'text-rose-600 font-medium' : 'text-slate-400'}">${s.weakness}</span></td>
                    <td class="p-3.5">
                        <span class="px-2.5 py-1 rounded-full text-[10px] font-bold ${isPassed ? 'bg-emerald-100 text-emerald-700' : 'bg-rose-100 text-rose-700'}">
                            ${isPassed ? 'ผ่านเกณฑ์' : 'ต้องพัฒนา'}
                        </span>
                    </td>
                    <td class="p-3.5 text-center">
                        <button onclick="openRemediationModal('${s.name}')" class="px-2.5 py-1 text-[11px] bg-slate-100 hover:bg-blue-50 text-blue-600 border border-slate-200 rounded-lg transition font-medium">
                            ${isPassed ? 'ดูรายงาน' : 'มอบหมายซ่อมเสริม'}
                        </button>
                    </td>
                `;
                tbody.appendChild(row);
            });

            document.getElementById('showing-count').innerText = data.length;
        }

        // Filter Table Function
        function filterTable(status) {
            currentFilter = status;
            
            // Update button UI
            ['all', 'passed', 'needs'].forEach(b => {
                const btn = document.getElementById(`btn-filter-${b}`);
                if (btn) {
                    btn.className = "px-3 py-1 rounded-lg text-slate-600 hover:text-slate-900";
                }
            });

            if (status === 'all') {
                document.getElementById('btn-filter-all').className = "px-3 py-1 rounded-lg bg-white shadow-sm text-slate-800 font-bold";
                renderTable(mockStudents);
            } else if (status === 'passed') {
                document.getElementById('btn-filter-passed').className = "px-3 py-1 rounded-lg bg-emerald-500 text-white shadow-sm font-bold";
                renderTable(mockStudents.filter(s => s.status === 'passed'));
            } else if (status === 'needs_improvement') {
                document.getElementById('btn-filter-needs').className = "px-3 py-1 rounded-lg bg-rose-500 text-white shadow-sm font-bold";
                renderTable(mockStudents.filter(s => s.status === 'needs_improvement'));
            }
        }

        // Search Input Function
        function searchStudent() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const filtered = mockStudents.filter(s => 
                s.name.toLowerCase().includes(query) && 
                (currentFilter === 'all' || s.status === currentFilter)
            );
            renderTable(filtered);
        }

        // View Tab Switching
        function switchTab(tabName) {
            ['teacher', 'student', 'simulator'].forEach(t => {
                document.getElementById(`view-${t}`).classList.add('hidden');
                document.getElementById(`tab-${t}`).classList.remove('tab-active');
                document.getElementById(`tab-${t}`).classList.add('text-slate-500');
            });

            document.getElementById(`view-${tabName}`).classList.remove('hidden');
            document.getElementById(`tab-${tabName}`).classList.add('tab-active');
            document.getElementById(`tab-${tabName}`).classList.remove('text-slate-500');
        }

        // Charts Initialization
        window.addEventListener('DOMContentLoaded', () => {
            renderTable(mockStudents);

            // 1. Mastery Pie Chart
            const pieCtx = document.getElementById('masteryPieChart').getContext('2d');
            new Chart(pieCtx, {
                type: 'doughnut',
                data: {
                    labels: ['ผ่านเกณฑ์ (Passed)', 'ต้องพัฒนา (Needs Improvement)'],
                    datasets: [{
                        data: [32, 8],
                        backgroundColor: ['#22c55e', '#f43f5e'],
                        borderWidth: 0,
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { position: 'bottom' }
                    },
                    cutout: '70%'
                }
            });

            // 2. Topic Radar/Bar Chart
            const radarCtx = document.getElementById('topicRadarChart').getContext('2d');
            new Chart(radarCtx, {
                type: 'bar',
                data: {
                    labels: ['การคำนวณเบื้องต้น', 'พีชคณิต/สมการ', 'ตรรกศาสตร์', 'โจทย์ปัญหาสถิติ'],
                    datasets: [{
                        label: 'เปอร์เซ็นต์ความเข้าใจเฉลี่ยของห้อง (%)',
                        data: [88, 74, 82, 58],
                        backgroundColor: ['#3b82f6', '#6366f1', '#8b5cf6', '#f43f5e'],
                        borderRadius: 8
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: { beginAtZero: true, max: 100 }
                    },
                    plugins: {
                        legend: { display: false }
                    }
                }
            });

            // 3. Student Personal Radar Chart
            const studentCtx = document.getElementById('studentRadarChart').getContext('2d');
            new Chart(studentCtx, {
                type: 'radar',
                data: {
                    labels: ['ความถูกต้อง', 'ความเร็วในการตอบ', 'ความเข้าใจสถิติ', 'พีชคณิต', 'ตรรกศาสตร์'],
                    datasets: [{
                        label: 'สมรรถนะของคุณ',
                        data: [82, 88, 54, 92, 80],
                        backgroundColor: 'rgba(59, 130, 246, 0.2)',
                        borderColor: '#3b82f6',
                        pointBackgroundColor: '#2563eb'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        r: { beginAtZero: true, max: 100 }
                    }
                }
            });

            // Load First Adaptive Question
            loadAdaptiveQuestion();
        });

        // Modal Functions
        function openRemediationModal(name) {
            document.getElementById('modalStudentName').innerText = name;
            document.getElementById('remediationModal').classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('remediationModal').classList.add('hidden');
        }

        function confirmRemediation() {
            alert('ระบบได้ส่งมอบหมายชุดเรียนซ่อมเสริมเรียบร้อยแล้ว');
            closeModal();
        }

        // Adaptive Quiz Simulator Mechanics
        const adaptiveQuestions = {
            easy: [
                {
                    q: "ข้อใดคือค่าเฉลี่ยเลขคณิตของข้อมูล: 4, 6, 8, 10?",
                    choices: ["6", "7", "8", "9"],
                    correct: 1,
                    hint: "คำแนะนำ: ค่าเฉลี่ย = (ผลรวมข้อมูล) ÷ จำนวนข้อมูล = (28) ÷ 4 = 7"
                }
            ],
            medium: [
                {
                    q: "ถ้าความสูงเฉลี่ยของนักเรียน 5 คนเท่ากับ 160 ซม. ต่อมามีนักเรียนสูง 170 ซม. เพิ่มเข้ามาอีก 1 คน ค่าเฉลี่ยใหม่จะเป็นเท่าใด?",
                    choices: ["160.5 ซม.", "161.6 ซม.", "162.0 ซม.", "165.0 ซม."],
                    correct: 1,
                    hint: "คำแนะนำ: ผลรวมเดิม = 5 × 160 = 800 | รวมใหม่ = 800 + 170 = 970 | เฉลี่ยใหม่ = 970 ÷ 6 = 161.6"
                }
            ],
            hard: [
                {
                    q: "ในการสอบวิชาคณิตศาสตร์ คะแนนมีความน่าจะเป็นแบบโค้งปกติ โดยมีค่าเฉลี่ย 50 และส่วนเบี่ยงเบนมาตรฐาน 10 ข้อใดคือเปอร์เซ็นต์ของนักเรียนที่ได้คะแนนระหว่าง 40 ถึง 60 คะแนน?",
                    choices: ["50.0%", "68.2%", "95.4%", "99.7%"],
                    correct: 1,
                    hint: "คำแนะนำ: ช่วง μ ± 1σ ในโค้งปกติจะมีพื้นที่ประมาณ 68.27%"
                }
            ]
        };

        let currentDiff = 'medium';
        let theta = 0.5;
        let questionCounter = 0;

        function loadAdaptiveQuestion() {
            const feedbackBox = document.getElementById('feedback-box');
            feedbackBox.classList.add('hidden');

            const diffText = {
                easy: "ง่าย (Easy)",
                medium: "ปานกลาง (Medium)",
                hard: "ยาก/ท้าทาย (Hard)"
            };

            const diffColor = {
                easy: "text-emerald-600 bg-emerald-50 border-emerald-200",
                medium: "text-amber-600 bg-amber-50 border-amber-200",
                hard: "text-rose-600 bg-rose-50 border-rose-200"
            };

            document.getElementById('current-difficulty').innerText = diffText[currentDiff];
            document.getElementById('current-difficulty').className = `text-sm font-bold px-2.5 py-0.5 rounded-md border ${diffColor[currentDiff]}`;
            document.getElementById('theta-score').innerText = theta.toFixed(2);
            document.getElementById('quiz-count').innerText = questionCounter;

            const qData = adaptiveQuestions[currentDiff][0];
            document.getElementById('question-text').innerText = qData.q;

            const container = document.getElementById('choices-container');
            container.innerHTML = '';

            qData.choices.forEach((choice, idx) => {
                const btn = document.createElement('button');
                btn.className = "w-full text-left p-3.5 bg-white hover:bg-blue-50 border border-slate-200 hover:border-blue-300 rounded-xl transition text-xs font-medium text-slate-700 flex items-center justify-between";
                btn.innerHTML = `<span>${idx + 1}. ${choice}</span> <i class="fa-solid fa-chevron-right text-slate-300 text-xs"></i>`;
                btn.onclick = () => submitAnswer(idx, qData.correct, qData.hint);
                container.appendChild(btn);
            });
        }

        function submitAnswer(selectedIndex, correctIndex, hintText) {
            questionCounter++;
            const feedbackBox = document.getElementById('feedback-box');
            feedbackBox.classList.remove('hidden');

            if (selectedIndex === correctIndex) {
                theta = Math.min(1.0, theta + 0.2);
                feedbackBox.className = "mt-4 p-3.5 rounded-xl text-xs bg-emerald-50 border border-emerald-200 text-emerald-800";
                feedbackBox.innerHTML = `<i class="fa-solid fa-circle-check text-emerald-600 mr-1"></i> <strong>ถูกต้อง!</strong> ระบบปรับเพิ่มระดับความยากในข้อถัดไปเพื่อทดสอบความสามารถระดับสูงขึ้น`;

                if (currentDiff === 'easy') currentDiff = 'medium';
                else if (currentDiff === 'medium') currentDiff = 'hard';

            } else {
                theta = Math.max(0.0, theta - 0.2);
                feedbackBox.className = "mt-4 p-3.5 rounded-xl text-xs bg-rose-50 border border-rose-200 text-rose-800";
                feedbackBox.innerHTML = `<i class="fa-solid fa-circle-xmark text-rose-600 mr-1"></i> <strong>ยังไม่ถูกต้อง!</strong> <br><span class="mt-1 block">${hintText}</span>`;

                if (currentDiff === 'hard') currentDiff = 'medium';
                else if (currentDiff === 'medium') currentDiff = 'easy';
            }

            setTimeout(() => {
                loadAdaptiveQuestion();
            }, 3000);
        }
    </script>
</body>
</html>
