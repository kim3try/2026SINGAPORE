
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>싱가포르 3박 4일 스마트 여행 대시보드</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Pretendard:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Pretendard', sans-serif; background-color: #fafaf9; }
        .chart-container { 
            position: relative; 
            width: 100%; 
            max-width: 500px; 
            margin-left: auto; 
            margin-right: auto; 
            height: 300px; 
            max-height: 350px; 
        }
    </style>
</head>
<body class="text-zinc-800 pb-12">

    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 pt-8">
        <!-- Header -->
        <header class="bg-white rounded-3xl p-6 mb-8 shadow-sm border border-zinc-100 flex flex-col md:flex-row justify-between items-start md:items-center gap-6">
            <div>
                <div class="flex items-center gap-2 mb-1">
                    <span class="text-2xl">🇸🇬</span>
                    <h1 class="text-2xl font-extrabold text-teal-700 tracking-tight">싱가포르 나 홀로 자유여행</h1>
                </div>
                <p class="text-zinc-400 text-sm font-medium">2026.08.25 (화) - 08.28 (금) | 3박 4일 일정</p>
            </div>
            <div class="flex gap-4">
                <div class="text-right">
                    <p class="text-[10px] text-zinc-400 font-bold uppercase tracking-widest">Weather (Aug)</p>
                    <p class="text-lg font-extrabold text-orange-500">31°C 건기</p>
                </div>
                <div class="h-10 w-[1px] bg-zinc-100"></div>
                <div class="text-right">
                    <p class="text-[10px] text-zinc-400 font-bold uppercase tracking-widest">Exchange Rate</p>
                    <p class="text-lg font-extrabold text-zinc-700">1 SGD ≈ 1,020원</p>
                </div>
            </div>
        </header>

        <!-- Section: Essential Insight -->
        <section class="mb-10">
            <div class="mb-6">
                <h2 class="text-xl font-bold flex items-center gap-2">
                    <span class="p-1.5 bg-teal-100 text-teal-700 rounded-lg">📌</span> 싱가포르 입국 전 필수 가이드
                </h2>
                <p class="text-zinc-500 text-sm mt-1">안전하고 쾌적한 여행을 위해 꼭 알아두어야 할 싱가포르의 기본 정보입니다.</p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <div class="bg-white p-5 rounded-2xl border border-zinc-100 shadow-sm hover:shadow-md transition-shadow">
                    <h3 class="font-bold text-teal-700 mb-2 flex items-center gap-2">🪪 국가 및 법률</h3>
                    <p class="text-xs text-zinc-600 leading-relaxed">
                        다민족(중국, 말레이, 인도)이 공존하는 영어 통용 국가입니다. 특히 **껌 반입 금지법**은 지하철 센서 오작동 대란을 막기 위해 1992년 제정되었습니다. 가방에 껌이 없도록 확인하세요!
                    </p>
                </div>
                <div class="bg-white p-5 rounded-2xl border border-zinc-100 shadow-sm hover:shadow-md transition-shadow">
                    <h3 class="font-bold text-orange-600 mb-2 flex items-center gap-2">☀️ 8월 말 날씨 & 습도</h3>
                    <p class="text-xs text-zinc-600 leading-relaxed">
                        화창한 **건기**에 속하며 스콜(소나기)이 짧게 지나갑니다. 습도는 평균 80%로 높지만 바람이 불어 야외 활동이 가능합니다. **에어컨이 매우 강한 실내**를 대비해 얇은 겉옷은 필수입니다.
                    </p>
                </div>
                <div class="bg-white p-5 rounded-2xl border border-zinc-100 shadow-sm hover:shadow-md transition-shadow">
                    <h3 class="font-bold text-blue-600 mb-2 flex items-center gap-2">💳 교통 & 결제</h3>
                    <p class="text-xs text-zinc-600 leading-relaxed">
                        환전보다 **컨택리스 신용카드(트래블로그, 트래블월렛 등)**가 월등히 편리합니다. MRT와 버스 모두 한국 카드를 찍고 즉시 탑승할 수 있으며, 택시는 'Grab' 앱을 추천합니다.
                    </p>
                </div>
            </div>
        </section>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-10">
            <!-- Left: Itinerary Timeline (2/3 width) -->
            <div class="lg:col-span-2">
                <div class="mb-6">
                    <h2 class="text-xl font-bold flex items-center gap-2">
                        <span class="p-1.5 bg-zinc-200 text-zinc-700 rounded-lg">🗺️</span> 인터랙티브 여행 로드맵
                    </h2>
                    <p class="text-zinc-500 text-sm mt-1">대학생 1인 기준, 가성비와 동선 효율을 극대화한 3박 4일 일정입니다. (지정한 숙소 기준)</p>
                </div>

                <div class="bg-white rounded-3xl p-6 shadow-sm border border-zinc-100">
                    <!-- Day Selector -->
                    <div class="flex p-1.5 bg-zinc-100 rounded-2xl mb-8 space-x-1">
                        <button onclick="changeDay(1)" id="day1-btn" class="flex-1 py-2.5 text-sm font-bold rounded-xl transition-all bg-white text-teal-700 shadow-sm">DAY 1</button>
                        <button onclick="changeDay(2)" id="day2-btn" class="flex-1 py-2.5 text-sm font-bold rounded-xl transition-all text-zinc-500">DAY 2</button>
                        <button onclick="changeDay(3)" id="day3-btn" class="flex-1 py-2.5 text-sm font-bold rounded-xl transition-all text-zinc-500">DAY 3</button>
                        <button onclick="changeDay(4)" id="day4-btn" class="flex-1 py-2.5 text-sm font-bold rounded-xl transition-all text-zinc-500">DAY 4</button>
                    </div>

                    <!-- Timeline Content -->
                    <div id="timeline-box" class="space-y-6 min-h-[400px]">
                        <!-- JS renders content here -->
                    </div>
                </div>
            </div>

            <!-- Right: Budget & Packing List (1/3 width) -->
            <div class="space-y-10">
                <!-- Budget Analysis -->
                <section>
                    <div class="mb-6">
                        <h2 class="text-xl font-bold flex items-center gap-2">
                            <span class="p-1.5 bg-emerald-100 text-emerald-700 rounded-lg">💰</span> 현실 예산 분석
                        </h2>
                        <p class="text-zinc-500 text-sm mt-1">실제 결제 시 수하물 추가, 수수료 및 비상시를 대비해 여유 있게 책정한 예산입니다.</p>
                    </div>
                    <div class="bg-white rounded-3xl p-6 shadow-sm border border-zinc-100">
                        <div class="chart-container">
                            <canvas id="budgetChart"></canvas>
                        </div>
                        <div class="mt-6 pt-6 border-t border-zinc-50">
                            <div class="flex justify-between text-xs font-bold mb-2">
                                <span class="text-zinc-400 uppercase tracking-tighter">항목별 예상액</span>
                                <span class="text-teal-700">총 1,380,000원</span>
                            </div>
                            <ul class="space-y-2">
                                <li class="flex justify-between text-sm">
                                    <span class="text-zinc-500">✈️ 항공권 </span>
                                    <span class="font-bold text-zinc-700">400,000원</span>
                                </li>
                                <li class="flex justify-between text-sm">
                                    <span class="text-zinc-500">🏨 숙박 예산 (3성 비즈니스 호텔 평균 기준)</span>
                                    <span class="font-bold text-zinc-700">450,000원</span>
                                </li>
                                <li class="flex justify-between text-sm">
                                    <span class="text-zinc-500">🍱 식비 (칠리크랩 및 현지 먹방 넉넉히)</span>
                                    <span class="font-bold text-zinc-700">220,000원</span>
                                </li>
                                <li class="flex justify-between text-sm">
                                    <span class="text-zinc-500">🎟️ 액티비티 (유니버셜+리버크루즈)</span>
                                    <span class="font-bold text-zinc-700">110,000원</span>
                                </li>
                                <li class="flex justify-between text-sm">
                                    <span class="text-zinc-500">🚕 교통비 (대중교통 및 비상 그랩 대비)</span>
                                    <span class="font-bold text-zinc-700">80,000원</span>
                                </li>
                                <li class="flex justify-between text-sm">
                                    <span class="text-zinc-500">🛍️ 쇼핑/선물 (바샤커피, 해피히포 등)</span>
                                    <span class="font-bold text-zinc-700">120,000원</span>
                                </li>
                            </ul>
                        </div>
                    </div>
                </section>

                <!-- Essential Packing Checklist Section -->
                <section>
                    <div class="mb-6">
                        <h2 class="text-xl font-bold flex items-center gap-2">
                            <span class="p-1.5 bg-purple-100 text-purple-700 rounded-lg">🧳</span> 실전 준비물 체크리스트
                        </h2>
                    </div>
                    <div class="bg-gradient-to-br from-purple-50 to-white rounded-3xl p-6 border border-purple-100">
                        <ul class="space-y-4">
                            <li class="flex gap-3">
                                <span class="text-lg">💳</span>
                                <div>
                                    <p class="text-sm font-bold text-purple-900">컨택리스 결제 카드</p>
                                    <p class="text-xs text-purple-600">트래블로그 또는 트래블월렛 필수 (MRT 탑승용)</p>
                                </div>
                            </li>
                            <li class="flex gap-3">
                                <span class="text-lg">🧥</span>
                                <div>
                                    <p class="text-sm font-bold text-purple-900">얇은 가디건 또는 셔츠</p>
                                    <p class="text-xs text-purple-600">냉동고 수준의 실내 강한 에어컨 방어용</p>
                                </div>
                            </li>
                            <li class="flex gap-3">
                                <span class="text-lg">🌂</span>
                                <div>
                                    <p class="text-sm font-bold text-purple-900">3단 암막 양우산</p>
                                    <p class="text-xs text-purple-600">뜨거운 한낮 햇빛과 오후 짧은 스콜 동시 방지</p>
                                </div>
                            </li>
                            <li class="flex gap-3">
                                <span class="text-lg">🚫</span>
                                <div>
                                    <p class="text-sm font-bold text-purple-900">껌 소지 금지</p>
                                    <p class="text-xs text-purple-600">가방 구석에 껌이나 츄잉껌이 없는지 사전 확인</p>
                                </div>
                            </li>
                        </ul>
                    </div>
                </section>
            </div>
        </div>
    </div>

    <script>
        const timelineData = {
            1: [
                { time: "21:30", title: "싱가포르 창이 공항 도착", desc: "그랩(Grab) 또는 공식 택시로 예약하실 숙소로 이동 (약 30 SGD 소요)", cost: "30,000원" },
                { time: "22:30", title: "숙소 체크인 및 휴식", desc: "지정하신 숙소에 안전하게 체크인 후 휴식", cost: "-" }
            ],
            2: [
                { time: "10:00", title: "야쿤 카야 토스트 본점", desc: "바삭한 토스트와 수란 세트로 든든한 아침 식사", cost: "7,000원" },
                { time: "11:30", title: "오차드 로드 아이온 몰", desc: "한낮 폭염 대피용 에어컨 빵빵한 쇼핑몰 투어", cost: "-" },
                { time: "17:00", title: "멀라이언 파크 인증샷", desc: "머라이언 동상 앞 입벌리기 시그니처 사진 촬영 (입장 무료)", cost: "-" },
                { time: "19:30", title: "클락 키 리버 크루즈", desc: "강바람을 맞으며 즐기는 환상적인 도심 야경 투어", cost: "18,000원" },
                { time: "20:30", title: "뉴튼 호커센터 (칠리크랩)", desc: "1인 세트로 가성비 있게 싱가포르 필수 음식인 칠리크랩 정복", cost: "46,000원" }
            ],
            3: [
                { time: "10:00", title: "유니버셜 스튜디오 싱가포르", desc: "목요일 평일 찬스! '싱글 라이더' 전용 대기줄로 트랜스포머/머미 롤러코스터 무한 탑승", cost: "80,000원" },
                { time: "16:30", title: "송파 바쿠테 본점", desc: "한국식 갈비탕과 싱크로율 95%인 보양식, 뜨끈한 국물 무한 리필", cost: "10,000원" },
                { time: "19:00", title: "가든스 바이 더 베이", desc: "슈퍼트리 쇼 '가든 랩소디' 감상 (입장 무료, 잔디밭 누워보기 권장)", cost: "-" }
            ],
            4: [
                { time: "10:00", title: "아랍 스트리트 & 하지 레인", desc: "황금 돔 사원과 감각적인 벽화 골목을 배경으로 자유롭게 사진 촬영", cost: "-" },
                { time: "12:00", title: "바샤 커피 (마리나 샌즈몰)", desc: "고급 크루아상 & 커피 테이크아웃 체험 및 선물용 제품 탐색", cost: "18,000원" },
                { time: "19:30", title: "쥬얼 창이 레인 보텍스", desc: "공항 내 위치한 세계 최대 실내 폭포 감상 및 면세점 기념품 쇼핑", cost: "선택적" },
                { time: "23:00", title: "귀국행 비행기 탑승", desc: "3박 4일 전체 일정 종료 후 한국행 출발", cost: "-" }
            ]
        };

        function renderTimeline(day) {
            const container = document.getElementById('timeline-box');
            container.innerHTML = '';
            
            timelineData[day].forEach(item => {
                const itemDiv = document.createElement('div');
                itemDiv.className = 'flex gap-4 group';
                itemDiv.innerHTML = `
                    <div class="flex flex-col items-center">
                        <div class="w-2.5 h-2.5 rounded-full bg-teal-600 ring-4 ring-teal-50"></div>
                        <div class="flex-1 w-0.5 bg-zinc-100 my-2"></div>
                    </div>
                    <div class="pb-6">
                        <span class="text-[10px] font-bold text-teal-600 bg-teal-50 px-2 py-0.5 rounded-full uppercase tracking-widest">${item.time}</span>
                        <h4 class="text-sm font-extrabold text-zinc-800 mt-1">${item.title}</h4>
                        <p class="text-xs text-zinc-500 mt-1 leading-relaxed">${item.desc}</p>
                        ${item.cost !== '-' ? `<span class="inline-block mt-2 text-[10px] text-zinc-400 font-bold">예상 비용: ${item.cost}</span>` : ''}
                    </div>
                `;
                container.appendChild(itemDiv);
            });
        }

        function changeDay(day) {
            [1, 2, 3, 4].forEach(d => {
                const btn = document.getElementById(`day${d}-btn`);
                btn.className = "flex-1 py-2.5 text-sm font-bold rounded-xl transition-all text-zinc-500";
            });
            const activeBtn = document.getElementById(`day${day}-btn`);
            activeBtn.className = "flex-1 py-2.5 text-sm font-bold rounded-xl transition-all bg-white text-teal-700 shadow-sm";
            renderTimeline(day);
        }

        function initChart() {
            const ctx = document.getElementById('budgetChart').getContext('2d');
            new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['항공권', '숙박비 (3박)', '식비', '기타 (교통/액티비티/쇼핑)'],
                    datasets: [{
                        data: [29, 33, 16, 22], // 40만, 45만, 22만, 31만
                        backgroundColor: ['#0d9488', '#0ea5e9', '#f97316', '#a855f7'],
                        borderWidth: 0,
                        hoverOffset: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { position: 'bottom', labels: { boxWidth: 12, font: { size: 10, weight: 'bold' } } }
                    },
                    cutout: '70%'
                }
            });
        }

        document.addEventListener('DOMContentLoaded', () => {
            renderTimeline(1);
            initChart();
        });
    </script>
</body>
</html>
