<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>싱가포르 나 홀로 여행 스마트 가이드</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Pretendard:wght@400;600;700&display=swap');
        
        body {
            font-family: 'Pretendard', sans-serif;
            background-color: #FDFBF7;
            color: #333;
        }

        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 400px;
        }

        .glass-card {
            background: rgba(255, 255, 255, 0.7);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.3);
            transition: transform 0.3s ease;
        }

        .glass-card:hover {
            transform: translateY(-5px);
        }

        .nav-tab.active {
            background-color: #008080;
            color: white;
        }

        .day-content {
            display: none;
        }

        .day-content.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #FDFBF7;
        }
        ::-webkit-scrollbar-thumb {
            background: #D1D5DB;
            border-radius: 4px;
        }
    </style>
</head>
<body class="p-4 md:p-8">

    <!-- Chosen Palette: Tropical Minimalist (Cream Background, Deep Teal Primary, Soft Coral Accent) -->
    <!-- Application Structure Plan: 
        1. Hero Section: 핵심 요약 및 테마 소개.
        2. Dashboard Section: 국가 정보와 날씨 데이터를 시각화하여 첫인상 결정.
        3. Interactive Itinerary: 탭 인터페이스를 사용하여 3박 4일 일정을 사용자가 선택적으로 탐색. 
        4. Budget Analysis: Chart.js를 이용해 예산 비중을 시각화하여 경제적 판단 지원.
        5. Essential Tips: 법규 및 짐 싸기 팁을 카드 형태로 배치.
        이 구조는 텍스트 위주의 보고서를 직관적인 데이터 대시보드로 변환하여 사용자가 필요한 정보만 빠르게 찾도록 설계되었습니다. -->
    <!-- Visualization & Content Choices: 
        - Budget -> Doughnut Chart (Chart.js) -> 전체 비용 중 항목별 비중 확인.
        - Weather -> Bar Chart (Chart.js) -> 온도 범위 시각화.
        - Timeline -> Vertical Step List -> 동선의 논리적 흐름 표현.
        - Cards -> Hover Effects -> 사용자 인터랙션 유도.
        - NO SVG/Mermaid: 모든 아이콘은 유니코드와 CSS를 활용하여 구현. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <div class="max-w-5xl mx-auto">
        <!-- Header -->
        <header class="mb-12 text-center">
            <h1 class="text-4xl md:text-5xl font-bold text-[#008080] mb-4">🇸🇬 싱가포르 나 홀로 여행 가이드</h1>
            <p class="text-lg text-gray-600">2026.08.25(화) - 08.28(금) | 대학생 실속 압축형</p>
        </header>

        <!-- Intro Section -->
        <section class="mb-12 bg-white rounded-3xl p-6 shadow-sm border border-gray-100">
            <h2 class="text-2xl font-bold mb-4 flex items-center">
                <span class="mr-2">ℹ️</span> 싱가포르 기초 정보
            </h2>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                <div class="p-4 rounded-2xl bg-teal-50 border border-teal-100">
                    <p class="text-sm text-teal-600 mb-1 font-semibold">치안</p>
                    <p class="text-lg font-bold">세계 1위 수준</p>
                </div>
                <div class="p-4 rounded-2xl bg-orange-50 border border-orange-100">
                    <p class="text-sm text-orange-600 mb-1 font-semibold">환율</p>
                    <p class="text-lg font-bold">1 SGD ≈ 1,020원</p>
                </div>
                <div class="p-4 rounded-2xl bg-blue-50 border border-blue-100">
                    <p class="text-sm text-blue-600 mb-1 font-semibold">언어</p>
                    <p class="text-lg font-bold">영어 (소통 원활)</p>
                </div>
                <div class="p-4 rounded-2xl bg-purple-50 border border-purple-100">
                    <p class="text-sm text-purple-600 mb-1 font-semibold">무비자</p>
                    <p class="text-lg font-bold">90일 체류 가능</p>
                </div>
            </div>
            <p class="mt-4 text-gray-600 text-sm leading-relaxed">
                싱가포르는 다민족 국가로 영어 소통이 매우 원활하며, 한국 문화에 대한 호감도가 높습니다. 껌 반입 금지, 지하철 취식 금지 등 강력한 법치주의 국가이므로 주의가 필요합니다.
            </p>
        </section>

        <!-- Weather & Logistics Section -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-12">
            <section class="bg-white rounded-3xl p-6 shadow-sm">
                <h3 class="text-xl font-bold mb-4 flex items-center">🌡️ 8월 말 기온 분석</h3>
                <div class="chart-container">
                    <canvas id="weatherChart"></canvas>
                </div>
                <p class="text-xs text-gray-500 mt-4">건기이지만 스콜이 잦으므로 우산 필수. 실내 에어컨이 매우 강하니 얇은 가디건을 꼭 챙기세요.</p>
            </section>

            <section class="bg-white rounded-3xl p-6 shadow-sm">
                <h3 class="text-xl font-bold mb-4 flex items-center">✈️ 항공 및 숙소 요약</h3>
                <div class="space-y-4">
                    <div class="flex items-start">
                        <div class="bg-gray-100 p-2 rounded-lg mr-3 text-xl">🛫</div>
                        <div>
                            <p class="font-bold">티웨이항공 (직항)</p>
                            <p class="text-sm text-gray-600">₩381,500 | 21:30 도착 - 23:00 출발</p>
                        </div>
                    </div>
                    <div class="flex items-start">
                        <div class="bg-gray-100 p-2 rounded-lg mr-3 text-xl">🏨</div>
                        <div>
                            <p class="font-bold">차이나타운 가성비 호텔</p>
                            <p class="text-sm text-gray-600">3성급 역세권 추천 | MRT 이동 최적화</p>
                        </div>
                    </div>
                    <div class="flex items-start">
                        <div class="bg-gray-100 p-2 rounded-lg mr-3 text-xl">💳</div>
                        <div>
                            <p class="font-bold">현지 교통</p>
                            <p class="text-sm text-gray-600">트래블월렛/로그 카드 태그 결제 (충전 불필요)</p>
                        </div>
                    </div>
                </div>
            </section>
        </div>

        <!-- Interactive Itinerary Section -->
        <section class="mb-12">
            <h2 class="text-2xl font-bold mb-6 flex items-center">🗺️ 3박 4일 실전 라우팅</h2>
            <div class="flex overflow-x-auto space-x-2 mb-6 pb-2">
                <button onclick="showDay(1)" class="nav-tab active px-6 py-2 rounded-full border border-gray-200 font-semibold transition-all">DAY 1</button>
                <button onclick="showDay(2)" class="nav-tab px-6 py-2 rounded-full border border-gray-200 font-semibold transition-all">DAY 2</button>
                <button onclick="showDay(3)" class="nav-tab px-6 py-2 rounded-full border border-gray-200 font-semibold transition-all">DAY 3</button>
                <button onclick="showDay(4)" class="nav-tab px-6 py-2 rounded-full border border-gray-200 font-semibold transition-all">DAY 4</button>
            </div>

            <div id="day-1" class="day-content active bg-white rounded-3xl p-8 shadow-sm">
                <h3 class="text-xl font-bold text-[#008080] mb-4">1일 차: 입국 및 안착</h3>
                <div class="border-l-2 border-dashed border-teal-200 ml-3 space-y-8">
                    <div class="relative pl-8">
                        <span class="absolute left-[-9px] top-0 w-4 h-4 bg-teal-500 rounded-full"></span>
                        <p class="text-sm text-teal-600 font-bold mb-1">21:30</p>
                        <p class="font-bold">창이 공항 도착</p>
                        <p class="text-sm text-gray-600">그랩(Grab) 택시 이용 시내 이동 (약 25분 / 30 SGD)</p>
                    </div>
                    <div class="relative pl-8">
                        <span class="absolute left-[-9px] top-0 w-4 h-4 bg-gray-300 rounded-full"></span>
                        <p class="text-sm text-teal-600 font-bold mb-1">22:30</p>
                        <p class="font-bold">호텔 체크인</p>
                        <p class="text-sm text-gray-600">숙소 인근 편의점 이용 및 휴식</p>
                    </div>
                </div>
            </div>

            <div id="day-2" class="day-content bg-white rounded-3xl p-8 shadow-sm">
                <h3 class="text-xl font-bold text-[#008080] mb-4">2일 차: 시내 정복 및 야경</h3>
                <div class="border-l-2 border-dashed border-teal-200 ml-3 space-y-8">
                    <div class="relative pl-8">
                        <span class="absolute left-[-9px] top-0 w-4 h-4 bg-teal-500 rounded-full"></span>
                        <p class="text-sm text-teal-600 font-bold mb-1">10:00</p>
                        <p class="font-bold">야쿤 카야 토스트 (본점)</p>
                        <p class="text-sm text-gray-600">카야 토스트 세트 (6.5 SGD)</p>
                    </div>
                    <div class="relative pl-8">
                        <span class="absolute left-[-9px] top-0 w-4 h-4 bg-gray-300 rounded-full"></span>
                        <p class="text-sm text-teal-600 font-bold mb-1">14:00</p>
                        <p class="font-bold">오차드 로드 쇼핑몰 피서</p>
                        <p class="text-sm text-gray-600">에어컨 빵빵한 아이온 오차드에서 치킨라이스 점심</p>
                    </div>
                    <div class="relative pl-8">
                        <span class="absolute left-[-9px] top-0 w-4 h-4 bg-gray-300 rounded-full"></span>
                        <p class="text-sm text-teal-600 font-bold mb-1">19:30</p>
                        <p class="font-bold">리버 크루즈 & 뉴튼 호커센터</p>
                        <p class="text-sm text-gray-600">1인 칠리크랩 세트(45 SGD)로 완벽한 저녁</p>
                    </div>
                </div>
            </div>

            <div id="day-3" class="day-content bg-white rounded-3xl p-8 shadow-sm">
                <h3 class="text-xl font-bold text-[#008080] mb-4">3일 차: 테마파크 정복의 날</h3>
                <div class="border-l-2 border-dashed border-teal-200 ml-3 space-y-8">
                    <div class="relative pl-8">
                        <span class="absolute left-[-9px] top-0 w-4 h-4 bg-teal-500 rounded-full"></span>
                        <p class="text-sm text-teal-600 font-bold mb-1">10:00</p>
                        <p class="font-bold">유니버셜 스튜디오 싱가포르 (USS)</p>
                        <p class="text-sm text-gray-600">'싱글 라이더' 줄 활용하여 무한 탑승 (목요일 눈치싸움 성공)</p>
                    </div>
                    <div class="relative pl-8">
                        <span class="absolute left-[-9px] top-0 w-4 h-4 bg-gray-300 rounded-full"></span>
                        <p class="text-sm text-teal-600 font-bold mb-1">16:30</p>
                        <p class="font-bold">송파 바쿠테</p>
                        <p class="text-sm text-gray-600">뜨끈한 갈비탕으로 체력 충전 (리필 가능)</p>
                    </div>
                    <div class="relative pl-8">
                        <span class="absolute left-[-9px] top-0 w-4 h-4 bg-gray-300 rounded-full"></span>
                        <p class="text-sm text-teal-600 font-bold mb-1">19:45</p>
                        <p class="font-bold">슈퍼트리 쇼 (가든 랩소디)</p>
                        <p class="text-sm text-gray-600">무료 야외 공연. 잔디밭에 누워 관람 필수</p>
                    </div>
                </div>
            </div>

            <div id="day-4" class="day-content bg-white rounded-3xl p-8 shadow-sm">
                <h3 class="text-xl font-bold text-[#008080] mb-4">4일 차: 기념품 및 귀국</h3>
                <div class="border-l-2 border-dashed border-teal-200 ml-3 space-y-8">
                    <div class="relative pl-8">
                        <span class="absolute left-[-9px] top-0 w-4 h-4 bg-teal-500 rounded-full"></span>
                        <p class="text-sm text-teal-600 font-bold mb-1">10:00</p>
                        <p class="font-bold">하지 레인 & 아랍 스트리트</p>
                        <p class="text-sm text-gray-600">이국적인 벽화와 술탄 모스크 배경 인생샷 촬영</p>
                    </div>
                    <div class="relative pl-8">
                        <span class="absolute left-[-9px] top-0 w-4 h-4 bg-gray-300 rounded-full"></span>
                        <p class="text-sm text-teal-600 font-bold mb-1">12:00</p>
                        <p class="font-bold">바샤 커피 (Bacha Coffee)</p>
                        <p class="text-sm text-gray-600">고급 커피 시음 및 지인 선물 드립백 구매</p>
                    </div>
                    <div class="relative pl-8">
                        <span class="absolute left-[-9px] top-0 w-4 h-4 bg-gray-300 rounded-full"></span>
                        <p class="text-sm text-teal-600 font-bold mb-1">20:00</p>
                        <p class="font-bold">쥬얼 창이공항 레인 보텍스</p>
                        <p class="text-sm text-gray-600">세계 최고 인공 폭포 감상 후 밤 비행기 탑승</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Budget Section -->
        <section class="bg-white rounded-3xl p-8 shadow-sm mb-12">
            <h2 class="text-2xl font-bold mb-6 flex items-center">💰 예산 요약 (1인 기준)</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-center">
                <div class="chart-container">
                    <canvas id="budgetChart"></canvas>
                </div>
                <div>
                    <div class="space-y-3">
                        <div class="flex justify-between border-b pb-2">
                            <span>항공권</span><span class="font-bold text-[#008080]">₩381,500</span>
                        </div>
                        <div class="flex justify-between border-b pb-2">
                            <span>숙박(3박)</span><span class="font-bold text-[#008080]">₩450,000</span>
                        </div>
                        <div class="flex justify-between border-b pb-2">
                            <span>식비</span><span class="font-bold text-[#008080]">₩150,000</span>
                        </div>
                        <div class="flex justify-between border-b pb-2">
                            <span>활동/교통</span><span class="font-bold text-[#008080]">₩148,000</span>
                        </div>
                        <div class="flex justify-between border-b pb-2">
                            <span>기념품</span><span class="font-bold text-[#008080]">₩100,000</span>
                        </div>
                        <div class="flex justify-between pt-4 text-xl">
                            <span class="font-bold">합계</span><span class="font-extrabold text-[#E2725B]">약 1,229,500원</span>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Packing & Laws Checklist -->
        <section class="mb-12">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <div class="bg-teal-50 rounded-3xl p-6 border border-teal-100">
                    <h3 class="text-lg font-bold mb-4">🎒 필수 준비물</h3>
                    <ul class="space-y-2 text-gray-700">
                        <li class="flex items-center"><span class="mr-2">✔️</span> 얇은 가디건 (에어컨 방어)</li>
                        <li class="flex items-center"><span class="mr-2">✔️</span> 3단 암막 양우산 (태양 & 스콜)</li>
                        <li class="flex items-center"><span class="mr-2">✔️</span> 트래블월렛/로그 카드</li>
                        <li class="flex items-center"><span class="mr-2">✔️</span> 싱가포르 SG 입국신고서 (온라인)</li>
                    </ul>
                </div>
                <div class="bg-red-50 rounded-3xl p-6 border border-red-100">
                    <h3 class="text-lg font-bold mb-4">🚫 주의 사항 (벌금 제도)</h3>
                    <ul class="space-y-2 text-gray-700">
                        <li class="flex items-center"><span class="mr-2">⚠️</span> 껌 반입 및 씹기 금지</li>
                        <li class="flex items-center"><span class="mr-2">⚠️</span> 지하철 내 음식/물 취식 금지</li>
                        <li class="flex items-center"><span class="mr-2">⚠️</span> 무단횡단 절대 금지</li>
                        <li class="flex items-center"><span class="mr-2">⚠️</span> 쓰레기 투기 금지</li>
                    </ul>
                </div>
            </div>
        </section>

        <footer class="text-center text-gray-400 text-sm py-8">
            &copy; 2026 싱가포르 나 홀로 여행 가이드 | 본 프로그램은 실전 최적화 데이터를 기반으로 합니다.
        </footer>
    </div>

    <script>
        // Tab Navigation
        function showDay(dayNum) {
            document.querySelectorAll('.day-content').forEach(content => content.classList.remove('active'));
            document.querySelectorAll('.nav-tab').forEach(tab => tab.classList.remove('active'));
            
            document.getElementById(`day-${dayNum}`).classList.add('active');
            event.target.classList.add('active');
        }

        // Weather Chart
        const weatherCtx = document.getElementById('weatherChart').getContext('2d');
        new Chart(weatherCtx, {
            type: 'bar',
            data: {
                labels: ['최저 기온', '최고 기온'],
                datasets: [{
                    label: '온도 (°C)',
                    data: [25, 32],
                    backgroundColor: ['#AEEEEE', '#E2725B'],
                    borderRadius: 10,
                    barThickness: 40
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { display: false }
                },
                scales: {
                    y: { beginAtZero: false, min: 20, max: 40 }
                }
            }
        });

        // Budget Chart
        const budgetCtx = document.getElementById('budgetChart').getContext('2d');
        new Chart(budgetCtx, {
            type: 'doughnut',
            data: {
                labels: ['항공', '숙박', '식비', '액티비티/교통', '기념품'],
                datasets: [{
                    data: [381500, 450000, 150000, 148000, 100000],
                    backgroundColor: ['#008080', '#20B2AA', '#E2725B', '#FFA07A', '#D1D5DB'],
                    borderWidth: 0,
                    hoverOffset: 10
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { position: 'bottom', labels: { boxWidth: 12, padding: 20 } }
                }
            }
        });
    </script>
</body>
</html>
