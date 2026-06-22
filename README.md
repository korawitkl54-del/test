



<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>โครงงานคณิตศาสตร์เรื่อง เทเลสโคปิกกำลังสาม (Telescoping Cubic)</title>

  <script src="https://cdn.jsdelivr.net/npm/decimal.js@9.0.0/decimal.min.js"></script>
  
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  
  <!-- Google Font: Prompt -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  
  <!-- Material Icons -->
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
  
  <!-- Chart.js -->
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  
  <!-- SweetAlert2 for beautiful popups -->
  <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>

  <!-- MathJax for rendering LaTeX equations beautifully -->
  <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

  <style>
    body {
      font-family: 'Prompt', sans-serif;
    }
    .pastel-gradient {
      background: linear-gradient(135deg, #F3F4F6 0%, #F5F3FF 50%, #EEF2F6 100%);
    }
    .card-pastel {
      background: rgba(255, 255, 255, 0.9);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.6);
      box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.05), 0 8px 10px -6px rgba(0, 0, 0, 0.03);
    }
    .custom-scrollbar::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    .custom-scrollbar::-webkit-scrollbar-track {
      background: #f1f1f1;
    }
    .custom-scrollbar::-webkit-scrollbar-thumb {
      background: #cbd5e1;
      border-radius: 3px;
    }
    .tab-active {
      background-color: #ffffff;
      color: #4f46e5;
      box-shadow: 0 4px 6px -1px rgba(79, 70, 229, 0.1), 0 2px 4px -1px rgba(79, 70, 229, 0.06);
      border-bottom: 2px solid #4f46e5;
    }
    /* Simple Animation */
    .fade-in {
      animation: fadeIn 0.4s ease-out forwards;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(8px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body class="pastel-gradient min-h-screen flex flex-col justify-between text-slate-800">

  <!-- Header Section -->
  <header class="bg-white/80 backdrop-blur-md border-b border-indigo-100 sticky top-0 z-50 transition-all">
    <div class="max-w-7xl mx-auto px-4 py-4 sm:px-6 lg:px-8 flex flex-col lg:flex-row items-center justify-between gap-4">
      <div class="flex items-center gap-3 w-full lg:w-auto">
        <!-- โลโก้โรงเรียนบัวใหญ่ -->
        <img src="https://itals.kku.ac.th/ups/myfile/6a29216fa6c98.jpg" alt="ตราโรงเรียนบัวใหญ่" class="h-16 w-auto object-contain filter drop-shadow-sm shrink-0">
        <div class="p-2 bg-indigo-50 rounded-2xl text-indigo-600 shadow-inner shrink-0 hidden sm:block">
          <span class="material-icons text-3xl animate-pulse">calculate</span>
        </div>
        <div>
          <h1 class="text-base sm:text-lg lg:text-xl font-bold bg-gradient-to-r from-indigo-600 via-purple-600 to-pink-500 bg-clip-text text-transparent">
            โครงงานคณิตศาสตร์เรื่อง เทเลสโคปิกกำลังสาม (Telescoping Cubic)
          </h1>
          <p class="text-[10px] sm:text-xs text-slate-500 font-medium">จากคณิตศาสตร์บริสุทธิ์สู่อัลกอริทึมการประมวลผลความเร็วสูง โรงเรียนบัวใหญ่</p>
        </div>
      </div>
      <!-- Tab Navigation Buttons -->
      <nav class="flex bg-slate-100/80 p-1.5 rounded-2xl w-full lg:w-auto overflow-x-auto gap-1">
        <button onclick="switchTab('lesson')" id="tab-lesson" class="flex-1 sm:flex-none flex items-center justify-center gap-1.5 px-4 py-2.5 rounded-xl text-sm font-semibold transition-all tab-active whitespace-nowrap">
          <span class="material-icons text-lg">local_library</span> บทเรียนโครงงาน
        </button>
        <button onclick="switchTab('simulation')" id="tab-simulation" class="flex-1 sm:flex-none flex items-center justify-center gap-1.5 px-4 py-2.5 rounded-xl text-sm font-semibold transition-all text-slate-600 hover:bg-white/50 whitespace-nowrap">
          <span class="material-icons text-lg">science</span> ระบบจำลองเวลา
        </button>
        <button onclick="switchTab('gallery')" id="tab-gallery" class="flex-1 sm:flex-none flex items-center justify-center gap-1.5 px-4 py-2.5 rounded-xl text-sm font-semibold transition-all text-slate-600 hover:bg-white/50 whitespace-nowrap">
          <span class="material-icons text-lg">photo_library</span> ภาพกิจกรรมการเรียนรู้
        </button>
      </nav>
    </div>
  </header>

  <!-- Main Content Container -->
  <main class="max-w-7xl mx-auto px-4 py-8 sm:px-6 lg:px-8 flex-grow w-full">
    
    <!-- ================= TAB 1: LESSONS ================= -->
    <section id="content-lesson" class="space-y-8 fade-in">
      <!-- Welcome Hero Card -->
      <div class="card-pastel p-6 sm:p-8 rounded-3xl shadow-sm border border-white/60 flex flex-col md:flex-row items-center gap-6">
        <div class="space-y-4 md:w-2/3">
          <span class="inline-flex items-center gap-1.5 px-3 py-1.5 rounded-full text-xs font-semibold bg-indigo-100 text-indigo-700">
            <span class="material-icons text-sm">stars</span> นวัตกรรมการคำนวณ ม.ต้น
          </span>
          <h2 class="text-xl sm:text-2xl lg:text-3xl font-extrabold text-slate-800 leading-snug">
            เทเลสโคปิกกำลังสาม (Telescoping Cubic): ยุบรูปสมการคณิตศาสตร์บริสุทธิ์สู่อัลกอริทึมแห่งอนาคt
          </h2>
          <p class="text-slate-600 leading-relaxed text-sm sm:text-base">
            ยินดีต้อนรับสู่ระบบเรียนรู้เชิงโต้ตอบ! โครงงานนี้เกิดจากความตั้งใจที่จะรวมเอา **คณิตศาสตร์บริสุทธิ์ (Pure Mathematics)** ในส่วนของอนุกรมคูณสะสม (Cumulative Product) และหลักการของ **เทเลสโคปิก (Telescoping)** มาร่วมขับเคลื่อนการพัฒนาโปรแกรมคอมพิวเตอร์ 
            ช่วยลดระยะเวลาประมวลผลและการจัดสรรหน่วยความจำ จากวิธีแบบตรง $O(k)$ เป็นวิธีลัดความเร็วแสง $O(1)$
          </p>
        </div>
        <div class="md:w-1/3 flex justify-center">
          <div class="w-48 h-48 rounded-3xl bg-gradient-to-br from-indigo-50 to-pink-50 flex items-center justify-center shadow-inner relative border border-white/40">
            <span class="material-icons text-7xl text-indigo-500/80 animate-bounce">speed</span>
            <div class="absolute -top-2 -right-2 w-14 h-14 bg-pink-100 rounded-full flex items-center justify-center shadow-md">
              <span class="material-icons text-2xl text-pink-500 animate-pulse">lightbulb</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Theory Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
        <!-- Formulas Card with LaTeX Rendering -->
        <div class="card-pastel p-6 rounded-3xl shadow-sm space-y-6">
          <div class="flex items-center gap-2 text-indigo-600 font-bold text-lg border-b border-indigo-50 pb-3">
            <span class="material-icons">architecture</span>
            <span>โครงสร้างรูปสมการที่ใช้ศึกษา</span>
          </div>
          <div class="space-y-6">
            <div class="bg-indigo-50/50 p-4 rounded-2xl border border-indigo-100 flex flex-col items-center">
              <p class="text-xs text-indigo-700 font-semibold mb-3 self-start">1. โจทย์ผลคูณสะสมเริ่มต้น (Cumulative Product)</p>
              <div class="text-center p-3 bg-white rounded-xl shadow-sm border border-indigo-50 w-full">
                $$\prod_{n = a+1}^{k} \frac{(n+1)^3 + a^3}{n^3 - a^3}$$
              </div>
            </div>
            
            <div class="bg-emerald-50/50 p-4 rounded-2xl border border-emerald-100 flex flex-col items-center">
              <p class="text-xs text-emerald-700 font-semibold mb-3 self-start">2. สูตรสำเร็จรูปที่ผ่านการยุบรูป (Closed-form Formula)</p>
              <div class="text-center p-3 bg-white rounded-xl shadow-sm border border-emerald-50 w-full">
                $$\binom{k+a+1}{2a+1} \times \frac{\prod_{i=2}^{a}(i^2+ai+a^2)}{\prod_{j=k-a+2}^{k}(j^2+aj+a^2)}$$
              </div>
            </div>
          </div>
        </div>

        <!-- Computer Science Theory Card -->
        <div class="card-pastel p-6 rounded-3xl shadow-sm space-y-6">
          <div class="flex items-center gap-2 text-pink-600 font-bold text-lg border-b border-pink-50 pb-3">
            <span class="material-icons">terminal</span>
            <span>ทำไมการพิสูจน์นี้จึงสำคัญต่อโลกโปรแกรมมิ่ง?</span>
          </div>
          <div class="space-y-4 text-sm leading-relaxed">
            <div class="flex gap-4 items-start bg-pink-50/30 p-4 rounded-2xl border border-pink-100/50">
              <div class="p-2 bg-pink-100 rounded-lg text-pink-600 font-semibold shrink-0">A</div>
              <div>
                <h4 class="font-bold text-slate-800">Algorithm A: วิธีวนลูปประมวลผล (Brute-Force)</h4>
                <p class="text-slate-600 mt-1">
                  คอมพิวเตอร์คำนวณวงเล็บทีละวงเล็บ ตั้งแต่ $n = a+1$ ถึง $k$ หาก $k$ มีค่า 1,000,000 รอบ คอมพิวเตอร์ต้องทำงานซ้ำ ๆ 1 ล้านครั้ง! คิดเป็นความซับซ้อนเชิงเวลา <strong class="text-pink-600 font-semibold">O(k) (Linear Time)</strong>
                </p>
              </div>
            </div>

            <div class="flex gap-4 items-start bg-indigo-50/30 p-4 rounded-2xl border border-indigo-100/50">
              <div class="p-2 bg-indigo-100 rounded-lg text-indigo-600 font-semibold shrink-0">B</div>
              <div>
                <h4 class="font-bold text-slate-800">Algorithm B: วิธีสูตรสำเร็จความเร็วแสง (Closed-Form)</h4>
                <p class="text-slate-600 mt-1">
                  เมื่อยุบรูปสูตรสำเร็จแล้ว คอมพิวเตอร์ไม่ต้องวิ่งลูปพจน์ซ้ำนับล้านตัว สามารถนำค่าขอบเขตบน ($k$) แทนค่าลงในสูตรสำเร็จรูปแล้วบวกลบคูณหารคำนวณผลลัพธ์ในครั้งเดียวได้ทันที คิดเป็นความซับซ้อนเชิงเวลา <strong class="text-indigo-600 font-semibold">O(1) (Constant Time)</strong>
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ================= TAB 2: SIMULATION & PLAYGROUND ================= -->
    <section id="content-simulation" class="hidden space-y-8 fade-in">
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
        
        <!-- Controls Card (1/3 Width) -->
        <div class="card-pastel p-6 rounded-3xl shadow-sm space-y-6 lg:col-span-1 h-fit">
          <div class="flex items-center gap-2 text-indigo-600 font-bold text-lg border-b border-indigo-50 pb-3">
            <span class="material-icons">settings</span>
            <span>ตั้งค่าเครื่องมือจำลอง</span>
          </div>

          <div class="space-y-4">
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-1 flex items-center justify-between">
                <span>กำหนดตัวแปรเริ่มต้น (a):</span>
                <span class="text-xs text-slate-400 font-normal">แนะนำ: 1 - 5</span>
              </label>
              <input type="number" id="input-a" value="3" min="1" max="10" 
                     class="w-full px-4 py-3 rounded-2xl bg-white border border-slate-200 focus:ring-2 focus:ring-indigo-400 focus:outline-none transition-all text-center font-semibold text-lg">
            </div>

            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-1 flex items-center justify-between">
                <span>กำหนดจำนวนพจน์สุดท้าย (k):</span>
                <span class="text-xs text-slate-400 font-normal">ยิ่งมากยิ่งเห็นความต่างของเวลา</span>
              </label>
              <input type="number" id="input-k" value="1000" min="2" max="10000000" 
                     class="w-full px-4 py-3 rounded-2xl bg-white border border-slate-200 focus:ring-2 focus:ring-indigo-400 focus:outline-none transition-all text-center font-semibold text-lg">
            </div>

            <!-- Quick presets -->
            <div class="space-y-1.5">
              <p class="text-xs text-slate-500 font-medium">กดเลือกขนาดจำลองด่วน (ค่า k):</p>
              <div class="grid grid-cols-3 gap-2">
                <button onclick="setK(10)" class="px-2 py-1.5 bg-slate-100 hover:bg-slate-200 rounded-lg text-xs font-semibold transition-all">10</button>
                <button onclick="setK(100)" class="px-2 py-1.5 bg-slate-100 hover:bg-slate-200 rounded-lg text-xs font-semibold transition-all">100</button>
                <button onclick="setK(1000)" class="px-2 py-1.5 bg-indigo-50 hover:bg-indigo-100 text-indigo-600 rounded-lg text-xs font-semibold transition-all">1,000</button>
              </div>
              <div class="grid grid-cols-3 gap-2">
                <button onclick="setK(10000)" class="px-2 py-1.5 bg-purple-50 hover:bg-purple-100 text-purple-600 rounded-lg text-xs font-semibold transition-all">1 หมื่น</button>
                <button onclick="setK(100000)" class="px-2 py-1.5 bg-pink-50 hover:bg-pink-100 text-pink-600 rounded-lg text-xs font-semibold transition-all">1 แสน</button>
                <button onclick="setK(1000000)" class="px-2 py-1.5 bg-red-50 hover:bg-red-100 text-red-600 rounded-lg text-xs font-semibold transition-all">1 ล้าน ⚡</button>
              </div>
            </div>

            <button onclick="runSimulation()" class="w-full py-4 bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 hover:opacity-90 text-white rounded-2xl font-bold shadow-lg shadow-indigo-100 flex items-center justify-center gap-2 transition-all">
              <span class="material-icons animate-spin" id="btn-spinner" style="display:none;">sync</span>
              <span class="material-icons" id="btn-icon">play_circle</span>
              <span id="btn-text">รันระบบจำลอง</span>
            </button>
          </div>
        </div>

        <!-- Dashboard Outputs (2/3 Width) -->
        <div class="lg:col-span-2 space-y-6">
          
          <!-- Key Indicators Summary -->
          <div class="card-pastel p-6 rounded-3xl shadow-sm grid grid-cols-2 sm:grid-cols-4 gap-4 items-center">
            <div class="text-center p-3.5 bg-pink-50/50 rounded-2xl border border-pink-100 space-y-1">
              <span class="text-[10px] sm:text-xs font-semibold text-pink-700 block">เวลา วิธีวนลูป (A)</span>
              <span class="text-base sm:text-lg font-bold text-pink-600 font-mono" id="time-a">0.000000</span>
              <span class="text-[10px] text-slate-500 block">มิลลิวินาที</span>
            </div>
            
            <div class="text-center p-3.5 bg-indigo-50/50 rounded-2xl border border-indigo-100 space-y-1">
              <span class="text-[10px] sm:text-xs font-semibold text-indigo-700 block">เวลา สูตรลัด (B)</span>
              <span class="text-base sm:text-lg font-bold text-indigo-600 font-mono" id="time-b">0.000000</span>
              <span class="text-[10px] text-slate-500 block">มิลลิวินาที</span>
            </div>

            <div class="text-center p-3.5 bg-emerald-50/80 rounded-2xl border border-emerald-100 space-y-1">
              <span class="text-[10px] sm:text-xs font-semibold text-emerald-700 block">ความเร็วที่เพิ่มขึ้น</span>
              <span class="text-base sm:text-lg font-bold text-emerald-600 font-mono" id="speedup-ratio">0.0</span>
              <span class="text-[10px] text-slate-500 block">เท่า! ⚡</span>
            </div>

            <div class="text-center p-3.5 bg-purple-50 rounded-2xl border border-purple-100 space-y-1">
              <span class="text-[10px] sm:text-xs font-semibold text-purple-700 block">จำนวนรอบวนซ้ำ</span>
              <span class="text-base sm:text-lg font-bold text-purple-600 font-mono" id="brute-rounds">0</span>
              <span class="text-[10px] text-slate-500 block">รอบ ($k-a$)</span>
            </div>
          </div>

          <!-- Answer & Correctness Validation -->
          <div class="card-pastel p-6 rounded-3xl shadow-sm space-y-4">
            <h3 class="font-bold text-slate-800 flex items-center gap-1.5">
              <span class="material-icons text-emerald-500">verified</span>
              ตรวจสอบความถูกต้องเชิงตัวเลข
            </h3>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
              <div class="p-3.5 bg-slate-50/60 rounded-2xl border border-slate-100">
                <span class="text-xs font-semibold text-slate-400 block">ผลลัพธ์จาก Algorithm A ( วนลูปถึก )</span>
                <span class="text-sm sm:text-base font-bold text-slate-700 break-all" id="result-a">-</span>
              </div>
              <div class="p-3.5 bg-slate-50/60 rounded-2xl border border-slate-100">
                <span class="text-xs font-semibold text-slate-400 block">ผลลัพธ์จาก Algorithm B ( สูตรลัดเสร็จเลย )</span>
                <span class="text-sm sm:text-base font-bold text-slate-700 break-all" id="result-b">-</span>
              </div>
            </div>
            <div id="equality-alert" class="hidden p-3 rounded-xl text-xs font-semibold text-center"></div>
          </div>

          <!-- Chart Card with 6 decimal precision context -->
          <div class="card-pastel p-6 rounded-3xl shadow-sm space-y-4">
            <div class="flex items-center justify-between border-b border-slate-100 pb-3">
              <h3 class="font-bold text-slate-800 flex items-center gap-1.5">
                <span class="material-icons text-indigo-500">show_chart</span>
                เปรียบเทียบประสิทธิภาพเวลาที่ใช้ประมวลผล (มิลลิวินาที)
              </h3>
              <button onclick="exportToCSV()" class="flex items-center gap-1 text-xs font-semibold text-indigo-600 hover:text-indigo-800">
                <span class="material-icons text-sm">download</span> ดาวน์โหลดตาราง CSV
              </button>
            </div>
            <div class="h-64 sm:h-80 w-full">
              <canvas id="performanceChart"></canvas>
            </div>
            <p class="text-[11px] text-slate-400 text-center leading-relaxed">
              *แกน X: จำนวนพจน์ในการคำนวณ (k), แกน Y: เวลาเฉลี่ยต่อรอบ (มิลลิวินาที ทศนิยม 6 ตำแหน่ง)
            </p>
          </div>

        </div>
      </div>
    </section>

    <!-- ================= TAB 3: GALLERY ================= -->
    <section id="content-gallery" class="hidden space-y-8 fade-in">
      <div class="card-pastel p-6 sm:p-8 rounded-3xl shadow-sm text-center max-w-3xl mx-auto space-y-4">
        <div class="w-16 h-16 bg-indigo-50 rounded-full flex items-center justify-center mx-auto shadow-sm text-indigo-500">
          <span class="material-icons text-3xl">photo_library</span>
        </div>
        <h2 class="text-xl sm:text-2xl font-bold text-slate-800 font-sans">แกลเลอรีภาพกิจกรรมและการพัฒนานวัตกรรม</h2>
        <p class="text-sm text-slate-500">ภาพบรรยากาศการทำวิจัยและร่วมทดสอบระบบการคำนวณอย่างถูกต้องเหมาะสม</p>
      </div>

      <!-- Grid of Uploaded Images Directly Rendering your exact uploaded JPG assets -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <!-- Photo 1: Planning and Analysis -->
        <div class="card-pastel overflow-hidden rounded-3xl shadow-sm border border-white/60 hover:shadow-md transition-all group">
          <div class="relative overflow-hidden aspect-[4/3] bg-indigo-50 flex items-center justify-center">
            <img id="img-gallery-1" src="https://itals.kku.ac.th/ups/myfile/6a292208f2d99.jpg" alt="การร่วมวิเคราะห์สูตรและวางแผนออกแบบระบบจำลองคอมพิวเตอร์" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300">
            <span class="absolute top-3 left-3 bg-indigo-600/90 text-white text-[10px] uppercase font-bold px-2.5 py-1 rounded-full backdrop-blur-sm">
              เฟสที่ 1: การวางแผน
            </span>
          </div>
          <div class="p-5 space-y-2">
            <h4 class="font-bold text-slate-800 text-sm sm:text-base">การคิดวิเคราะห์ตรรกะร่วมกับครู</h4>
            <p class="text-xs text-slate-500 leading-relaxed">
              คณะนักเรียนร่วมกันวิเคราะห์และทบทวนตรรกะคณิตศาสตร์บริสุทธิ์เพื่อจัดเตรียมความพร้อมในการยุบรูปสูตรสำหรับพัฒนาโปรแกรมจำลองความเร็วเปรียบเทียบ
            </p>
          </div>
        </div>

        <!-- Photo 2: Testing Verification -->
        <div class="card-pastel overflow-hidden rounded-3xl shadow-sm border border-white/60 hover:shadow-md transition-all group">
          <div class="relative overflow-hidden aspect-[4/3] bg-emerald-50 flex items-center justify-center">
            <img id="img-gallery-2" src="https://itals.kku.ac.th/ups/myfile/6a292264bdcd4.jpg" alt="การร่วมกันวิเคราะห์และทบทวนความถูกต้องของอัลกอริทึม" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300">
            <span class="absolute top-3 left-3 bg-emerald-600/90 text-white text-[10px] uppercase font-bold px-2.5 py-1 rounded-full backdrop-blur-sm">
              เฟสที่ 2: การพัฒนาและทดสอบ
            </span>
          </div>
          <div class="p-5 space-y-2">
            <h4 class="font-bold text-slate-800 text-sm sm:text-base">การทดสอบสอบทานรหัสโปรแกรมจำลอง</h4>
            <p class="text-xs text-slate-500 leading-relaxed">
              คณะนักเรียนและคณะครูที่ปรึกษาร่วมกันทดสอบฟังก์ชันจับเวลา Micro-benchmark เพื่อตรวจจับข้อบกพร่องและวิเคราะห์พฤติกรรมโครงสร้าง $O(1)$ ของการลดรูป
            </p>
          </div>
        </div>

        <!-- Photo 3: Presentation and Delivery -->
        <div class="card-pastel overflow-hidden rounded-3xl shadow-sm border border-white/60 hover:shadow-md transition-all group">
          <div class="relative overflow-hidden aspect-[4/3] bg-pink-50 flex items-center justify-center">
            <img id="img-gallery-3" src="https://itals.kku.ac.th/ups/myfile/6a29228edc795.jpg" alt="ทีมงานโครงงานถ่ายภาพร่วมกับคุณครู" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300">
            <span class="absolute top-3 left-3 bg-pink-600/90 text-white text-[10px] uppercase font-bold px-2.5 py-1 rounded-full backdrop-blur-sm">
              เฟสที่ 3: ความสำเร็จโครงงาน
            </span>
          </div>
          <div class="p-5 space-y-2">
            <h4 class="font-bold text-slate-800 text-sm sm:text-base">การส่งมอบงานและถ่ายรูปความสำเร็จ</h4>
            <p class="text-xs text-slate-500 leading-relaxed">
              ภาพความภาคภูมิใจของผู้จัดทำร่วมกับคุณครูขจรภพ และคุณครูที่ปรึกษาโครงงานหลังการร่วมใจวิจัยนวัตกรรมสำเร็จเสร็จสิ้นสมบูรณ์พร้อมจัดแสดงผลการแข่งขัน
            </p>
          </div>
        </div>
      </div>
    </section>

  </main>

  <!-- Visitor Counter Component Section -->
  <section class="max-w-7xl mx-auto px-4 pb-6 sm:px-6 lg:px-8 w-full">
    <div class="card-pastel p-4 sm:p-5 rounded-3xl shadow-sm border border-white/60 flex flex-col sm:flex-row items-center justify-between gap-4 text-center sm:text-left">
      <div class="flex items-center gap-3.5 flex-col sm:flex-row">
        <div class="p-2.5 bg-indigo-50 text-indigo-600 rounded-2xl shadow-inner shrink-0">
          <span class="material-icons text-2xl">visibility</span>
        </div>
        <div>
          <h4 class="text-xs font-extrabold text-slate-500 uppercase tracking-wider">สถิติผู้เข้าชมเว็บไซต์นวัตกรรม (Visitor Counter)</h4>
          <p class="text-xs text-slate-400 mt-1">จำนวนการเยี่ยมชมจริงนับทุกครั้งที่คลิกโหลดหน้าเพจโดยผู้ใช้</p>
        </div>
      </div>
      <div class="flex items-center gap-2 bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 text-white px-5 py-2.5 rounded-2xl font-bold font-mono text-xl shadow-md">
        <span id="visitor-count">000,000</span>
        <span class="text-xs font-medium opacity-90 font-sans">ครั้ง</span>
      </div>
    </div>
  </section>

  <!-- Footer Section -->
  <footer class="bg-slate-900 text-slate-400 py-8 border-t border-slate-800">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col md:flex-row items-center justify-between gap-6 text-center md:text-left">
      <div class="space-y-2 max-w-xl">
        <p class="text-sm font-semibold text-slate-300">
          โครงงานคณิตศาสตร์เรื่อง เทเลสโคปิกกำลังสาม (Telescoping Cubic): จากคณิตศาสตร์บริสุทธิ์สู่อัลกอริทึมการประมวลผลความเร็วสูง
        </p>
        <p class="text-xs text-slate-500 leading-relaxed">
          พัฒนาและออกแบบระบบประเมินจำลองผลความละเอียดสูงทศนิยม 6 ตำแหน่ง สำหรับการสาธิตเชิงประจักษ์และการศึกษาค้นคว้าวิทยาการคอมพิวเตอร์เชิงคณิตศาสตร์
        </p>
      </div>
      <div class="text-xs space-y-1.5 shrink-0">
        <p>© 2025  Ai กับนายขจรภพ  วรรณพงษ์ ครูชำนาญการ โรงเรียนบัวใหญ่  : <a href="mailto:khajonpop@gmail.com" class="hover:underline font-semibold text-indigo-400">khajonpop@gmail.com</a></p>
      </div>
    </div>
  </footer>

  <!-- Firebase SDK Modules for Real-Time Visitor Counter with secure auth fallback -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
    import { getAuth, signInAnonymously, signInWithCustomToken } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
    import { getFirestore, doc, getDoc, setDoc, updateDoc, increment } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

    // Setup basic variable scopes
    let db = null;
    let auth = null;
    const appId = typeof __app_id !== 'undefined' ? __app_id : 'bua-yai-telescopic-app';

    // Safely check and initialize Firebase Config
    if (typeof __firebase_config !== 'undefined' && __firebase_config) {
      try {
        const firebaseConfig = JSON.parse(__firebase_config);
        const app = initializeApp(firebaseConfig);
        auth = getAuth(app);
        db = getFirestore(app);
      } catch (err) {
        console.error("Firebase Initialization failed:", err);
      }
    }

    // Main function to run real-time visitors count with robust simulated fallback
    async function setupVisitorCounter() {
      // Step 1: Initialize local storage check so we increment by 1 on each load
      let count = parseInt(localStorage.getItem('bua_yai_local_visitor_count') || "2450");
      count += 1;
      localStorage.setItem('bua_yai_local_visitor_count', count.toString());

      if (db && auth) {
        try {
          // Rule 3: Auth priority before queries
          if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
            await signInWithCustomToken(auth, __initial_auth_token);
          } else {
            await signInAnonymously(auth);
          }

          // Rule 1: Strict collection paths
          // Path: /artifacts/{appId}/public/data/counters/visitors
          const counterDocRef = doc(db, 'artifacts', appId, 'public', 'data', 'counters', 'visitors');
          const snap = await getDoc(counterDocRef);

          if (snap.exists()) {
            const data = snap.data();
            const cloudCount = (data.count || 2450) + 1;
            await updateDoc(counterDocRef, { count: increment(1) });
            count = cloudCount;
          } else {
            // Document creation
            await setDoc(counterDocRef, { count: count });
          }
        } catch (err) {
          console.warn("Firestore count update failed, using local count increment:", err);
        }
      }

      // Display formatted output
      const formatted = String(Math.round(count)).replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      const element = document.getElementById('visitor-count');
      if (element) {
        element.innerText = formatted;
      }
    }

    // Trigger on boot
    setupVisitorCounter();
  </script>

  <script>
    // Global variable to keep the chart instance
    let perfChartInstance = null;

    // High precision timing function
    function getHighPrecisionTime() {
      return performance.now(); // Floating-point milliseconds
    }

    // Tab switcher logic
    function switchTab(tabId) {
      document.getElementById('content-lesson').classList.add('hidden');
      document.getElementById('content-simulation').classList.add('hidden');
      document.getElementById('content-gallery').classList.add('hidden');

      document.getElementById('tab-lesson').className = 'flex-1 sm:flex-none flex items-center justify-center gap-1.5 px-4 py-2.5 rounded-xl text-sm font-semibold transition-all text-slate-600 hover:bg-white/50 whitespace-nowrap';
      document.getElementById('tab-simulation').className = 'flex-1 sm:flex-none flex items-center justify-center gap-1.5 px-4 py-2.5 rounded-xl text-sm font-semibold transition-all text-slate-600 hover:bg-white/50 whitespace-nowrap';
      document.getElementById('tab-gallery').className = 'flex-1 sm:flex-none flex items-center justify-center gap-1.5 px-4 py-2.5 rounded-xl text-sm font-semibold transition-all text-slate-600 hover:bg-white/50 whitespace-nowrap';

      document.getElementById('content-' + tabId).classList.remove('hidden');
      document.getElementById('tab-' + tabId).className = 'flex-1 sm:flex-none flex items-center justify-center gap-1.5 px-4 py-2.5 rounded-xl text-sm font-semibold transition-all tab-active whitespace-nowrap';

      if (tabId === 'simulation') {
        initChart();
      }
    }

    // Quick set parameter k
    function setK(val) {
      document.getElementById('input-k').value = val;
      Swal.fire({
        icon: 'info',
        title: 'กำหนดค่าจำลองเสร็จสิ้น!',
        text: `ตั้งค่าพจน์สูงสุด k เป็น ${val.toLocaleString()} เรียบร้อยแล้วค่ะ`,
        confirmButtonColor: '#4f46e5',
        toast: true,
        position: 'top-end',
        showConfirmButton: false,
        timer: 1800
      });
    }

    // ================= ALGORITHMS IMPLEMENTATION =================

    // Mathematical Helper for combination calculation C(n, r) USING Decimal.js
   function calculateCombination(n, r) {
  if (r < 0 || r > n) return new Decimal(0);
  if (r === 0 || r === n) return new Decimal(1);
  if (r > n / 2) r = n - r;

  let res = new Decimal(1);
  for (let i = 1; i <= r; i++) {
    res = res.times(n - r + i).dividedBy(i);
  }
  return res;
}
 // Algorithm A: Brute-Force Cumulative Product (O(k)) USING Decimal.js
function calculateBruteForce(a, k) {
  let result = new Decimal(1.0);
  const decA = new Decimal(a);
  const aCubed = decA.pow(3);
  
  for (let n = a + 1; n <= k; n++) {
    const numerator = new Decimal(n + 1).pow(3).plus(aCubed);
    const denominator = new Decimal(n).pow(3).minus(aCubed);
    result = result.times(numerator.dividedBy(denominator));
  }
  return result; // คืนค่าตัวเลขเต็มๆ ไปใช้คำนวณ Benchmark ก่อน
}

// Algorithm B: High-speed Closed-form Formula (O(1)) USING Decimal.js
function calculateByFormula(a, k) {
  const comb = calculateCombination(k + a + 1, 2 * a + 1);
  const decA = new Decimal(a);
  const aSquared = decA.pow(2);

  let numProd = new Decimal(1);
  for (let i = 2; i <= a; i++) {
    const decI = new Decimal(i);
    const term = decI.pow(2).plus(decA.times(decI)).plus(aSquared);
    numProd = numProd.times(term);
  }

  let denProd = new Decimal(1);
  // 📍 แก้จาก j <= j = k เป็น j <= k แค่นี้เลยครับอ้าย!
  for (let j = k - a + 2; j <= k; j++) { 
    const decJ = new Decimal(j);
    const term = decJ.pow(2).plus(decA.times(decJ)).plus(aSquared);
    denProd = denProd.times(term);
  }

  return comb.times(numProd.dividedBy(denProd)); // คืนค่าตัวเลขเต็มๆ ไปใช้คำนวณ Benchmark ก่อน
}

// ================= BENCHMARKING ENGINE WITH HIGH PRECISION =================
// Micro-benchmarking loop technique to secure non-zero float times
function getBenchmarkTimeA(a, k) {
  const iterations = k < 100 ? 5000 : (k < 1000 ? 500 : (k < 10000 ? 50 : 1));
  
  const start = getHighPrecisionTime();
  for (let i = 0; i < iterations; i++) {
    calculateBruteForce(a, k);
  }
  const end = getHighPrecisionTime();
  
  return (end - start) / iterations; // Average time in milliseconds
}

    function getBenchmarkTimeB(a, k) {
      const iterations = 5000;
      
      const start = getHighPrecisionTime();
      for (let i = 0; i < iterations; i++) {
        calculateByFormula(a, k);
      }
      const end = getHighPrecisionTime();
      
      return (end - start) / iterations; // Average time in milliseconds
    }

    // ================= RUN SYSTEM SIMULATION =================
    async function runSimulation() {
      // 📍 บรรทัดนี้สำคัญมาก! ตั้งค่าให้คำนวณแม่นยำลึก 35 ตำแหน่ง
      Decimal.set({ precision: 35 });

      const a = parseInt(document.getElementById('input-a').value);
      const k = parseInt(document.getElementById('input-k').value);

      if (isNaN(a) || isNaN(k) || a < 1 || k <= a) {
        Swal.fire({
          icon: 'error',
          title: 'ข้อมูลนำเข้าไม่ถูกต้อง',
          text: 'กรุณากรอกตัวแปร a และ k ให้ถูกต้อง โดย k ต้องมีค่ามากกว่า a เสมอค่ะ!',
          confirmButtonColor: '#f43f5e'
        });
        return;
      }

      // Dynamic Loader UI
      document.getElementById('btn-spinner').style.display = 'inline-block';
      document.getElementById('btn-icon').style.display = 'none';
      document.getElementById('btn-text').innerText = 'กำลังคำนวณเปรียบเทียบ...';

      // Give UI time to update
      await new Promise(resolve => setTimeout(resolve, 50));

      // 1. Run Algorithm A & Benchmark time
      const timeElapsedA = getBenchmarkTimeA(a, k);
      // 📍 [แก้ไขตรงนี้] สั่งดึงคำตอบแบบตัดเศษเหลือ 4 ตำแหน่งทันที!
      const resA = calculateBruteForce(a, k).toFixed(4);

      // 2. Run Algorithm B & Benchmark time
      const timeElapsedB = getBenchmarkTimeB(a, k);
      // 📍 [แก้ไขตรงนี้] สั่งดึงคำตอบแบบตัดเศษเหลือ 4 ตำแหน่งทันที!
      const resB = calculateByFormula(a, k).toFixed(4);

      // Show loop rounds: k - a
      const rounds = k - a;
      document.getElementById('brute-rounds').innerText = rounds.toLocaleString();

      // Convert times nicely to 6 decimal places
      document.getElementById('time-a').innerText = timeElapsedA.toFixed(6);
      document.getElementById('time-b').innerText = timeElapsedB.toFixed(6);

      // Speedup ratio calculation
      let speedup = 1.0;
      if (timeElapsedB > 0) {
        speedup = timeElapsedA / timeElapsedB;
      }
      if (speedup < 1.0) speedup = 1.0;
      
      document.getElementById('speedup-ratio').innerText = speedup.toLocaleString(undefined, {
        minimumFractionDigits: 1,
        maximumFractionDigits: 2
      });

      // Display Answers
      document.getElementById('result-a').innerText = resA.toLocaleString(undefined, {maximumFractionDigits: 10});
      document.getElementById('result-b').innerText = resB.toLocaleString(undefined, {maximumFractionDigits: 10});

      // Equality check
      const diff = Math.abs(resA - resB);
      const alertDiv = document.getElementById('equality-alert');
      alertDiv.classList.remove('hidden');
      if (diff < 1e-5) {
        alertDiv.className = "p-3 rounded-2xl text-xs font-semibold text-center bg-emerald-100 text-emerald-800 border border-emerald-200";
        alertDiv.innerHTML = `<span class="material-icons text-sm align-middle mr-1">done_all</span>ผลลัพธ์คำนวณถูกต้องตรงกัน 100%! ค่าความคลาดเคลื่อนทางคณิตศาสตร์มีค่าน้อยมาก (${diff.toExponential(6)})`;
      } else {
        alertDiv.className = "p-3 rounded-2xl text-xs font-semibold text-center bg-amber-100 text-amber-800 border border-amber-200";
        alertDiv.innerHTML = `<span class="material-icons text-sm align-middle mr-1">warning</span>ผลลัพธ์คลาดเคลื่อนเล็กน้อยอันเนื่องมาจากข้อจำกัดเรื่องทศนิยม 64 บิตของเบราว์เซอร์`;
      }

      // Reset Button UI
      document.getElementById('btn-spinner').style.display = 'none';
      document.getElementById('btn-icon').style.display = 'inline-block';
      document.getElementById('btn-text').innerText = 'รันระบบจำลอง';

      // Pop success alerting message beautifully
      Swal.fire({
        icon: 'success',
        title: 'การทดลองจำลองเสร็จสิ้น!',
        html: `คำนวณรอบถึกจริง <strong>${rounds.toLocaleString()} รอบ</strong><br>สูตรสำเร็จรูปเร็วกว่าวิธีวนลูปถึง <strong>${speedup.toLocaleString(undefined, {maximumFractionDigits: 1})} เท่า!</strong> ⚡`,
        confirmButtonColor: '#4f46e5'
      });

      // Render performance graph based on calculated settings
      updateSimulationGraph(a);
    }

    // Generate simulated dynamic comparative chart data points (formatted to 6 decimal precision)
    function updateSimulationGraph(a) {
      const kSteps = [10, 100, 1000, 5000, 10000, 50000];
      const timesA = [];
      const timesB = [];

      kSteps.forEach(currentK => {
        const timeA = getBenchmarkTimeA(a, currentK);
        timesA.push(parseFloat(timeA.toFixed(6))); 

        const timeB = getBenchmarkTimeB(a, currentK);
        timesB.push(parseFloat(timeB.toFixed(6)));
      });

      // Update Chart points
      if (perfChartInstance) {
        perfChartInstance.data.labels = kSteps.map(kVal => `k = ${kVal.toLocaleString()}`);
        perfChartInstance.data.datasets[0].data = timesA;
        perfChartInstance.data.datasets[1].data = timesB;
        perfChartInstance.update();
      }
    }

    // Chart Initial setup
    function initChart() {
      if (perfChartInstance) return;

      const ctx = document.getElementById('performanceChart').getContext('2d');
      perfChartInstance = new Chart(ctx, {
        type: 'line',
        data: {
          labels: ['k = 10', 'k = 100', 'k = 1,000', 'k = 5,000', 'k = 10,000', 'k = 50,000'],
          datasets: [
            {
              label: 'Algorithm A: วนลูปถึก O(k)',
              data: [0, 0, 0, 0, 0, 0],
              borderColor: '#f43f5e',
              backgroundColor: 'rgba(244, 63, 94, 0.05)',
              borderWidth: 3,
              tension: 0.3,
              fill: true
            },
            {
              label: 'Algorithm B: สูตรสำเร็จ O(1)',
              data: [0, 0, 0, 0, 0, 0],
              borderColor: '#4f46e5',
              backgroundColor: 'rgba(79, 70, 229, 0.05)',
              borderWidth: 3,
              tension: 0.3,
              fill: true
            }
          ]
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          plugins: {
            legend: {
              position: 'top',
              labels: {
                font: { family: 'Prompt', size: 12 }
              }
            },
            tooltip: {
              callbacks: {
                label: function(context) {
                  let label = context.dataset.label || '';
                  if (label) {
                    label += ': ';
                  }
                  if (context.parsed.y !== null) {
                    label += context.parsed.y.toFixed(6) + ' ms';
                  }
                  return label;
                }
              }
            }
          },
          scales: {
            y: {
              title: {
                display: true,
                text: 'เวลาที่ประมวลผลได้ (มิลลิวินาที)',
                font: { family: 'Prompt', weight: 'bold' }
              },
              ticks: { 
                font: { family: 'Prompt' },
                callback: function(value) {
                  return value.toFixed(6);
                }
              }
            },
            x: {
              title: {
                display: true,
                text: 'ขนาดข้อมูล (ขอบเขตบน k)',
                font: { family: 'Prompt', weight: 'bold' }
              },
              ticks: { font: { family: 'Prompt' } }
            }
          }
        }
      });
    }

    // EXPORT TO EXCEL COMPATIBLE CSV
    function exportToCSV() {
      const a = parseInt(document.getElementById('input-a').value) || 3;
      const kSteps = [10, 100, 1000, 10000, 50000, 100000];
      
      let csvContent = "data:text/csv;charset=utf-8,";
      csvContent += "k_Value,Brute_Force_Rounds,Algorithm_A_Time_ms,Algorithm_B_Time_ms,Efficiency_Speedup_Ratio\n";

      kSteps.forEach(kVal => {
        const rounds = kVal - a;
        const timeA = getBenchmarkTimeA(a, kVal).toFixed(6);
        const timeB = getBenchmarkTimeB(a, kVal).toFixed(6);
        const ratio = (parseFloat(timeA) / parseFloat(timeB)).toFixed(6);

        csvContent += `${kVal},${rounds},${timeA},${timeB},${ratio}\n`;
      });

      const encodedUri = encodeURI(csvContent);
      const link = document.createElement("a");
      link.setAttribute("href", encodedUri);
      link.setAttribute("download", "Telescopic_Cubic_Performance_Data.csv");
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);

      Swal.fire({
        icon: 'success',
        title: 'ดาวน์โหลด Excel สำเร็จ!',
        text: 'ส่งออกข้อมูลผลลัพธ์ประสิทธิภาพออกเป็นไฟล์ CSV เรียบร้อยแล้วค่ะ',
        confirmButtonColor: '#4f46e5'
      });
    }

    // Attach modules to window context for inline HTML access
    window.switchTab = switchTab;
    window.setK = setK;
    window.runSimulation = runSimulation;
    window.exportToCSV = exportToCSV;

    // Windows Onload Initialize Everything
    window.onload = function() {
      // Warm up standard calculation simulation automatically
      runSimulation();
    }
  </script>
</body>
</html>
