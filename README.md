```html
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>政治獻金透明化儀表板 | 掌握民主的錢流</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@300;400;500;700&display=swap');
        
        body {
            font-family: 'Noto Sans TC', sans-serif;
            background-color: #f8fafc;
            color: #1e293b;
        }

        .hero-gradient {
            background: linear-gradient(135deg, #1e3a8a 0%, #0f172a 100%);
        }

        .card-shadow {
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .card-shadow:hover {
            transform: translateY(-4px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
        }

        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #f1f1f1;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 10px;
        }

        /* 簡單的視圖切換動畫 */
        .view-content {
            display: none;
        }
        .view-content.active {
            display: block;
            animation: fadeIn 0.4s ease-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>

    <!-- 導航欄 -->
    <nav class="sticky top-0 z-50 bg-white/80 backdrop-blur-md border-b border-slate-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16 items-center">
                <div class="flex items-center cursor-pointer" onclick="switchView('landing')">
                    <i data-lucide="shield-check" class="text-blue-700 mr-2"></i>
                    <span class="text-xl font-bold tracking-tight text-slate-800">透明監督儀表板</span>
                </div>
                <div class="hidden md:flex space-x-8">
                    <a href="#" onclick="switchView('landing')" class="text-slate-600 hover:text-blue-700 font-medium">首頁</a>
                    <a href="#" onclick="switchView('results')" class="text-slate-600 hover:text-blue-700 font-medium">數據庫</a>
                    <a href="#" class="text-slate-600 hover:text-blue-700 font-medium">關於計畫</a>
                </div>
                <button onclick="switchView('results')" class="bg-blue-700 text-white px-4 py-2 rounded-lg text-sm font-medium hover:bg-blue-800 transition">
                    立即查詢
                </button>
            </div>
        </div>
    </nav>

    <!-- 頁面 1: Landing Page -->
    <main id="view-landing" class="view-content active">
        <!-- Hero Section -->
        <section class="hero-gradient text-white py-20 px-4">
            <div class="max-w-4xl mx-auto text-center">
                <h1 class="text-4xl md:text-6xl font-bold mb-6 leading-tight">
                    金權背後的真相：<br><span class="text-blue-400">誰在資助我們的代議士？</span>
                </h1>
                <p class="text-lg md:text-xl text-slate-300 mb-10 leading-relaxed">
                    政治獻金不只是數字，更是權力的投射。透過數據透明化，我們能看見候選人的經費來源——是來自基層支持，還是特定企業的重金傾注？這是守護民主的第一道防線。
                </p>
                
                <!-- Search Input CTA -->
                <div class="max-w-2xl mx-auto relative">
                    <input type="text" id="landing-search" placeholder="輸入候選人姓名或政黨... (例如：柯建銘)" 
                        class="w-full px-6 py-4 rounded-full bg-white text-slate-900 text-lg shadow-2xl focus:ring-4 focus:ring-blue-500/50 outline-none">
                    <button onclick="handleHeroSearch()" class="absolute right-2 top-2 bg-blue-700 text-white px-8 py-2.5 rounded-full font-bold hover:bg-blue-800">
                        搜尋
                    </button>
                </div>

                <!-- 範例查詢 -->
                <div class="mt-6 flex flex-wrap justify-center gap-3">
                    <span class="text-slate-400 text-sm py-1">熱門查詢：</span>
                    <button onclick="quickSearch('民主進步黨')" class="text-xs bg-white/10 hover:bg-white/20 px-3 py-1 rounded-full border border-white/20 transition">民主進步黨</button>
                    <button onclick="quickSearch('中國國民黨')" class="text-xs bg-white/10 hover:bg-white/20 px-3 py-1 rounded-full border border-white/20 transition">中國國民黨</button>
                    <button onclick="quickSearch('企業捐贈')" class="text-xs bg-white/10 hover:bg-white/20 px-3 py-1 rounded-full border border-white/20 transition">企業捐贈前十名</button>
                </div>
            </div>
        </section>

        <!-- 編輯精選案例 Editor's Picks -->
        <section class="max-w-7xl mx-auto py-20 px-4">
            <div class="flex items-center mb-12">
                <div class="h-1 w-12 bg-blue-700 mr-4"></div>
                <h2 class="text-3xl font-bold text-slate-800">編輯精選分析</h2>
            </div>
            
            <div class="grid md:grid-cols-3 gap-8">
                <!-- Case 1 -->
                <div class="bg-white rounded-2xl p-6 card-shadow border border-slate-100">
                    <div class="w-12 h-12 bg-blue-100 text-blue-700 rounded-full flex items-center justify-center mb-4">
                        <i data-lucide="trending-up"></i>
                    </div>
                    <h3 class="text-xl font-bold mb-2">高額企業捐贈者</h3>
                    <p class="text-slate-600 mb-4">分析本屆選舉中，企業捐贈比例超過 50% 的候選人。其背後的產業與政策傾向是否相關？</p>
                    <button onclick="switchView('results')" class="text-blue-700 font-semibold flex items-center hover:underline">
                        查看數據 <i data-lucide="chevron-right" class="ml-1 w-4 h-4"></i>
                    </button>
                </div>
                <!-- Case 2 -->
                <div class="bg-white rounded-2xl p-6 card-shadow border border-slate-100">
                    <div class="w-12 h-12 bg-purple-100 text-purple-700 rounded-full flex items-center justify-center mb-4">
                        <i data-lucide="users"></i>
                    </div>
                    <h3 class="text-xl font-bold mb-2">小額捐款影響力</h3>
                    <p class="text-slate-600 mb-4">哪些候選人主要是依賴個人小額捐款？這代表了更廣泛的基層民意，還是募款策略的差異？</p>
                    <button onclick="switchView('results')" class="text-blue-700 font-semibold flex items-center hover:underline">
                        查看列表 <i data-lucide="chevron-right" class="ml-1 w-4 h-4"></i>
                    </button>
                </div>
                <!-- Case 3 -->
                <div class="bg-white rounded-2xl p-6 card-shadow border border-slate-100">
                    <div class="w-12 h-12 bg-amber-100 text-amber-700 rounded-full flex items-center justify-center mb-4">
                        <i data-lucide="bar-chart-3"></i>
                    </div>
                    <h3 class="text-xl font-bold mb-2">得票成本計算</h3>
                    <p class="text-slate-600 mb-4">將總支出除以得票數，揭露每一張選票背後的「金錢成本」。高支出的效益真的比較高嗎？</p>
                    <button onclick="switchView('results')" class="text-blue-700 font-semibold flex items-center hover:underline">
                        深度排行 <i data-lucide="chevron-right" class="ml-1 w-4 h-4"></i>
                    </button>
                </div>
            </div>
        </section>
    </main>

    <!-- 頁面 2: Results List -->
    <main id="view-results" class="view-content">
        <div class="max-w-7xl mx-auto py-10 px-4">
            
            <!-- Quick Summary Header -->
            <div class="grid grid-cols-1 md:grid-cols-4 gap-4 mb-8">
                <div class="bg-white p-5 rounded-xl border border-slate-200 card-shadow">
                    <p class="text-sm text-slate-500 mb-1">總收錄人數</p>
                    <p class="text-2xl font-bold text-slate-800" id="stat-total">--</p>
                </div>
                <div class="bg-white p-5 rounded-xl border border-slate-200 card-shadow">
                    <p class="text-sm text-slate-500 mb-1">平均企業捐贈率</p>
                    <p class="text-2xl font-bold text-blue-600" id="stat-corp-avg">--</p>
                </div>
                <div class="bg-white p-5 rounded-xl border border-slate-200 card-shadow">
                    <p class="text-sm text-slate-500 mb-1">最高得票數</p>
                    <p class="text-2xl font-bold text-slate-800" id="stat-max-votes">--</p>
                </div>
                <div class="bg-white p-5 rounded-xl border border-slate-200 card-shadow">
                    <p class="text-sm text-slate-500 mb-1">政黨分佈</p>
                    <p class="text-2xl font-bold text-slate-800" id="stat-parties">--</p>
                </div>
            </div>

            <div class="flex flex-col lg:flex-row gap-8">
                <!-- 側邊欄過濾器 -->
                <aside class="w-full lg:w-64 space-y-6">
                    <div>
                        <label class="block text-sm font-bold text-slate-700 mb-2">排序方式</label>
                        <select id="sort-select" onchange="applyFilters()" class="w-full bg-white border border-slate-300 rounded-lg px-3 py-2 outline-none focus:ring-2 focus:ring-blue-500">
                            <option value="votes-desc">得票數 (高到低)</option>
                            <option value="income-desc">總收入 (高到低)</option>
                            <option value="corp-desc">企業捐贈比例 (高到低)</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-bold text-slate-700 mb-2">政黨篩選</label>
                        <div id="party-filters" class="space-y-2">
                            <!-- JS 動態生成 -->
                        </div>
                    </div>
                </aside>

                <!-- 結果列表 -->
                <div class="flex-1">
                    <div class="mb-4 flex justify-between items-center">
                        <h2 class="text-lg font-bold text-slate-700">查詢結果：<span id="results-count" class="text-blue-700">0</span> 筆資料</h2>
                        <div class="flex space-x-2">
                            <input type="text" id="list-search" oninput="applyFilters()" placeholder="搜尋姓名..." class="border border-slate-300 rounded-lg px-3 py-1 text-sm">
                        </div>
                    </div>

                    <!-- 數據卡片容器 -->
                    <div id="results-grid" class="grid gap-4">
                        <!-- JS 動態生成結果卡片 -->
                    </div>

                    <!-- 加載更多 / 分頁 -->
                    <div id="pagination" class="mt-10 flex justify-center pb-10">
                        <button onclick="loadMore()" class="bg-slate-200 hover:bg-slate-300 text-slate-700 px-8 py-3 rounded-full font-medium transition flex items-center">
                            <i data-lucide="refresh-cw" class="w-4 h-4 mr-2"></i> 顯示更多數據
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </main>

    <footer class="bg-slate-900 text-slate-400 py-12 px-4 mt-20">
        <div class="max-w-7xl mx-auto grid md:grid-cols-3 gap-8">
            <div>
                <h4 class="text-white font-bold text-lg mb-4">關於本計畫</h4>
                <p class="text-sm">我們致力於透過公開數據，讓公民更輕易地監督政府運作與政治資金，推動透明、健康的民主社會。</p>
            </div>
            <div>
                <h4 class="text-white font-bold text-lg mb-4">數據來源</h4>
                <p class="text-sm">資料來源：監察院政治獻金公開查閱平臺、中選會選舉資料庫。</p>
            </div>
            <div>
                <h4 class="text-white font-bold text-lg mb-4">聯絡我們</h4>
                <p class="text-sm">如有任何數據錯誤或建議，請聯繫：support@transparency.example</p>
            </div>
        </div>
    </footer>

    <script>
        // 模擬從 A05_basic_all.csv 載入的資料 (由於前端無法直接讀取本地 CSV，這裡放入具代表性的範例資料)
        const mockData = [
            { name: "柯建銘", party: "民主進步黨", district: "新竹市", votes: 90642, rate: "41.33%", income: 51641147, corp_rate: "52.12%", expense: 52187931, gender: "男" },
            { name: "邱志偉", party: "民主進步黨", district: "高雄市", votes: 110819, rate: "63.23%", income: 38603507, corp_rate: "55.03%", expense: 32000000, gender: "男" },
            { name: "董建一", party: "中華民國機車黨", district: "新北市", votes: 3040, rate: "1.92%", income: 260110, corp_rate: "0.00%", expense: 260932, gender: "男" },
            { name: "陳永順", party: "信心希望聯盟", district: "新北市", votes: 4892, rate: "3.13%", income: 1003334, corp_rate: "94.87%", expense: 1016799, gender: "男" },
            { name: "魏揚", party: "軍公教聯盟黨", district: "新竹市", votes: 723, rate: "0.32%", income: 201000, corp_rate: "0.00%", expense: 198000, gender: "男" },
            { name: "蔣萬安", party: "中國國民黨", district: "臺北市", votes: 89673, rate: "46.68%", income: 45000000, corp_rate: "48.20%", expense: 42000000, gender: "男" },
            { name: "吳思瑤", party: "民主進步黨", district: "臺北市", votes: 95951, rate: "50.81%", income: 32000000, corp_rate: "35.50%", expense: 31000000, gender: "女" },
            { name: "賴士葆", party: "中國國民黨", district: "臺北市", votes: 83931, rate: "49.69%", income: 28000000, corp_rate: "60.10%", expense: 27500000, gender: "男" }
        ];

        let filteredData = [...mockData];
        let displayLimit = 5;

        function init() {
            lucide.createIcons();
            renderStats();
            renderPartyFilters();
            applyFilters();
        }

        function switchView(viewId) {
            document.querySelectorAll('.view-content').forEach(v => v.classList.remove('active'));
            document.getElementById(`view-${viewId}`).classList.add('active');
            window.scrollTo(0, 0);
        }

        function handleHeroSearch() {
            const query = document.getElementById('landing-search').value;
            document.getElementById('list-search').value = query;
            switchView('results');
            applyFilters();
        }

        function quickSearch(tag) {
            if (tag === '企業捐贈前十名') {
                document.getElementById('sort-select').value = 'corp-desc';
                document.getElementById('list-search').value = '';
            } else {
                document.getElementById('list-search').value = tag;
            }
            switchView('results');
            applyFilters();
        }

        function renderStats() {
            document.getElementById('stat-total').innerText = mockData.length + " 人";
            const avgCorp = (mockData.reduce((acc, curr) => acc + parseFloat(curr.corp_rate), 0) / mockData.length).toFixed(2);
            document.getElementById('stat-corp-avg').innerText = avgCorp + "%";
            const maxVotes = Math.max(...mockData.map(d => d.votes));
            document.getElementById('stat-max-votes').innerText = maxVotes.toLocaleString();
            const parties = new Set(mockData.map(d => d.party)).size;
            document.getElementById('stat-parties').innerText = parties + " 個政黨";
        }

        function renderPartyFilters() {
            const parties = Array.from(new Set(mockData.map(d => d.party)));
            const container = document.getElementById('party-filters');
            container.innerHTML = parties.map(party => `
                <label class="flex items-center space-x-2 text-sm text-slate-600">
                    <input type="checkbox" value="${party}" onchange="applyFilters()" class="rounded text-blue-700">
                    <span>${party}</span>
                </label>
            `).join('');
        }

        function applyFilters() {
            const searchTerm = document.getElementById('list-search').value.toLowerCase();
            const sortVal = document.getElementById('sort-select').value;
            
            // 獲取選中的政黨
            const checkedParties = Array.from(document.querySelectorAll('#party-filters input:checked')).map(i => i.value);

            filteredData = mockData.filter(d => {
                const matchSearch = d.name.includes(searchTerm) || d.party.includes(searchTerm);
                const matchParty = checkedParties.length === 0 || checkedParties.includes(d.party);
                return matchSearch && matchParty;
            });

            // 排序
            if (sortVal === 'votes-desc') filteredData.sort((a, b) => b.votes - a.votes);
            if (sortVal === 'income-desc') filteredData.sort((a, b) => b.income - a.income);
            if (sortVal === 'corp-desc') filteredData.sort((a, b) => parseFloat(b.corp_rate) - parseFloat(a.corp_rate));

            displayLimit = 5;
            renderResults();
        }

        function loadMore() {
            displayLimit += 5;
            renderResults();
        }

        function renderResults() {
            const grid = document.getElementById('results-grid');
            const counter = document.getElementById('results-count');
            counter.innerText = filteredData.length;

            const toDisplay = filteredData.slice(0, displayLimit);
            
            if (toDisplay.length === 0) {
                grid.innerHTML = '<div class="text-center py-20 text-slate-500">找不到相符的數據</div>';
                return;
            }

            grid.innerHTML = toDisplay.map(d => `
                <div class="bg-white rounded-xl p-5 border border-slate-200 card-shadow flex flex-col md:flex-row md:items-center justify-between gap-4">
                    <div class="flex items-center space-x-4">
                        <div class="w-12 h-12 bg-slate-100 rounded-full flex items-center justify-center text-slate-400">
                            <i data-lucide="user"></i>
                        </div>
                        <div>
                            <div class="flex items-center gap-2">
                                <h3 class="text-lg font-bold text-slate-800">${d.name}</h3>
                                <span class="px-2 py-0.5 bg-blue-100 text-blue-700 text-xs rounded-full font-medium">${d.party}</span>
                            </div>
                            <p class="text-sm text-slate-500">${d.district} • 得票率 ${d.rate}</p>
                        </div>
                    </div>
                    
                    <div class="grid grid-cols-2 md:flex md:space-x-8 text-sm">
                        <div>
                            <p class="text-slate-400 text-xs uppercase font-semibold">總收入</p>
                            <p class="font-bold text-slate-700">$${(d.income / 10000).toFixed(0)} 萬</p>
                        </div>
                        <div>
                            <p class="text-slate-400 text-xs uppercase font-semibold">企業捐贈比</p>
                            <p class="font-bold ${parseFloat(d.corp_rate) > 50 ? 'text-amber-600' : 'text-slate-700'}">${d.corp_rate}</p>
                        </div>
                        <div class="hidden md:block">
                            <p class="text-slate-400 text-xs uppercase font-semibold">得票數</p>
                            <p class="font-bold text-slate-700">${d.votes.toLocaleString()}</p>
                        </div>
                    </div>

                    <button class="bg-slate-50 hover:bg-slate-100 text-slate-600 px-4 py-2 rounded-lg text-sm font-medium transition border border-slate-200">
                        詳情
                    </button>
                </div>
            `).join('');

            lucide.createIcons();

            // 隱藏加載更多按鈕
            const pagination = document.getElementById('pagination');
            if (displayLimit >= filteredData.length) {
                pagination.style.display = 'none';
            } else {
                pagination.style.display = 'flex';
            }
        }

        window.onload = init;
    </script>
</body>
</html>

```
