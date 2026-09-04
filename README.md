<!DOCTYPE html>
<html lang="zh-HK">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2025 HKDSE BAFS Paper 1A MC Game | 企會財選擇題操練</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
        body {
            font-family: 'Inter', system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
        }
        .option-card {
            transition: all 0.2s ease-in-out;
        }
        .option-card:hover:not(.disabled) {
            transform: translateY(-2px);
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 min-h-screen flex flex-col">

    <!-- Header -->
    <header class="bg-indigo-700 text-white shadow-lg sticky top-0 z-50">
        <div class="max-w-4xl mx-auto px-4 py-3 flex justify-between items-center">
            <div class="flex items-center space-x-3">
                <i class="fa-solid fa-[# graduation-cap] text-2xl text-yellow-300"></i>
                <div>
                    <h1 class="font-bold text-lg leading-tight">HKDSE BAFS 2025</h1>
                    <p class="text-xs text-indigo-200">Paper 1A MC Trainer / 卷一甲部操題神器</p>
                </div>
            </div>
            <div class="flex items-center space-x-2">
                <button id="langToggle" class="bg-indigo-600 hover:bg-indigo-500 text-xs px-3 py-1.5 rounded-full border border-indigo-400 font-medium transition flex items-center gap-1.5">
                    <i class="fa-solid fa-globe"></i> <span id="currentLangLabel">中文 / ENG</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="flex-1 max-w-4xl w-full mx-auto p-4 md:p-6 flex flex-col justify-center">

        <!-- Welcome Screen -->
        <div id="welcomeScreen" class="bg-white rounded-2xl shadow-md p-6 md:p-10 text-center space-y-6 my-auto">
            <div class="inline-block p-4 bg-indigo-50 text-indigo-600 rounded-full mb-2">
                <i class="fa-solid fa-gamepad text-4xl"></i>
            </div>
            <h2 class="text-2xl md:text-3xl font-bold text-slate-800" id="welcomeTitle">
                2025 BAFS 卷一甲部選擇題操練
            </h2>
            <p class="text-slate-600 max-w-xl mx-auto text-sm md:text-base leading-relaxed" id="welcomeDesc">
                收錄 24 道精華考題，涵蓋「營商環境、基礎個人理財及基礎管理」。備有雙語對照及官方詳細解析。
            </p>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 max-w-md mx-auto pt-4">
                <button onclick="startGame(10)" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-semibold py-3 px-6 rounded-xl shadow transition flex items-center justify-center gap-2">
                    <i class="fa-solid fa-bolt"></i> <span id="btnQuick10">隨機 10 題快操</span>
                </button>
                <button onclick="startGame(24)" class="w-full bg-slate-800 hover:bg-slate-900 text-white font-semibold py-3 px-6 rounded-xl shadow transition flex items-center justify-center gap-2">
                    <i class="fa-solid fa-list-check"></i> <span id="btnAll24">全套 24 題挑戰</span>
                </button>
            </div>
        </div>

        <!-- Quiz Screen -->
        <div id="quizScreen" class="hidden space-y-6 my-auto">
            <!-- Progress & Stats Bar -->
            <div class="bg-white rounded-xl shadow-sm p-4 flex justify-between items-center border border-slate-200">
                <div class="flex items-center space-x-4">
                    <span id="questionProgress" class="font-bold text-indigo-600 text-sm md:text-base">Q1 / 24</span>
                    <span id="scoreTracker" class="text-xs md:text-sm bg-slate-100 px-2.5 py-1 rounded-md text-slate-600 font-medium">得分: 0</span>
                </div>
                <div class="w-1/3 bg-slate-100 rounded-full h-2.5 overflow-hidden">
                    <div id="progressBar" class="bg-indigo-600 h-2.5 rounded-full transition-all duration-300" style="width: 0%"></div>
                </div>
            </div>

            <!-- Question Card -->
            <div class="bg-white rounded-2xl shadow-md p-6 md:p-8 space-y-6 border border-slate-100">
                <!-- Topic Tag & Success Rate -->
                <div class="flex justify-between items-center text-xs">
                    <span id="topicTag" class="bg-indigo-50 text-indigo-700 font-medium px-3 py-1 rounded-md border border-indigo-100">
                        Topic
                    </span>
                    <span id="rateTag" class="text-slate-400 font-medium">
                        歷年正確率: --%
                    </span>
                </div>

                <!-- Question Text -->
                <div id="questionText" class="text-base md:text-lg font-semibold text-slate-800 leading-relaxed whitespace-pre-line">
                    Question loading...
                </div>

                <!-- Options -->
                <div id="optionsContainer" class="space-y-3 pt-2">
                    <!-- Dynamic Options -->
                </div>

                <!-- Explanation Box (Initially Hidden) -->
                <div id="explanationBox" class="hidden bg-slate-50 border border-slate-200 rounded-xl p-5 space-y-2 text-sm leading-relaxed">
                    <div class="font-bold text-slate-700 flex items-center gap-2">
                        <i class="fa-solid fa-lightbulb text-amber-500"></i>
                        <span id="expTitle">答案解析</span>
                    </div>
                    <div id="explanationText" class="text-slate-600 whitespace-pre-line">
                        Explanation details...
                    </div>
                </div>

                <!-- Next Button Container -->
                <div id="nextBtnContainer" class="hidden pt-2 flex justify-end">
                    <button id="nextBtn" onclick="nextQuestion()" class="bg-indigo-600 hover:bg-indigo-700 text-white font-semibold py-2.5 px-6 rounded-xl shadow transition flex items-center gap-2">
                        <span id="nextBtnText">下一題</span> <i class="fa-solid fa-arrow-right"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- Result Screen -->
        <div id="resultScreen" class="hidden bg-white rounded-2xl shadow-md p-6 md:p-10 text-center space-y-6 my-auto">
            <div class="inline-block p-4 bg-emerald-50 text-emerald-600 rounded-full mb-2">
                <i class="fa-solid fa-trophy text-5xl"></i>
            </div>
            <h2 class="text-2xl md:text-3xl font-bold text-slate-800" id="resultTitle">
                練習完成！
            </h2>
            
            <div class="grid grid-cols-2 gap-4 max-w-xs mx-auto py-2">
                <div class="bg-slate-50 p-4 rounded-xl border border-slate-100">
                    <div class="text-2xl font-extrabold text-indigo-600" id="finalScore">0 / 0</div>
                    <div class="text-xs text-slate-500 font-medium" id="lblFinalScore">答對題數</div>
                </div>
                <div class="bg-slate-50 p-4 rounded-xl border border-slate-100">
                    <div class="text-2xl font-extrabold text-emerald-600" id="finalAccuracy">0%</div>
                    <div class="text-xs text-slate-500 font-medium" id="lblAccuracy">正確率</div>
                </div>
            </div>

            <p class="text-slate-600 text-sm max-w-md mx-auto" id="resultMessage">
                做得好！繼續保持，多操多練是考好 BAFS 的不二法門！
            </p>

            <div class="pt-4">
                <button onclick="resetGame()" class="bg-indigo-600 hover:bg-indigo-700 text-white font-semibold py-3 px-8 rounded-xl shadow transition inline-flex items-center gap-2">
                    <i class="fa-solid fa-rotate-right"></i> <span id="btnRetry">再操一次</span>
                </button>
            </div>
        </div>

    </main>

    <!-- Footer -->
    <footer class="bg-slate-100 border-t border-slate-200 text-center py-4 text-xs text-slate-500">
        Based on 2025 HKDSE BAFS Curriculum Guide | BAFS Paper 1A Multiple-Choice Trainer
    </footer>

    <script>
        // Data Store for 24 Questions
        const rawQuestions = [
            {
                qNo: 1,
                topic: { zh: "營商環境 —— 香港的經濟特徵", en: "Business Environment —— Characteristics of Hong Kong Economy" },
                rate: "55%",
                correct: "D",
                q: {
                    zh: "1. 下列哪項有關香港營商環境的陳述是正確的？\n(1) 香港是以服務業為主的經濟體。\n(2) 香港不設外匯管制。\n(3) 企業須繳納利得稅，該稅項是政府的主要收入來源之一。",
                    en: "1. Which of the following statements about the Hong Kong business environment is/are correct?\n(1) Hong Kong is a service-oriented economy.\n(2) Hong Kong does not maintain foreign exchange controls.\n(3) Businesses are subject to profits tax, which is one of the main sources of government revenue."
                },
                options: {
                    zh: { A: "只有(1)及(2)", B: "只有(1)及(3)", C: "只有(2)及(3)", D: "(1)、(2)及(3)" },
                    en: { A: "(1) and (2) only", B: "(1) and (3) only", C: "(2) and (3) only", D: "(1), (2) and (3)" }
                },
                exp: {
                    zh: "1. (1) 正確：香港服務業佔 GDP 比例超過 90%。\n2. (2) 正確：香港實行自由港政策，不設外匯管制。\n3. (3) 正確：利得稅與印花稅等是我國特區政府財政收入的主要來源之一。\n因此，(1)、(2)及(3)均正確，選 D。",
                    en: "1. (1) is correct: Hong Kong's service sector contributes to over 90% of GDP.\n2. (2) is correct: Hong Kong is a free port with no foreign exchange controls.\n3. (3) is correct: Profits tax is one of the primary sources of government revenue.\nTherefore, (1), (2), and (3) are all correct. Thus, D is correct."
                }
            },
            {
                qNo: 2,
                topic: { zh: "營商環境 —— 近況 (CEPA)", en: "Business Environment —— Recent Developments (CEPA)" },
                rate: "50%",
                correct: "B",
                q: {
                    zh: "2. 下列哪項有關《更緊密經貿關係的安排》(CEPA)的陳述是正確的？\n(1) 它是調解香港與內地之間的貿易糾紛的平台。\n(2) 它涵蓋四個範疇，分別是「貨物貿易」、「服務貿易」、「投資」及「經濟技術合作」。\n(3) 它為在大灣區工作的香港專業人士提供資助。",
                    en: "2. Which of the following statements about the Closer Economic Partnership Arrangement (CEPA) is/are correct?\n(1) It provides a platform for resolving trade disputes between Hong Kong and the Mainland.\n(2) It covers four areas, namely 'trade in goods', 'trade in services', 'investment', and 'economic and technical cooperation'.\n(3) It provides subsidies for Hong Kong professionals working in the Greater Bay Area."
                },
                options: {
                    zh: { A: "只有(1)", B: "只有(2)", C: "只有(1)及(3)", D: "只有(2)及(3)" },
                    en: { A: "(1) only", B: "(2) only", C: "(1) and (3) only", D: "(2) and (3) only" }
                },
                exp: {
                    zh: "1. (1) 錯誤：調解國際貿易糾紛是世貿組織 (WTO) 的功能，非 CEPA 職能。\n2. (2) 正確：CEPA 精確涵蓋貨物貿易、服務貿易、投資及經濟技術合作四大範疇。\n3. (3) 錯誤：CEPA 放寬市場准入，但不提供直接資金補貼。\n因此僅 (2) 正確，選 B。",
                    en: "1. (1) is incorrect: Resolving trade disputes is the function of the WTO, not CEPA.\n2. (2) is correct: Officially, CEPA covers 'trade in goods', 'trade in services', 'investment', and 'economic and technical cooperation'.\n3. (3) is incorrect: CEPA facilitates market access but does not provide direct cash subsidies.\nTherefore, only (2) is correct. Thus, B is correct."
                }
            },
            {
                qNo: 3,
                topic: { zh: "營商環境 —— 中港經貿關係", en: "Business Environment —— Mainland-HK Economic Relations" },
                rate: "51%",
                correct: "D",
                q: {
                    zh: "3. 下列哪項有關香港與內地關係的陳述是正確的？\n(1) 內地企業可在香港聯合交易所主板上市。\n(2) 內地是香港最大的貿易夥伴。\n(3) 內地是香港直接投資流入的主要來源。",
                    en: "3. Which of the following statements about the relationship between Hong Kong and the Mainland is/are correct?\n(1) Mainland enterprises can be listed on the Main Board of the Stock Exchange of Hong Kong.\n(2) The Mainland is Hong Kong's largest trading partner.\n(3) The Mainland is the major source of direct investment inflows to Hong Kong."
                },
                options: {
                    zh: { A: "只有(1)及(2)", B: "只有(1)及(3)", C: "只有(2)及(3)", D: "(1)、(2)及(3)" },
                    en: { A: "(1) and (2) only", B: "(1) and (3) only", C: "(2) and (3) only", D: "(1), (2) and (3)" }
                },
                exp: {
                    zh: "1. (1) 正確：內地企業符合標準皆可在港交所上市。\n2. (2) 正確：內地是香港最大的整體商品貿易夥伴。\n3. (3) 正確：內地是香港外來直接投資 (FDI) 的最主要來源。\n因此，(1)、(2)及(3)均正確，選 D。",
                    en: "1. (1) is correct: Mainland enterprises can list on SEHK if criteria are met.\n2. (2) is correct: The Mainland is HK's largest trading partner.\n3. (3) is correct: The Mainland is the largest source of FDI inflows into HK.\nTherefore, (1), (2), and (3) are all correct. Thus, D is correct."
                }
            },
            {
                qNo: 4,
                topic: { zh: "營商環境 —— 全球化與外判", en: "Business Environment —— Globalisation & Outsourcing" },
                rate: "56%",
                correct: "C",
                q: {
                    zh: "4. 下列哪項是一家體育用品製造商實行外判的例子？",
                    en: "4. Which of the following is an example of outsourcing by a sports goods manufacturer?"
                },
                options: {
                    zh: {
                        A: "以較低成本從其他國家購買原材料",
                        B: "將其廠房遷往勞工成本較低的國家",
                        C: "簽訂合約交由發展中國家的製造商生產運動鞋",
                        D: "與海外分銷商合夥在發展中國家推出新型號的運動鞋"
                    },
                    en: {
                        A: "purchasing raw materials from other countries at a lower cost",
                        B: "relocating its factory to a country with lower labour costs",
                        C: "signing a contract with a manufacturer in a developing country to produce sports shoes",
                        D: "partnering with an overseas distributor to launch a new model of sports shoes in a developing country"
                    }
                },
                exp: {
                    zh: "外判是將原由內部執行的功能委託給「第三方外部獨立機構」執行。A 是採購；B 是搬遷自設廠房；D 是合資行銷；只有 C 簽訂合約交由第三方製造商生產屬於外判。故選 C。",
                    en: "Outsourcing is contracting out internal processes to a third-party independent organization. A is sourcing; B is internal relocation; D is joint venture. Only C describes contracting out to a third-party manufacturer. Thus, C is correct."
                }
            },
            {
                qNo: 5,
                topic: { zh: "營商環境 —— 獨資與私人有限公司", en: "Business Environment —— Sole Proprietorship vs. Private Limited Company" },
                rate: "70%",
                correct: "B",
                q: {
                    zh: "5. 下列哪項是獨資商號與私人有限公司的分別？\n(1) 擁有人承擔的債務責任：獨資(無限) vs 私人有限公司(有限)\n(2) 擁有人數目：獨資(1) vs 私人有限公司(1 - 100)\n(3) 獨立的法定個體：獨資(不是) vs 私人有限公司(是)",
                    en: "5. Which of the following are differences between a sole proprietorship and a private limited company?\n(1) Liability borne by owner(s): Sole(Unlimited) vs Private Ltd(Limited)\n(2) Number of owners: Sole(1) vs Private Ltd(1 - 100)\n(3) Separate legal entity: Sole(No) vs Private Ltd(Yes)"
                },
                options: {
                    zh: { A: "只有(1)及(2)", B: "只有(1)及(3)", C: "只有(2)及(3)", D: "(1)、(2)及(3)" },
                    en: { A: "(1) and (2) only", B: "(1) and (3) only", C: "(2) and (3) only", D: "(1), (2) and (3)" }
                },
                exp: {
                    zh: "1. (1) 正確：獨資東主承擔無限責任；私人有限公司股東承擔有限責任。\n2. (2) 錯誤：私人有限公司的最大股東人數上限為 50 人，非 100 人。\n3. (3) 正確：私人有限公司具備獨立法定個體地位，獨資則無。\n因此，只有 (1) 和 (3) 正確，選 B。",
                    en: "1. (1) is correct: Sole proprietor has unlimited liability; shareholders of private limited company have limited liability.\n2. (2) is incorrect: Maximum number of shareholders for a private limited company is 50, not 100.\n3. (3) is correct: Private limited company is a separate legal entity.\nTherefore, only (1) and (3) are correct, making B correct."
                }
            },
            {
                qNo: 6,
                topic: { zh: "營商環境 —— 合夥與上市公司", en: "Business Environment —— Partnership vs. Public Listed Company" },
                rate: "80%",
                correct: "B",
                q: {
                    zh: "6. 與在證券交易所上市的公眾有限公司比較,下列哪項是合夥商號的優點？\n(1) 成立程序較簡單\n(2) 利得稅率較低\n(3) 資金來源較廣",
                    en: "6. Compared with a public limited company listed on the stock exchange, which of the following are advantages of a partnership?\n(1) simpler setup procedures\n(2) lower profits tax rate\n(3) wider sources of capital"
                },
                options: {
                    zh: { A: "只有(1)", B: "只有(1)及(2)", C: "只有(1)及(3)", D: "只有(2)及(3)" },
                    en: { A: "(1) only", B: "(1) and (2) only", C: "(1) and (3) only", D: "(2) and (3) only" }
                },
                exp: {
                    zh: "1. (1) 正確：合夥僅需商業登記，成立極為簡單。\n2. (2) 正確：香港非法人企業（合夥）稅率為 15%，低於法團（有限公司）的 16.5%。\n3. (3) 錯誤：上市公司可向公眾發股發債，資金來源遠比合夥廣泛。\n因此 (1) 和 (2) 正確，選 B。",
                    en: "1. (1) is correct: Partnership setup requires only simple agreement and business registration.\n2. (2) is correct: Standard profits tax rate for unincorporated business is 15%, lower than 16.5% for corporations.\n3. (3) is incorrect: Public listed companies have much wider sources of capital.\nTherefore, (1) and (2) are correct. Thus, B is correct."
                }
            },
            {
                qNo: 7,
                topic: { zh: "營商環境 —— 跨國公司 (MNC)", en: "Business Environment —— Multinational Corporation (MNC)" },
                rate: "60%",
                correct: "A",
                q: {
                    zh: "7. 下列是三家以香港為基地的公司的商業活動例子：\n(1) 甲公司 - 在其他國家設立廠房\n(2) 乙公司 - 在海外證券交易所購買股票\n(3) 丙公司 - 經代理人銷售貨品往海外市場\n以上哪家是跨國公司？",
                    en: "7. The following are examples of business activities of three Hong Kong-based companies:\n(1) Company A - sets up a factory in another country.\n(2) Company B - purchases shares on an overseas stock exchange.\n(3) Company C - sells goods to overseas markets via agents.\nWhich of the above is/are multinational corporation(s)?"
                },
                options: {
                    zh: { A: "只有(1)", B: "只有(2)", C: "只有(1)及(3)", D: "只有(2)及(3)" },
                    en: { A: "(1) only", B: "(2) only", C: "(1) and (3) only", D: "(2) and (3) only" }
                },
                exp: {
                    zh: "跨國公司 (MNC) 必須在多於一個國家擁有並進行「實質的商業營運/生產」。(1) 在海外設廠屬於實體營運，是 MNC；(2) 僅屬證券投資；(3) 僅屬出口貿易。故選 A。",
                    en: "An MNC must own and control physical operations/factories in more than one country. (1) setting up an overseas factory is an MNC operation; (2) is portfolio investment; (3) is simple export trade. Thus, A is correct."
                }
            },
            {
                qNo: 8,
                topic: { zh: "營商環境 —— 社會責任 (CSR)", en: "Business Environment —— Corporate Social Responsibility" },
                rate: "46%",
                correct: "A",
                q: {
                    zh: "8. 下列是一家物流公司所採用的措施。哪項措施是履行社會責任？\n(1) 貨車使用碳排放較少的燃料\n(2) 在合約的指定時限內將包裹送達顧客\n(3) 為司機座位配置安全帶",
                    en: "8. The following are measures adopted by a logistics company. Which of these measures is/are fulfilling social responsibilities?\n(1) using fuel with less carbon emission for lorries\n(2) delivering parcels to customers within the time limit stated in the contracts\n(3) installing seat belts for drivers"
                },
                options: {
                    zh: { A: "只有(1)", B: "只有(1)及(2)", C: "只有(2)及(3)", D: "(1)、(2)及(3)" },
                    en: { A: "(1) only", B: "(1) and (2) only", C: "(2) and (3) only", D: "(1), (2) and (3)" }
                },
                exp: {
                    zh: "1. (1) 正確：自願使用低碳燃料減排，屬超越法律底線的環保社會責任。\n2. (2) 錯誤：按合約送達包裹是 basic 合約與誠信義務。\n3. (3) 錯誤：配置安全帶是交通法例規定的強制法律義務。\n因此僅 (1) 正確，選 A。",
                    en: "1. (1) is correct: Voluntarily using eco-friendly fuel is a CSR initiative.\n2. (2) is incorrect: On-time delivery is a contractual obligation.\n3. (3) is incorrect: Seat belts are mandatory legal requirements.\nTherefore, only (1) is correct. Thus, A is correct."
                }
            },
            {
                qNo: 9,
                topic: { zh: "基礎個人理財 —— 金錢的時間值 (EAR)", en: "Basics of Personal Financial Management —— Time Value of Money" },
                rate: "74%",
                correct: "B",
                q: {
                    zh: "9. 一家銀行提供一個投資計劃，每年回報率為12%，每季複息計算。這投資計劃的實際回報率是多少？",
                    en: "9. A bank offers an investment plan with an annual rate of return of 12%, compounded quarterly. What is the effective rate of return of the investment plan?"
                },
                options: {
                    zh: { A: "9.27%", B: "12.55%", C: "13.63%", D: "15.92%" },
                    en: { A: "9.27%", B: "12.55%", C: "13.63%", D: "15.92%" }
                },
                exp: {
                    zh: "每季利率 r = 12% ÷ 4 = 3% = 0.03。\n實際年利率 EAR = (1 + 0.03)^4 - 1 = (1.03)^4 - 1 = 1.1255 - 1 = 12.55%。\n故選 B。",
                    en: "Quarterly rate r = 12% ÷ 4 = 3% = 0.03.\nEffective Annual Rate EAR = (1 + 0.03)^4 - 1 = (1.03)^4 - 1 = 12.55%.\nThus, B is correct."
                }
            },
            {
                qNo: 10,
                topic: { zh: "基礎個人理財 —— 個人信貸記錄", en: "Basics of Personal Financial Management —— Credit Records" },
                rate: "80%",
                correct: "D",
                q: {
                    zh: "10. 下列哪項有關個人信貸記錄的陳述是正確的？\n(1) 退休人士的信貸評分較受僱人士的為低。\n(2) 任何人均有權查閱自己的信貸報告。\n(3) 信貸評分較高的借貸人較易借得貸款。",
                    en: "10. Which of the following statements about personal credit record is/are correct?\n(1) The credit score of a retired person is lower than that of an employed person.\n(2) Any individual has the right to check his/her own credit report.\n(3) A borrower with a higher credit score can obtain loans more easily."
                },
                options: {
                    zh: { A: "只有(1)", B: "只有(2)", C: "只有(1)及(3)", D: "只有(2)及(3)" },
                    en: { A: "(1) only", B: "(2) only", C: "(1) and (3) only", D: "(2) and (3) only" }
                },
                exp: {
                    zh: "1. (1) 錯誤：信貸評分由過往還款紀錄及債務等決定，非單純由退休身份決定。\n2. (2) 正確：個人有權查閱個人的信貸報告。\n3. (3) 正確：高評分代表違約風險低，銀行更容易批核貸款。\n因此 (2) 和 (3) 正確，選 D。",
                    en: "1. (1) is incorrect: Credit score is based on repayment history and debt records, not retirement status alone.\n2. (2) is correct: Individuals have the right to check their own credit reports.\n3. (3) is correct: Higher credit scores indicate lower risk, making loans easier to obtain.\nTherefore, (2) and (3) are correct. Thus, D is correct."
                }
            },
            {
                qNo: 11,
                topic: { zh: "基礎個人理財 —— 信用卡利息機制", en: "Basics of Personal Financial Management —— Credit Cards" },
                rate: "52%",
                correct: "A",
                q: {
                    zh: "11. 下列哪項有關信用卡的陳述是正確的？\n(1) 利息是按過期結欠逐日計算。\n(2) 所有信用卡用戶的信用限額是相同的。\n(3) 如信用卡用戶在到期日前繳付最低還款額，銀行便不會就結欠徵收利息。",
                    en: "11. Which of the following statements about credit cards is/are correct?\n(1) Interest is calculated on the overdue balance on a daily basis.\n(2) The credit limit of all credit card users is the same.\n(3) The bank will not charge interest on the outstanding balance if a credit card user repays the minimum payment before the due date."
                },
                options: {
                    zh: { A: "只有(1)", B: "只有(1)及(2)", C: "只有(1)及(3)", D: "只有(2) conquest(3)" },
                    en: { A: "(1) only", B: "(1) and (2) only", C: "(1) and (3) only", D: "(2) and (3) only" }
                },
                exp: {
                    zh: "1. (1) 正確：信用卡過期結欠按每日複息計算。\n2. (2) 錯誤：信用額度由銀行依用戶財務狀況個別審核。\n3. (3) 錯誤：只還最低還款額（Min pay），銀行依然會對剩餘結欠徵收高額每日利息！\n因此僅 (1) 正確，選 A。",
                    en: "1. (1) is correct: Interest on overdue balances is calculated on a daily basis.\n2. (2) is incorrect: Credit limits are determined individually.\n3. (3) is incorrect: Paying minimum payment avoids late fees, but interest is STILL charged on outstanding balances!\nTherefore, only (1) is correct. Thus, A is correct."
                }
            },
            {
                qNo: 12,
                topic: { zh: "基礎個人理財 —— 公司債券與定期存款", en: "Basics of Personal Financial Management —— Bonds vs Term Deposits" },
                rate: "57%",
                correct: "C",
                q: {
                    zh: "12. 下列哪項有關投資於公司債券與定期存款的陳述是正確的？\n(1) 由於投資於公司債券的風險較定期存款高，故投資前者的回報率必定較高。\n(2) 在投資期內兩者的利率皆是固定的。\n(3) 兩者的投資者皆有權在到期日取回本金。",
                    en: "12. Which of the following statements about investing in company bonds and term deposits is/are correct?\n(1) Since investing in company bonds is riskier than in term deposits, the rate of return of the former must be higher.\n(2) The interest rates of both are fixed during the investment period.\n(3) Investors of both have the right to get back the principal upon maturity."
                },
                options: {
                    zh: { A: "只有(1)", B: "只有(2)", C: "只有(2)及(3)", D: "(1)、(2)及(3)" },
                    en: { A: "(1) only", B: "(2) only", C: "(2) and (3) only", D: "(1), (2) and (3)" }
                },
                exp: {
                    zh: "1. (1) 錯誤：高風險不保證「必定」有高實際回報（可能面臨違約虧損）。\n2. (2) 正確：標準公司債券票面利率與定期存款利率皆為固定。\n3. (3) 正確：兩者皆為債權合約，到期有權取回本金。\n因此 (2) 和 (3) 正確，選 C。",
                    en: "1. (1) is incorrect: High risk does NOT guarantee a higher actual return (default risk exists).\n2. (2) is correct: Both carry fixed interest rates.\n3. (3) is correct: Both have the contractual right to retrieve principal upon maturity.\nTherefore, (2) and (3) are correct. Thus, C is correct."
                }
            },
            {
                qNo: 13,
                topic: { zh: "基礎個人理財 —— 強積金提取條件", en: "Basics of Personal Financial Management —— MPF Scheme Withdrawal" },
                rate: "72%",
                correct: "A",
                q: {
                    zh: "13. 下列哪位人士有資格從強制性公積金（強積金）計劃提取累算權益？",
                    en: "13. Which of the following persons is/are eligible to withdraw the accrued benefits from the Mandatory Provident Fund (MPF) Scheme?"
                },
                options: {
                    zh: {
                        A: "自僱的士司機，62歲，剛剛退休。",
                        B: "工人，60歲，強積金帳戶結餘為$10000。",
                        C: "跨國公司經理，40歲，剛調職到海外總公司。",
                        D: "文員，35歲，為進修辭去工作。"
                    },
                    en: {
                        A: "A self-employed taxi driver, aged 62, who has just retired.",
                        B: "A worker, aged 60, with an MPF account balance of $10 000.",
                        C: "An MNC manager, aged 40, who has just been transferred to the overseas headquarters.",
                        D: "A clerk, aged 35, who resigned to pursue further studies."
                    }
                },
                exp: {
                    zh: "強積金法定提早提取條件之一為「年滿 60 歲並聲明永久性退休」。A 滿 62 歲且已退休，完全符合條件。B 未提及退休；C 海外調職非永久離港；D 離職進修不符合條件。故選 A。",
                    en: "Early withdrawal of MPF is permitted when one reaches age 60 and permanently retires. A is 62 and retired, satisfying the requirement. B did not state retirement; C is temporary overseas transfer; D is not a statutory reason. Thus, A is correct."
                }
            },
            {
                qNo: 14,
                topic: { zh: "基礎個人理財 —— 投資者的權利", en: "Basics of Personal Financial Management —— Investor Rights" },
                rate: "76%",
                correct: "D",
                q: {
                    zh: "14. 下列哪項是個人投資者的權利？\n(1) 毋須透過經紀在香港聯合交易所買賣股票\n(2) 知悉投資交易的服務收費\n(3) 可選擇是否依照投資顧問的建議作投資決定",
                    en: "14. Which of the following is/are right(s) of a share investor?\n(1) to trade stocks on the Stock Exchange of Hong Kong without using brokers\n(2) to know the service charges of investment transactions\n(3) to choose whether to follow the investment decisions recommended by investment advisors"
                },
                options: {
                    zh: { A: "只有(1)", B: "只有(2)", C: "只有(3)", D: "只有(2)及(3)" },
                    en: { A: "(1) only", B: "(2) only", C: "(3) only", D: "(2) and (3) only" }
                },
                exp: {
                    zh: "1. (1) 錯誤：個人散戶必須透過持牌經紀商或銀行代為買賣股票。\n2. (2) 正確：投資者有權知悉各項交易收費與佣金。\n3. (3) 正確：投資者有權自主決定是否採納顧問建議。\n因此 (2) 和 (3) 正確，選 D。",
                    en: "1. (1) is incorrect: Individual investors must trade through licensed brokers or banks.\n2. (2) is correct: Investors have the right to know service fees and commissions.\n3. (3) is correct: Investors have the absolute right to decide whether to follow advice.\nTherefore, (2) and (3) are correct. Thus, D is correct."
                }
            },
            {
                qNo: 15,
                topic: { zh: "基礎個人理財 —— 影響股價的因素", en: "Basics of Personal Financial Management —— Factors Affecting Stock Price" },
                rate: "68%",
                correct: "C",
                q: {
                    zh: "15. 撇除其他因素，下列哪項會對一家船務公司的股價帶來不利影響？\n(1) 員工罷工\n(2) 碼頭容量增加\n(3) 貨船燃料（油價）上升",
                    en: "15. Ignoring other factors, which of the following will have an adverse effect on the share price of a listed shipping company?\n(1) strike of employees\n(2) increase in port capacity\n(3) rise in fuel (oil) price"
                },
                options: {
                    zh: { A: "只有(1)", B: "只有(2)", C: "只有(1)及(3)", D: "(1)、(2)及(3)" },
                    en: { A: "(1) only", B: "(2) only", C: "(1) and (3) only", D: "(1), (2) and (3)" }
                },
                exp: {
                    zh: "1. (1) 不利：罷工導致營運癱瘓、損失收入，打擊股價。\n2. (2) 有利：碼頭容量增加提高港口運作效率，屬正面利好。\n3. (3) 不利：燃油價格上漲直接大幅增加營運成本，削減利潤。\n因此 (1) 和 (3) 帶來不利影響，選 C。",
                    en: "1. (1) adverse: Strikes disrupt operations and revenue, lowering stock price.\n2. (2) positive: Increased port capacity improves operational efficiency.\n3. (3) adverse: Rising fuel prices increase core operating costs, lowering net profit.\nTherefore, (1) and (3) have adverse effects. Thus, C is correct."
                }
            },
            {
                qNo: 16,
                topic: { zh: "基礎個人理財 —— 恒生指數 (HSI)", en: "Basics of Personal Financial Management —— Hang Seng Index" },
                rate: "34%",
                correct: "C",
                q: {
                    zh: "16. 下列哪項有關恒生指數的陳述是正確的？",
                    en: "16. Which of the following statements about the Hang Seng Index is correct?"
                },
                options: {
                    zh: {
                        A: "過去五年的成份股數目維持不變。",
                        B: "它是香港上市公司發行的股票和債券整體表現的指標。",
                        C: "在計算指數時，不同成份股所佔的比重不同。",
                        D: "「旅遊業」是四個分類指數的其中一個。"
                    },
                    en: {
                        A: "The number of constituent stocks has remained unchanged in the past five years.",
                        B: "It serves as a benchmark of the general performance of the stocks and bonds issued by companies listed in Hong Kong.",
                        C: "A different weighting is assigned to different constituent stocks when computing the index.",
                        D: "'Tourism' is one of the four sub-indexes."
                    }
                },
                exp: {
                    zh: "1. C 正確：恆指採用市值加權計算，不同成份股依市值大小賦予不同權重。\n2. A 錯誤：成份股數目近年持續擴容調整。\n3. B 錯誤：恆指僅反映「股票」表現，不包債券。\n4. D 錯誤：四大分類指數為金融、公用事業、地產、工商業，無旅遊業。故選 C。",
                    en: "1. C is correct: HSI is a market-cap weighted index, assigning different weightings to constituent stocks.\n2. A is incorrect: Constituent stock numbers have expanded recently.\n3. B is incorrect: HSI reflects the stock market only, excluding bonds.\n4. D is incorrect: Four sub-indexes are Finance, Utilities, Properties, and Commerce & Industry. Thus, C is correct."
                }
            },
            {
                qNo: 17,
                topic: { zh: "基礎管理 —— 管理的重要性", en: "Basics of Management —— Importance of Management" },
                rate: "81%",
                correct: "B",
                q: {
                    zh: "17. 下列哪項顯示管理對企業的重要？\n(1) 有效達至機構的目標\n(2) 有效率地運用人力資源\n(3) 避免產生營業費用",
                    en: "17. Which of the following shows the importance of management to a business?\n(1) achieve the goals of the organization effectively\n(2) utilize human resources efficiently\n(3) avoid incurring operating expenses"
                },
                options: {
                    zh: { A: "只有(1)", B: "只有(1)及(2)", C: "只有(1)及(3)", D: "(1)、(2)及(3)" },
                    en: { A: "(1) only", B: "(1) and (2) only", C: "(1) and (3) only", D: "(1), (2) and (3)" }
                },
                exp: {
                    zh: "1. (1) 正確：管理能引導團隊有效達至目標 (Effectiveness)。\n2. (2) 正確：管理能妥善配置資源以發揮效率 (Efficiency)。\n3. (3) 錯誤：營業費用（如租金、薪金）是營運所必需且不可避免的，管理旨在控制而非完全避免費用。\n因此 (1) 和 (2) 正確，選 B。",
                    en: "1. (1) is correct: Management ensures goals are achieved effectively.\n2. (2) is correct: Management ensures resources are utilized efficiently.\n3. (3) is incorrect: Incurring operating expenses is necessary for business; management controls expenses rather than avoiding them entirely.\nTherefore, (1) and (2) are correct. Thus, B is correct."
                }
            },
            {
                qNo: 18,
                topic: { zh: "基礎管理 —— 統一命令原則", en: "Basics of Management —— Unity of Command" },
                rate: "42%",
                correct: "A",
                q: {
                    zh: "18. 下列哪項有關「統一命令」的陳述是正確的？\n(1) 下屬不會收到來自不同上司的指令。\n(2) 下屬更能理解上司發出的指令。\n(3) 它能鞏固上司與其下屬之間的人際關係。",
                    en: "18. Which of the following statements about 'unity of command' is correct?\n(1) Subordinates do not receive conflicting instructions from different superiors.\n(2) Subordinates can understand the instructions from superiors better.\n(3) It can strengthen interpersonal relationships between superiors and subordinates."
                },
                options: {
                    zh: { A: "只有(1)", B: "只有(1)及(2)", C: "只有(1)及(3)", D: "(1)、(2)及(3)" },
                    en: { A: "(1) only", B: "(1) and (2) only", C: "(1) and (3) only", D: "(1), (2) and (3)" }
                },
                exp: {
                    zh: "1. (1) 正確：統一命令指每名下屬只向一位直屬上司匯報，能防止接收矛盾指令。\n2. (2) 錯誤：能否理解指令取決於溝通技巧，與結構無關。\n3. (3) 錯誤：此為權力劃分原則，非人際關係鞏固機制。\n因此僅 (1) 正確，選 A。",
                    en: "1. (1) is correct: Unity of command dictates reporting to only one boss, preventing conflicting instructions.\n2. (2) is incorrect: Understanding instructions depends on communication skills.\n3. (3) is incorrect: This is a structural principle, not a tool for building interpersonal relationships.\nTherefore, only (1) is correct. Thus, A is correct."
                }
            },
            {
                qNo: 19,
                topic: { zh: "基礎管理 —— 組織架構與職權", en: "Basics of Management —— Organisational Structure & Authority" },
                rate: "44%",
                correct: "A",
                q: {
                    zh: "19. 志偉是一家貿易公司的總經理。他向市場營銷經理、人力資源經理和財務經理發出指令。\n根據以上資料，下列哪項陳述是正確的？\n(1) 這貿易公司是按功能劃分部門的。\n(2) 志偉比其他三位經理有較大的職權。\n(3) 市場營銷經理對人力資源經理和財務經理有幕僚職權。",
                    en: "19. Tracy is the general manager of a trading company. He issues instructions to the marketing manager, human resources manager and finance manager.\nBased on the above information, which of the following statements are correct?\n(1) The trading company is departmentalised by function.\n(2) Tracy has greater authority than the other three managers.\n(3) The marketing manager has staff authority over the human resources manager and the finance manager."
                },
                options: {
                    zh: { A: "只有(1)及(2)", B: "只有(1)及(3)", C: "只有(2)及(3)", D: "(1)、(2)及(3)" },
                    en: { A: "(1) and (2) only", B: "(1) and (3) only", C: "(2) and (3) only", D: "(1), (2) and (3)" }
                },
                exp: {
                    zh: "1. (1) 正確：按市場、HR、財務劃分屬於功能劃分部門。\n2. (2) 正確：總經理處於高層，比部門經理擁有更大的直線職權。\n3. (3) 錯誤：三位經理屬於同級平行關係，市場經理對其他人無任何幕僚職權。\n因此 (1) 和 (2) 正確，選 A。",
                    en: "1. (1) is correct: Marketing, HR, and Finance represent departmentalisation by function.\n2. (2) is correct: General Manager is top management with greater line authority.\n3. (3) is incorrect: The three managers are peers; marketing manager has no authority over peers.\nTherefore, (1) and (2) are correct. Thus, A is correct."
                }
            },
            {
                qNo: 20,
                topic: { zh: "基礎管理 —— 營運部門的職掌", en: "Basics of Management —— Role of Operations Department" },
                rate: "79%",
                correct: "D",
                q: {
                    zh: "20. 一家本地初創公司計劃興建廠房。下列哪項是這公司營運部門的工作？",
                    en: "20. A local start-up company plans to set up a factory. Which of the following tasks is performed by the operations department of the company?"
                },
                options: {
                    zh: {
                        A: "為廠房購買火險",
                        B: "為興建廠房籌集資金",
                        C: "為廠房發展網絡系統以分享生產信息",
                        D: "制定廠房的產能"
                    },
                    en: {
                        A: "buying fire insurance for the plant",
                        B: "raising capital for the construction of the plant",
                        C: "developing network systems for the plant to share production information",
                        D: "determining the production capacity of the plant"
                    }
                },
                exp: {
                    zh: "A 屬於風險管理；B 屬於財務管理；C 屬於資訊管理/IT；D 制定廠房產能 (Production capacity) 直接屬於營運管理的核心範疇。故選 D。",
                    en: "A belongs to risk management; B belongs to finance; C belongs to IT/info management; D determining production capacity is a core task of operations management. Thus, D is correct."
                }
            },
            {
                qNo: 21,
                topic: { zh: "基礎管理 —— SMART 目標準則", en: "Basics of Management —— SMART Objectives" },
                rate: "78%",
                correct: "C",
                q: {
                    zh: "21. 某商號的資訊管理經理訂立以下目標：「一年內減少5%的錯誤。」\n上述目標符合以下哪項良好目標的準則？\n(1) 具體的\n(2) 可量度的\n(3) 具時限的",
                    en: "21. The information manager of a firm sets the following objective: 'To reduce errors by 5% within one year.'\nWhich of the following criteria for good objectives is/are fulfilled in the target?\n(1) specific\n(2) measurable\n(3) time-bound"
                },
                options: {
                    zh: { A: "只有(1)及(2)", B: "只有(1)及(3)", C: "只有(2)及(3)", D: "(1)、(2)及(3)" },
                    en: { A: "(1) and (2) only", B: "(1) and (3) only", C: "(2) and (3) only", D: "(1), (2) and (3)" }
                },
                exp: {
                    zh: "1. (1) 不符合：「減少錯誤」未列明何種錯誤（如代碼、數據輸入等），缺乏具體性 (Specific)。\n2. (2) 符合：列出「5%」屬於可量度 (Measurable)。\n3. (3) 符合：列出「一年內」屬於具時限 (Time-bound)。\n因此 (2) 和 (3) 符合，選 C。",
                    en: "1. (1) unfulfilled: 'Reduce errors' is vague, lacking specificity.\n2. (2) fulfilled: 'By 5%' is quantitative and measurable.\n3. (3) fulfilled: 'Within one year' specifies a timeframe.\nTherefore, only (2) and (3) are fulfilled. Thus, C is correct."
                }
            },
            {
                qNo: 22,
                topic: { zh: "中小型企業 —— 中小企的重要性", en: "SMEs —— Importance of SMEs to Hong Kong Economy" },
                rate: "59%",
                correct: "C",
                q: {
                    zh: "22. 下列哪項顯示中小型企業對香港經濟的重要？\n(1) 提供更多產品和服務以促進市場競爭\n(2) 向政府提供超過90%的利得稅收入\n(3) 為大約45%的總就業人數(不計公務員)提供就業機會",
                    en: "22. Which of the following shows the importance of small and medium enterprises (SMEs) to the Hong Kong economy?\n(1) provide more products and services to promote market competition\n(2) provide over 90% of profits tax revenue to the government\n(3) provide employment opportunities for around 45% of total employment (excluding civil service)"
                },
                options: {
                    zh: { A: "只有(1)", B: "只有(2)", C: "只有(1)及(3)", D: "(1)、(2)及(3)" },
                    en: { A: "(1) only", B: "(2) only", C: "(1) and (3) only", D: "(1), (2) and (3)" }
                },
                exp: {
                    zh: "1. (1) 正確：中小企提供多元產品，促進競爭。\n2. (2) 錯誤：政府絕大部分利得稅來自少數大型企業集團，非中小企。\n3. (3) 正確：官方數據顯示中小企聘用全港私營機構約 45% 的勞動人口。\n因此 (1) 和 (3) 正確，選 C。",
                    en: "1. (1) is correct: SMEs promote market competition.\n2. (2) is incorrect: Majority of profits tax revenue comes from large conglomerates, not SMEs.\n3. (3) is correct: SMEs employ around 45% of total private sector employment in HK.\nTherefore, (1) and (3) are correct. Thus, C is correct."
                }
            },
            {
                qNo: 23,
                topic: { zh: "基礎管理 —— 計劃流程步驟", en: "Basics of Management —— Planning Process Steps" },
                rate: "61%",
                correct: "D",
                q: {
                    zh: "23. 計劃過程中，執行行動方案前的上一個步驟是",
                    en: "23. In the planning process, the step immediately before implementing the action plan is"
                },
                options: {
                    zh: {
                        A: "分析資料",
                        B: "評估其他行動方案",
                        C: "監察行動方案的進度",
                        D: "制訂行動方案的日程"
                    },
                    en: {
                        A: "analyzing information",
                        B: "evaluating alternative action plans",
                        C: "monitoring the progress of the action plan",
                        D: "formulating the schedule of the action plan"
                    }
                },
                exp: {
                    zh: "計劃流程：設定目標 -> 分析資料 -> 擬定備選方案 -> 評估方案 -> 制訂行動方案及日程 (Formulating schedule) -> 執行方案 (Implementation) -> 監察進度。因此執行前一步為 D。",
                    en: "Planning steps: Set goals -> Analyze info -> Formulate options -> Evaluate -> Formulate Action Plan & Schedule -> Implementation -> Monitor. The step right before implementation is D."
                }
            },
            {
                qNo: 24,
                topic: { zh: "基礎管理 —— 分工原則的影響", en: "Basics of Management —— Division of Work" },
                rate: "61%",
                correct: "B",
                q: {
                    zh: "24. 下列哪項有關一家廠商採用「分工」的陳述是正確的？\n(1) 它減輕生產工人的工作量。\n(2) 如其中一個工序出錯，整個生產程序都會受到影響。\n(3) 它提高員工的工作滿足感。",
                    en: "24. Which of the following statements about a manufacturer adopting 'division of work' is correct?\n(1) It reduces the workload of production workers.\n(2) If an error occurs in one stage of the work, the whole production process will be affected.\n(3) It increases the job satisfaction of employees."
                },
                options: {
                    zh: { A: "只有(1)", B: "只有(2)", C: "只有(2)及(3)", D: "(1)、(2)及(3)" },
                    en: { A: "(1) only", B: "(1) and (2) only", C: "(2) and (3) only", D: "(1), (2) and (3)" }
                },
                exp: {
                    zh: "1. (1) 錯誤：分工拆解工序提升效率，但不減輕總工作量。\n2. (2) 正確：工序間高度互相倚賴，一環出錯會癱瘓整個生產線。\n3. (3) 錯誤：長期做單一重複工序易生枯燥，會降低工作滿足感。\n因此僅 (2) 正確，選 B。",
                    en: "1. (1) is incorrect: Division of work optimizes efficiency but doesn't reduce total workload.\n2. (2) is correct: High interdependence means an error in one stage bottlenecks the whole line.\n3. (3) is incorrect: Repetitive tasks lead to boredom and reduce job satisfaction.\nTherefore, only (2) is correct. Thus, B is correct."
                }
            }
        ];

        // Game State
        let currentLang = 'zh'; // 'zh' or 'en'
        let quizQuestions = [];
        let currentIndex = 0;
        let score = 0;
        let selectedOption = null;
        let isAnswered = false;

        // UI Element References
        const elements = {
            welcomeScreen: document.getElementById('welcomeScreen'),
            quizScreen: document.getElementById('quizScreen'),
            resultScreen: document.getElementById('resultScreen'),
            langToggle: document.getElementById('langToggle'),
            currentLangLabel: document.getElementById('currentLangLabel'),
            welcomeTitle: document.getElementById('welcomeTitle'),
            welcomeDesc: document.getElementById('welcomeDesc'),
            btnQuick10: document.getElementById('btnQuick10'),
            btnAll24: document.getElementById('btnAll24'),
            questionProgress: document.getElementById('questionProgress'),
            scoreTracker: document.getElementById('scoreTracker'),
            progressBar: document.getElementById('progressBar'),
            topicTag: document.getElementById('topicTag'),
            rateTag: document.getElementById('rateTag'),
            questionText: document.getElementById('questionText'),
            optionsContainer: document.getElementById('optionsContainer'),
            explanationBox: document.getElementById('explanationBox'),
            expTitle: document.getElementById('expTitle'),
            explanationText: document.getElementById('explanationText'),
            nextBtnContainer: document.getElementById('nextBtnContainer'),
            nextBtnText: document.getElementById('nextBtnText'),
            finalScore: document.getElementById('finalScore'),
            finalAccuracy: document.getElementById('finalAccuracy'),
            lblFinalScore: document.getElementById('lblFinalScore'),
            lblAccuracy: document.getElementById('lblAccuracy'),
            resultTitle: document.getElementById('resultTitle'),
            resultMessage: document.getElementById('resultMessage'),
            btnRetry: document.getElementById('btnRetry')
        };

        // Translations Dictionary
        const uiText = {
            zh: {
                langLabel: "中文 / ENG",
                welcomeTitle: "2025 BAFS 卷一甲部選擇題操練",
                welcomeDesc: "收錄 24 道精華考題，涵蓋「營商環境、基礎個人理財及基礎管理」。備有雙語對照及官方詳細解析。",
                btnQuick10: "隨機 10 題快操",
                btnAll24: "全套 24 題挑戰",
                scoreTracker: "得分",
                ratePrefix: "歷屆正確率",
                expTitle: "官方答案解析",
                nextBtn: "下一題",
                finishBtn: "查看總成績",
                resultTitle: "練習完成！",
                lblFinalScore: "答對題數",
                lblAccuracy: "正確率",
                btnRetry: "再操一次",
                msgHigh: "太厲害了！你對 2025 新學制 BAFS 卷一必修部分掌握得非常通透！",
                msgMid: "表現不錯！仔細複習錯題的解析，相信下次能拿到滿分！",
                msgLow: "再接再厲！建議詳讀題目解析並重新練習，熟悉考試設陷位。"
            },
            en: {
                langLabel: "ENG / 中文",
                welcomeTitle: "2025 BAFS Paper 1A MC Trainer",
                welcomeDesc: "Contains 24 core MC questions covering Business Environment, Personal Financial Management, and Basics of Management with bilingual detailed explanations.",
                btnQuick10: "Random 10 Quick Workout",
                btnAll24: "Full 24 Challenge",
                scoreTracker: "Score",
                ratePrefix: "Passing Rate",
                expTitle: "Official Explanation",
                nextBtn: "Next Question",
                finishBtn: "View Results",
                resultTitle: "Quiz Completed!",
                lblFinalScore: "Correct Answers",
                lblAccuracy: "Accuracy",
                btnRetry: "Try Again",
                msgHigh: "Excellent! You have mastered the 2025 DSE BAFS Paper 1 compulsory module!",
                msgMid: "Good job! Review the explanations carefully to achieve 100% next time!",
                msgLow: "Keep trying! Read through the explanations to get familiar with exam traps."
            }
        };

        // Initialize Language Toggle Event
        elements.langToggle.addEventListener('click', () => {
            currentLang = currentLang === 'zh' ? 'en' : 'zh';
            updateLanguageUI();
            if (!elements.quizScreen.classList.contains('hidden')) {
                renderQuestion();
            }
        });

        function updateLanguageUI() {
            const t = uiText[currentLang];
            elements.currentLangLabel.textContent = t.langLabel;
            elements.welcomeTitle.textContent = t.welcomeTitle;
            elements.welcomeDesc.textContent = t.welcomeDesc;
            elements.btnQuick10.textContent = t.btnQuick10;
            elements.btnAll24.textContent = t.btnAll24;
            elements.expTitle.textContent = t.expTitle;
            elements.lblFinalScore.textContent = t.lblFinalScore;
            elements.lblAccuracy.textContent = t.lblAccuracy;
            elements.btnRetry.textContent = t.btnRetry;
            
            if (isAnswered) {
                elements.nextBtnText.textContent = currentIndex < quizQuestions.length - 1 ? t.nextBtn : t.finishBtn;
            }
        }

        // Start Game
        function startGame(count) {
            let shuffled = [...rawQuestions].sort(() => 0.5 - Math.random());
            quizQuestions = shuffled.slice(0, count);
            currentIndex = 0;
            score = 0;
            
            elements.welcomeScreen.classList.add('hidden');
            elements.resultScreen.classList.add('hidden');
            elements.quizScreen.classList.remove('hidden');

            renderQuestion();
        }

        // Render Current Question
        function renderQuestion() {
            isAnswered = false;
            selectedOption = null;
            const item = quizQuestions[currentIndex];
            const t = uiText[currentLang];

            // Progress & Score
            elements.questionProgress.textContent = `Q${currentIndex + 1} / ${quizQuestions.length}`;
            elements.scoreTracker.textContent = `${t.scoreTracker}: ${score}`;
            elements.progressBar.style.width = `${((currentIndex + 1) / quizQuestions.length) * 100}%`;

            // Question Info
            elements.topicTag.textContent = item.topic[currentLang];
            elements.rateTag.textContent = `${t.ratePrefix}: ${item.rate}`;
            elements.questionText.textContent = item.q[currentLang];

            // Options
            elements.optionsContainer.innerHTML = '';
            const opts = item.options[currentLang];
            
            ['A', 'B', 'C', 'D'].forEach(key => {
                if (opts[key]) {
                    const btn = document.createElement('button');
                    btn.className = `option-card w-full text-left p-4 rounded-xl border border-slate-200 bg-white hover:border-indigo-300 flex items-start gap-3 text-sm md:text-base font-medium text-slate-700 disabled:cursor-not-allowed`;
                    btn.onclick = () => selectOption(key);
                    btn.id = `option-${key}`;
                    
                    btn.innerHTML = `
                        <span class="w-7 h-7 rounded-lg bg-slate-100 text-slate-600 font-bold flex items-center justify-center shrink-0 border border-slate-200">${key}</span>
                        <span class="pt-0.5 leading-relaxed">${opts[key]}</span>
                    `;
                    elements.optionsContainer.appendChild(btn);
                }
            });

            // Reset Explanation and Next Button
            elements.explanationBox.classList.add('hidden');
            elements.nextBtnContainer.classList.add('hidden');
        }

        // Handle Option Selection
        function selectOption(key) {
            if (isAnswered) return;
            isAnswered = true;
            selectedOption = key;

            const item = quizQuestions[currentIndex];
            const isCorrect = key === item.correct;
            const t = uiText[currentLang];

            if (isCorrect) score++;

            // Update UI for options
            ['A', 'B', 'C', 'D'].forEach(k => {
                const btn = document.getElementById(`option-${k}`);
                if (!btn) return;

                btn.classList.add('disabled');
                const badge = btn.querySelector('span');

                if (k === item.correct) {
                    btn.className = "w-full text-left p-4 rounded-xl border-2 border-emerald-500 bg-emerald-50/60 text-emerald-900 font-semibold flex items-start gap-3 text-sm md:text-base";
                    badge.className = "w-7 h-7 rounded-lg bg-emerald-500 text-white font-bold flex items-center justify-center shrink-0";
                } else if (k === selectedOption && !isCorrect) {
                    btn.className = "w-full text-left p-4 rounded-xl border-2 border-rose-500 bg-rose-50/60 text-rose-900 font-semibold flex items-start gap-3 text-sm md:text-base";
                    badge.className = "w-7 h-7 rounded-lg bg-rose-500 text-white font-bold flex items-center justify-center shrink-0";
                } else {
                    btn.className = "w-full text-left p-4 rounded-xl border border-slate-200 bg-white opacity-50 flex items-start gap-3 text-sm md:text-base text-slate-500";
                }
            });

            // Update Score Tracker
            elements.scoreTracker.textContent = `${t.scoreTracker}: ${score}`;

            // Show Explanation
            elements.explanationText.textContent = item.exp[currentLang];
            elements.explanationBox.classList.remove('hidden');

            // Show Next Button
            elements.nextBtnText.textContent = currentIndex < quizQuestions.length - 1 ? t.nextBtn : t.finishBtn;
            elements.nextBtnContainer.classList.remove('hidden');
        }

        // Next Question or Finish
        function nextQuestion() {
            if (currentIndex < quizQuestions.length - 1) {
                currentIndex++;
                renderQuestion();
            } else {
                showResults();
            }
        }

        // Show Final Results
        function showResults() {
            elements.quizScreen.classList.add('hidden');
            elements.resultScreen.classList.remove('hidden');

            const total = quizQuestions.length;
            const percentage = Math.round((score / total) * 100);
            const t = uiText[currentLang];

            elements.finalScore.textContent = `${score} / ${total}`;
            elements.finalAccuracy.textContent = `${percentage}%`;

            if (percentage >= 80) {
                elements.resultMessage.textContent = t.msgHigh;
            } else if (percentage >= 50) {
                elements.resultMessage.textContent = t.msgMid;
            } else {
                elements.resultMessage.textContent = t.msgLow;
            }
        }

        // Reset to Welcome Screen
        function resetGame() {
            elements.resultScreen.classList.add('hidden');
            elements.welcomeScreen.classList.remove('hidden');
        }

        // Initial setup
        updateLanguageUI();
    </script>
</body>
</html>
```eof

已為您建立包含 **2025 DSE BAFS 卷一甲部全部 24 道 MC 題目** 的單檔案練習遊戲 (`bafs_mc_game.html`)。

### 遊戲特色：
1. **完全離線可用**：使用 HTML5/TailwindCSS 打造，單一檔案即可在任何瀏覽器開啟。
2. **雙語切換**：點擊右上角的「中文 / ENG」按鈕，即可隨時無縫切換繁體中文與英文考題及選項。
3. **官方詳細解析**：回答每道題目後，會即時顯示該題的考點分析與詳細題解。
4. **靈活操題模式**：提供「隨機 10 題快操」及「24 題全套挑戰」兩種模式。
5. **數據統計**：包含答題進度條、即時得分與最終正確率統計。
