```html
<!DOCTYPE html>
<html lang="en" class="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Liam &amp; Amy Budget Portal</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      background-color: #020617;
      color: #f8fafc;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    }
    .tab-active {
      background: linear-gradient(135deg, #2563eb, #4f46e5);
      color: #ffffff;
      box-shadow: 0 8px 20px -4px rgba(37, 99, 235, 0.5);
      border: 1px solid rgba(96, 165, 250, 0.4);
    }
    .tab-inactive {
      background-color: #0f172a;
      color: #94a3b8;
      border: 1px solid #1e293b;
    }
    .tab-inactive:hover {
      background-color: #1e293b;
      color: #e2e8f0;
    }
  </style>
</head>
<body class="min-h-screen p-4 sm:p-6 lg:p-8">

  <div class="max-w-7xl mx-auto space-y-6">

    <!-- Top Visual Hero Banner -->
    <header class="relative rounded-3xl overflow-hidden border border-slate-800 shadow-2xl">
      <img
        src="https://images.unsplash.com/photo-1554224155-6726b3ff858f?auto=format&fit=crop&w=1600&q=80"
        alt="Financial Command Center"
        class="absolute inset-0 w-full h-full object-cover opacity-25"
      />
      <div class="absolute inset-0 bg-gradient-to-r from-slate-950 via-slate-950/90 to-blue-950/70"></div>

      <div class="relative z-10 p-6 sm:p-8 flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4">
        <div class="flex items-center gap-4">
          <div class="w-14 h-14 rounded-2xl bg-blue-600/20 border border-blue-500/40 flex items-center justify-center text-blue-400 shrink-0 shadow-inner">
            <svg class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
          </div>
          <div>
            <span class="inline-flex items-center gap-1.5 text-[11px] font-bold uppercase tracking-widest text-blue-400 bg-blue-500/10 border border-blue-500/20 px-2.5 py-0.5 rounded-full">
              Financial Hub
            </span>
            <h1 class="text-2xl sm:text-3xl font-extrabold text-white tracking-tight mt-1">
              Liam &amp; Amy Budget Portal
            </h1>
            <p class="text-xs sm:text-sm text-slate-400">
              Real-time joint household splits, personal cashflow &amp; expense tracking
            </p>
          </div>
        </div>

        <div class="flex items-center gap-3 bg-slate-900/90 backdrop-blur-md border border-slate-800 px-4 py-2.5 rounded-2xl self-start sm:self-auto">
          <span class="w-2.5 h-2.5 rounded-full bg-emerald-400"></span>
          <div class="text-xs">
            <div class="font-bold text-white text-sm">Liam &amp; Amy</div>
            <div class="text-emerald-400 font-medium">Active Fortnight</div>
          </div>
        </div>
      </div>
    </header>

    <!-- Navigation Tabs -->
    <nav class="grid grid-cols-2 sm:grid-cols-4 gap-2">
      <button id="tab-btn-household" onclick="switchTab('household')" class="tab-active py-3 px-4 rounded-xl font-semibold text-xs sm:text-sm transition flex items-center justify-center gap-2">
        <span>🏠</span>
        <span>Household Dashboard</span>
      </button>
      <button id="tab-btn-personal" onclick="switchTab('personal')" class="tab-inactive py-3 px-4 rounded-xl font-semibold text-xs sm:text-sm transition flex items-center justify-center gap-2">
        <span>💼</span>
        <span>Personal Budget</span>
      </button>
      <button id="tab-btn-hh-log" onclick="switchTab('hh-log')" class="tab-inactive py-3 px-4 rounded-xl font-semibold text-xs sm:text-sm transition flex items-center justify-center gap-2">
        <span>🧾</span>
        <span>Household Expense Log</span>
      </button>
      <button id="tab-btn-p-log" onclick="switchTab('p-log')" class="tab-inactive py-3 px-4 rounded-xl font-semibold text-xs sm:text-sm transition flex items-center justify-center gap-2">
        <span>💳</span>
        <span>Personal Expense Log</span>
      </button>
    </nav>

    <!-- ==================== TAB 1: HOUSEHOLD DASHBOARD ==================== -->
    <section id="tab-household" class="space-y-6">
      <!-- Top Surplus Cards -->
      <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5 flex items-start justify-between">
          <div>
            <div class="text-xs font-semibold uppercase tracking-wider text-slate-400">Monthly Budget Remaining</div>
            <div id="hh-kpi-monthly" class="text-2xl sm:text-3xl font-bold text-emerald-400 mt-1">$7,151.25</div>
            <div class="text-xs text-slate-500 mt-1">Total monthly unspent budget</div>
          </div>
          <div class="w-12 h-12 rounded-xl bg-emerald-500/10 border border-emerald-500/20 flex items-center justify-center text-emerald-400 text-xl shrink-0">
            💰
          </div>
        </div>

        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5 flex items-start justify-between">
          <div>
            <div class="text-xs font-semibold uppercase tracking-wider text-slate-400">Fortnightly Budget Required</div>
            <div id="hh-kpi-fortnightly" class="text-2xl sm:text-3xl font-bold text-blue-400 mt-1">$3,295.85</div>
            <div class="text-xs text-slate-500 mt-1">Equivalent per fortnight</div>
          </div>
          <div class="w-12 h-12 rounded-xl bg-blue-500/10 border border-blue-500/20 flex items-center justify-center text-blue-400 text-xl shrink-0">
            📅
          </div>
        </div>

        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5 flex items-start justify-between">
          <div>
            <div class="text-xs font-semibold uppercase tracking-wider text-slate-400">Weekly Budget Required</div>
            <div id="hh-kpi-weekly" class="text-2xl sm:text-3xl font-bold text-indigo-400 mt-1">$1,647.92</div>
            <div class="text-xs text-slate-500 mt-1">Equivalent per week</div>
          </div>
          <div class="w-12 h-12 rounded-xl bg-indigo-500/10 border border-indigo-500/20 flex items-center justify-center text-indigo-400 text-xl shrink-0">
            ⏱️
          </div>
        </div>
      </div>

      <!-- Income Split & Reconciliation Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <!-- Income Contributions & Fortnightly Split -->
        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5 overflow-x-auto">
          <div class="flex items-center gap-2.5 mb-3">
            <span class="w-8 h-8 rounded-lg bg-blue-500/10 border border-blue-500/20 flex items-center justify-center text-sm">⚖️</span>
            <h2 class="text-base font-bold text-white">Income Contributions &amp; Fortnightly Split</h2>
          </div>
          <table class="w-full text-xs sm:text-sm text-left">
            <thead class="text-slate-200 bg-blue-950/70 border-b border-blue-900 uppercase text-[11px]">
              <tr>
                <th class="py-2.5 px-3 rounded-l-lg">Contributor</th>
                <th class="py-2.5 px-3 text-right">Baseline Input</th>
                <th class="py-2.5 px-3 text-right">% Split</th>
                <th class="py-2.5 px-3 text-right rounded-r-lg">Dynamic Required</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-slate-800/70">
              <tr>
                <td class="py-2.5 px-3 font-semibold text-white">Liam</td>
                <td class="py-2.5 px-3 text-right">
                  <input id="liam-baseline" type="number" step="0.01" value="1875.00" onchange="updateContributors()" class="w-24 bg-slate-800 border border-slate-700 rounded-lg px-2 py-1 text-right text-white focus:outline-none focus:border-blue-500" />
                </td>
                <td id="liam-split-pct" class="py-2.5 px-3 text-right text-slate-300">56.4%</td>
                <td id="liam-dynamic-req" class="py-2.5 px-3 text-right font-semibold text-blue-400">$1,858.56</td>
              </tr>
              <tr>
                <td class="py-2.5 px-3 font-semibold text-white">Amy</td>
                <td class="py-2.5 px-3 text-right">
                  <input id="amy-baseline" type="number" step="0.01" value="1450.00" onchange="updateContributors()" class="w-24 bg-slate-800 border border-slate-700 rounded-lg px-2 py-1 text-right text-white focus:outline-none focus:border-blue-500" />
                </td>
                <td id="amy-split-pct" class="py-2.5 px-3 text-right text-slate-300">43.6%</td>
                <td id="amy-dynamic-req" class="py-2.5 px-3 text-right font-semibold text-blue-400">$1,437.29</td>
              </tr>
              <tr class="font-bold bg-blue-950/30">
                <td class="py-2.5 px-3 text-white rounded-l-lg">Total Fortnightly Income Pool</td>
                <td id="pool-baseline-total" class="py-2.5 px-3 text-right text-emerald-400">$3,325.00</td>
                <td class="py-2.5 px-3 text-right text-slate-300">100.0%</td>
                <td id="pool-dynamic-total" class="py-2.5 px-3 text-right text-blue-400 rounded-r-lg">$3,295.85</td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- Budget Reconciliation & Buffer -->
        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5 flex flex-col justify-between">
          <div>
            <div class="relative h-20 rounded-xl overflow-hidden mb-4 border border-slate-800">
              <img src="https://images.unsplash.com/photo-1579621970563-ebec7560ff3e?auto=format&fit=crop&w=800&q=80" alt="Savings buffer" class="w-full h-full object-cover opacity-35" />
              <div class="absolute inset-0 bg-gradient-to-r from-slate-950 via-slate-900/75 to-transparent flex items-center px-4">
                <div class="flex items-center gap-2.5">
                  <span class="w-8 h-8 rounded-lg bg-emerald-500/20 border border-emerald-500/30 flex items-center justify-center text-sm">📈</span>
                  <h2 class="text-base font-bold text-white">Budget Reconciliation &amp; Buffer</h2>
                </div>
              </div>
            </div>

            <div class="space-y-3 text-xs sm:text-sm">
              <div class="flex justify-between py-2 border-b border-slate-800">
                <span class="text-slate-400">Total Fortnightly Income Pool</span>
                <span id="rec-pool" class="font-semibold text-white">$3,325.00</span>
              </div>
              <div class="flex justify-between py-2 border-b border-slate-800">
                <span class="text-slate-400">Total Fortnightly Budget Required</span>
                <span id="rec-req" class="font-semibold text-white">$3,295.85</span>
              </div>
              <div class="flex justify-between py-2 border-b border-slate-800">
                <span class="text-slate-300 font-medium">Fortnightly Difference / Buffer (Surplus to Savings)</span>
                <span id="rec-fn-buffer" class="font-bold text-emerald-400">$29.15</span>
              </div>
              <div class="flex justify-between py-2">
                <span class="text-slate-300 font-medium">Monthly Surplus from Income</span>
                <span id="rec-mo-buffer" class="font-bold text-emerald-400">$63.17</span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Joint / Household Category Table -->
      <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-6 overflow-x-auto">
        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-2 mb-4">
          <div class="flex items-center gap-2.5">
            <span class="w-8 h-8 rounded-lg bg-indigo-500/10 border border-indigo-500/20 flex items-center justify-center text-sm">🏡</span>
            <h2 class="text-base sm:text-lg font-bold text-white">Joint Household Budget Categories</h2>
          </div>
          <span class="text-xs text-slate-400">✏️ Edit Monthly, Fortnightly, or Weekly amounts — the other columns calculate automatically</span>
        </div>
        <table class="w-full text-xs sm:text-sm text-left">
          <thead class="text-slate-200 bg-blue-950/70 border-b border-blue-900 uppercase text-[11px]">
            <tr>
              <th class="py-3 px-3 rounded-l-lg">Category</th>
              <th class="py-3 px-3 text-right">✏️ Monthly Budget</th>
              <th class="py-3 px-3 text-right">✏️ Fortnightly Budget</th>
              <th class="py-3 px-3 text-right">✏️ Weekly Budget</th>
              <th class="py-3 px-3 text-right">Actual Spend</th>
              <th class="py-3 px-3 text-right rounded-r-lg">Surplus / Remaining</th>
            </tr>
          </thead>
          <tbody id="hh-category-tbody" class="divide-y divide-slate-800/70"></tbody>
          <tfoot class="border-t-2 border-slate-700 font-bold bg-slate-800/50 text-white">
            <tr>
              <td class="py-3 px-3">Total Joint Budget</td>
              <td id="hh-tot-mo" class="py-3 px-3 text-right">$0.00</td>
              <td id="hh-tot-fn" class="py-3 px-3 text-right">$0.00</td>
              <td id="hh-tot-wk" class="py-3 px-3 text-right">$0.00</td>
              <td id="hh-tot-act" class="py-3 px-3 text-right">$0.00</td>
              <td id="hh-tot-rem" class="py-3 px-3 text-right text-emerald-400">$0.00</td>
            </tr>
          </tfoot>
        </table>
      </div>
    </section>

    <!-- ==================== TAB 2: PERSONAL BUDGET ==================== -->
    <section id="tab-personal" class="hidden space-y-6">
      <div class="relative h-24 rounded-2xl overflow-hidden border border-slate-800">
        <img src="https://images.unsplash.com/photo-1526304640581-d334cdbbf45e?auto=format&fit=crop&w=1400&q=80" alt="Personal Wealth" class="w-full h-full object-cover opacity-30" />
        <div class="absolute inset-0 bg-gradient-to-r from-slate-950 via-slate-900/85 to-transparent flex items-center justify-between px-6">
          <div class="flex items-center gap-3.5">
            <div class="w-11 h-11 rounded-2xl bg-blue-500/20 border border-blue-500/30 flex items-center justify-center text-xl">
              💼
            </div>
            <div>
              <h2 class="text-lg sm:text-xl font-bold text-white">Personal Cashflow &amp; Discretionary Tracker</h2>
              <p class="text-xs text-slate-400">Manage fortnightly take-home pay, account splits, and savings targets</p>
            </div>
          </div>
        </div>
      </div>

      <!-- Top 5 Personal KPI Cards -->
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-4">
        <div class="bg-slate-900 border border-blue-500/40 rounded-2xl p-4">
          <div class="flex items-center justify-between">
            <div class="text-[11px] font-semibold uppercase tracking-wider text-blue-300">Fortnightly Pay (Input)</div>
            <span class="w-6 h-6 rounded-md bg-blue-500/20 text-blue-400 flex items-center justify-center text-xs">✏️</span>
          </div>
          <div class="mt-2 flex items-center">
            <span class="text-xl font-bold text-blue-400 mr-1">$</span>
            <input id="p-pay-input" type="number" step="0.01" value="3400.00" onchange="updatePersonalPay()" class="w-full bg-slate-800 border border-slate-700 rounded-xl px-2.5 py-1.5 text-xl font-bold text-white focus:outline-none focus:border-blue-400" />
          </div>
          <div class="text-xs text-slate-400 mt-1.5">Base / cycle take-home pay</div>
        </div>

        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4">
          <div class="flex items-center justify-between">
            <div class="text-[11px] font-semibold uppercase tracking-wider text-slate-400">Total Fortnightly Expenses</div>
            <span>📤</span>
          </div>
          <div id="p-kpi-expenses" class="text-2xl font-bold text-white mt-2">$0.00</div>
          <div id="p-kpi-expenses-sub" class="text-xs text-slate-400 mt-1.5">Fixed + Discretionary</div>
        </div>

        <div class="bg-emerald-950/30 border border-emerald-500/40 rounded-2xl p-4">
          <div class="flex items-center justify-between">
            <div class="text-[11px] font-semibold uppercase tracking-wider text-emerald-300">Fortnightly Surplus To Save</div>
            <span>🏦</span>
          </div>
          <div id="p-kpi-fn-surplus" class="text-2xl font-bold text-emerald-400 mt-2">$0.00</div>
          <div class="text-xs text-emerald-300/70 mt-1.5">Target surplus to savings</div>
        </div>

        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4">
          <div class="flex items-center justify-between">
            <div class="text-[11px] font-semibold uppercase tracking-wider text-slate-400">Weekly Surplus Equivalent</div>
            <span>⏱️</span>
          </div>
          <div id="p-kpi-wk-surplus" class="text-2xl font-bold text-indigo-400 mt-2">$0.00</div>
          <div id="p-kpi-wk-sub" class="text-xs text-slate-400 mt-1.5">Equiv. Pay: $1,700.00</div>
        </div>

        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4">
          <div class="flex items-center justify-between">
            <div class="text-[11px] font-semibold uppercase tracking-wider text-slate-400">Monthly Surplus Equivalent</div>
            <span>🗓️</span>
          </div>
          <div id="p-kpi-mo-surplus" class="text-2xl font-bold text-blue-400 mt-2">$0.00</div>
          <div id="p-kpi-mo-sub" class="text-xs text-slate-400 mt-1.5">Equiv. Pay: $7,366.67</div>
        </div>
      </div>

      <!-- Personal Budget Category Table -->
      <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-6 overflow-x-auto">
        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-2 mb-4">
          <div class="flex items-center gap-2.5">
            <span class="w-8 h-8 rounded-lg bg-blue-500/10 border border-blue-500/20 flex items-center justify-center text-sm">📋</span>
            <h2 class="text-base sm:text-lg font-bold text-white">Personal Budget Breakdown</h2>
          </div>
          <span class="text-xs text-slate-400">✏️ Edit Monthly, Fortnightly, or Weekly targets — the other columns calculate automatically</span>
        </div>
        <table class="w-full text-xs sm:text-sm text-left">
          <thead class="text-slate-200 bg-blue-950/70 border-b border-blue-900 uppercase text-[11px]">
            <tr>
              <th class="py-3 px-3 rounded-l-lg">Category</th>
              <th class="py-3 px-3 text-right">✏️ Monthly Budget</th>
              <th class="py-3 px-3 text-right">✏️ Fortnightly Budget</th>
              <th class="py-3 px-3 text-right">✏️ Weekly Budget</th>
              <th class="py-3 px-3 text-right">Actual Spend (FN)</th>
              <th class="py-3 px-3 text-right rounded-r-lg">Surplus / Remaining (FN)</th>
            </tr>
          </thead>
          <tbody id="p-category-tbody" class="divide-y divide-slate-800/70"></tbody>
          <tfoot class="border-t-2 border-slate-700 font-bold bg-slate-800/50 text-white">
            <tr>
              <td class="py-3 px-3">Total Personal Budget</td>
              <td id="p-tot-mo" class="py-3 px-3 text-right">$0.00</td>
              <td id="p-tot-fn" class="py-3 px-3 text-right">$0.00</td>
              <td id="p-tot-wk" class="py-3 px-3 text-right">$0.00</td>
              <td id="p-tot-act" class="py-3 px-3 text-right">$0.00</td>
              <td id="p-tot-rem" class="py-3 px-3 text-right text-emerald-400">$0.00</td>
            </tr>
          </tfoot>
        </table>
      </div>

      <!-- Account Distribution Split & Reconciliation Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <!-- Account Distribution Split -->
        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5 overflow-x-auto">
          <h2 class="text-base font-bold text-white mb-3">Account Distribution Split (Discretionary &amp; Bills)</h2>
          <table class="w-full text-xs sm:text-sm text-left">
            <thead class="text-slate-200 bg-blue-950/70 border-b border-blue-900 uppercase text-[11px]">
              <tr>
                <th class="py-2.5 px-3 rounded-l-lg">Account</th>
                <th class="py-2.5 px-3 text-right">Monthly</th>
                <th class="py-2.5 px-3 text-right">Fortnightly</th>
                <th class="py-2.5 px-3 text-right">Weekly</th>
                <th class="py-2.5 px-3 text-right">Actual</th>
                <th class="py-2.5 px-3 text-right rounded-r-lg">Remaining</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-slate-800/70">
              <tr>
                <td class="py-2.5 px-3 font-semibold text-white">
                  <div class="flex items-center gap-2">
                    <span class="w-7 h-7 rounded-lg bg-purple-500/15 text-purple-400 flex items-center justify-center">💳</span>
                    <span>Spending Account</span>
                  </div>
                </td>
                <td id="acc-spend-mo" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="acc-spend-fn" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="acc-spend-wk" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="acc-spend-act" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="acc-spend-rem" class="py-2.5 px-3 text-right text-emerald-400">$0.00</td>
              </tr>
              <tr>
                <td class="py-2.5 px-3 font-semibold text-white">
                  <div class="flex items-center gap-2">
                    <span class="w-7 h-7 rounded-lg bg-amber-500/15 text-amber-400 flex items-center justify-center">🧾</span>
                    <span>Bills Account</span>
                  </div>
                </td>
                <td id="acc-bills-mo" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="acc-bills-fn" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="acc-bills-wk" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="acc-bills-act" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="acc-bills-rem" class="py-2.5 px-3 text-right text-emerald-400">$0.00</td>
              </tr>
              <tr class="font-bold bg-blue-950/30 text-white">
                <td class="py-2.5 px-3 rounded-l-lg">Total Personal (Excl. Joint)</td>
                <td id="acc-tot-mo" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="acc-tot-fn" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="acc-tot-wk" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="acc-tot-act" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="acc-tot-rem" class="py-2.5 px-3 text-right text-emerald-400 rounded-r-lg">$0.00</td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- Annualized & Multi-Frequency Savings Overview -->
        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5 overflow-x-auto">
          <h2 class="text-base font-bold text-white mb-3">Annualized &amp; Multi-Frequency Savings Overview</h2>
          <table class="w-full text-xs sm:text-sm text-left">
            <thead class="text-slate-200 bg-blue-950/70 border-b border-blue-900 uppercase text-[11px]">
              <tr>
                <th class="py-2.5 px-3 rounded-l-lg">Frequency</th>
                <th class="py-2.5 px-3 text-right">Take-Home Pay</th>
                <th class="py-2.5 px-3 text-right">Budget Expenses</th>
                <th class="py-2.5 px-3 text-right rounded-r-lg">Target Surplus</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-slate-800/70">
              <tr>
                <td class="py-2.5 px-3 font-semibold text-white">⏱️ Weekly</td>
                <td id="freq-wk-pay" class="py-2.5 px-3 text-right">$1,700.00</td>
                <td id="freq-wk-exp" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="freq-wk-sur" class="py-2.5 px-3 text-right font-semibold text-emerald-400">$0.00</td>
              </tr>
              <tr>
                <td class="py-2.5 px-3 font-semibold text-white">📅 Fortnightly</td>
                <td id="freq-fn-pay" class="py-2.5 px-3 text-right">$3,400.00</td>
                <td id="freq-fn-exp" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="freq-fn-sur" class="py-2.5 px-3 text-right font-semibold text-emerald-400">$0.00</td>
              </tr>
              <tr>
                <td class="py-2.5 px-3 font-semibold text-white">🗓️ Monthly</td>
                <td id="freq-mo-pay" class="py-2.5 px-3 text-right">$7,366.67</td>
                <td id="freq-mo-exp" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="freq-mo-sur" class="py-2.5 px-3 text-right font-semibold text-emerald-400">$0.00</td>
              </tr>
              <tr class="font-bold bg-blue-950/30 text-white">
                <td class="py-2.5 px-3 rounded-l-lg">🎯 Annual (26 Pays)</td>
                <td id="freq-yr-pay" class="py-2.5 px-3 text-right">$88,400.00</td>
                <td id="freq-yr-exp" class="py-2.5 px-3 text-right">$0.00</td>
                <td id="freq-yr-sur" class="py-2.5 px-3 text-right text-emerald-400 rounded-r-lg">$0.00</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>

      <!-- Fortnightly Pay Reconciliation & Surplus Buffer -->
      <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5 overflow-x-auto">
        <h2 class="text-base font-bold text-white mb-3">Fortnightly Pay Reconciliation &amp; Surplus Buffer</h2>
        <table class="w-full text-xs sm:text-sm text-left">
          <thead class="text-slate-200 bg-blue-950/70 border-b border-blue-900 uppercase text-[11px]">
            <tr>
              <th class="py-2.5 px-3 rounded-l-lg">Component</th>
              <th class="py-2.5 px-3 text-right">Budgeted</th>
              <th class="py-2.5 px-3 text-right">Actual to Date</th>
              <th class="py-2.5 px-3 text-right rounded-r-lg">Variance / Buffer</th>
            </tr>
          </thead>
          <tbody class="divide-y divide-slate-800/70">
            <tr>
              <td class="py-2.5 px-3 font-semibold text-white">💵 Fortnightly Take-Home Pay</td>
              <td id="p-rec-pay-bud" class="py-2.5 px-3 text-right">$3,400.00</td>
              <td id="p-rec-pay-act" class="py-2.5 px-3 text-right">$3,400.00</td>
              <td class="py-2.5 px-3 text-right">$0.00</td>
            </tr>
            <tr>
              <td class="py-2.5 px-3 text-slate-300">🏡 Less: Fixed Household Transfer</td>
              <td id="p-rec-hh-bud" class="py-2.5 px-3 text-right">$1,875.00</td>
              <td id="p-rec-hh-act" class="py-2.5 px-3 text-right">$0.00</td>
              <td id="p-rec-hh-var" class="py-2.5 px-3 text-right">$1,875.00</td>
            </tr>
            <tr>
              <td class="py-2.5 px-3 text-slate-300">🛍️ Less: Personal Discretionary Spending</td>
              <td id="p-rec-disc-bud" class="py-2.5 px-3 text-right">$0.00</td>
              <td id="p-rec-disc-act" class="py-2.5 px-3 text-right">$0.00</td>
              <td id="p-rec-disc-var" class="py-2.5 px-3 text-right">$0.00</td>
            </tr>
            <tr class="font-semibold">
              <td class="py-2.5 px-3 text-white">📤 Total Fortnightly Outflows</td>
              <td id="p-rec-out-bud" class="py-2.5 px-3 text-right">$0.00</td>
              <td id="p-rec-out-act" class="py-2.5 px-3 text-right">$0.00</td>
              <td id="p-rec-out-var" class="py-2.5 px-3 text-right">$0.00</td>
            </tr>
            <tr class="font-bold bg-blue-950/40 text-emerald-400">
              <td class="py-2.5 px-3 rounded-l-lg">🏦 Net Surplus Available to Transfer to Savings</td>
              <td id="p-rec-net-bud" class="py-2.5 px-3 text-right">$0.00</td>
              <td id="p-rec-net-act" class="py-2.5 px-3 text-right">$3,400.00</td>
              <td id="p-rec-net-var" class="py-2.5 px-3 text-right rounded-r-lg">$0.00</td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <!-- ==================== TAB 3: HOUSEHOLD EXPENSE LOG ==================== -->
    <section id="tab-hh-log" class="hidden space-y-6">
      <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-6">
        <div class="relative h-24 rounded-xl overflow-hidden mb-5 border border-slate-800">
          <img src="https://images.unsplash.com/photo-1556742049-0cfed4f6a45d?auto=format&fit=crop&w=1200&q=80" alt="Household Receipts" class="w-full h-full object-cover opacity-30" />
          <div class="absolute inset-0 bg-gradient-to-r from-slate-950 via-slate-900/80 to-transparent flex flex-col justify-center px-5">
            <h2 class="text-base sm:text-lg font-bold text-white">🧾 Household Quick Expense Log</h2>
            <p class="text-xs text-slate-400">Log purchases below to automatically update Household Dashboard actual spend and remaining surplus.</p>
          </div>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-4 gap-3 mb-6">
          <input id="hh-log-date" type="date" class="bg-slate-800 border border-slate-700 rounded-xl px-3 py-2 text-sm text-white" />
          <select id="hh-log-cat" class="bg-slate-800 border border-slate-700 rounded-xl px-3 py-2 text-sm text-white"></select>
          <input id="hh-log-desc" type="text" placeholder="Description" class="bg-slate-800 border border-slate-700 rounded-xl px-3 py-2 text-sm text-white" />
          <div class="flex gap-2">
            <input id="hh-log-amt" type="number" step="0.01" placeholder="Amount ($)" class="w-full bg-slate-800 border border-slate-700 rounded-xl px-3 py-2 text-sm text-white" />
            <button onclick="addExpense('hh')" class="px-4 py-2 bg-blue-600 hover:bg-blue-500 text-white font-semibold rounded-xl text-sm whitespace-nowrap">Add</button>
          </div>
        </div>

        <div class="overflow-x-auto">
          <table class="w-full text-xs sm:text-sm text-left">
            <thead class="text-slate-200 bg-blue-950/70 border-b border-blue-900 uppercase text-[11px]">
              <tr>
                <th class="py-2.5 px-3 rounded-l-lg">Date</th>
                <th class="py-2.5 px-3">Category</th>
                <th class="py-2.5 px-3">Description</th>
                <th class="py-2.5 px-3 text-right">Amount</th>
                <th class="py-2.5 px-3 text-right rounded-r-lg">Action</th>
              </tr>
            </thead>
            <tbody id="hh-log-tbody" class="divide-y divide-slate-800/70"></tbody>
          </table>
        </div>
      </div>
    </section>

    <!-- ==================== TAB 4: PERSONAL EXPENSE LOG ==================== -->
    <section id="tab-p-log" class="hidden space-y-6">
      <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-6">
        <div class="relative h-24 rounded-xl overflow-hidden mb-5 border border-slate-800">
          <img src="https://images.unsplash.com/photo-1563013544-824ae1b704d3?auto=format&fit=crop&w=1200&q=80" alt="Personal Transactions" class="w-full h-full object-cover opacity-30" />
          <div class="absolute inset-0 bg-gradient-to-r from-slate-950 via-slate-900/80 to-transparent flex flex-col justify-center px-5">
            <h2 class="text-base sm:text-lg font-bold text-white">💳 Personal Expense Log</h2>
            <p class="text-xs text-slate-400">Select a category for each personal transaction to automatically sync with your Personal Budget actual spend.</p>
          </div>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-4 gap-3 mb-6">
          <input id="p-log-date" type="date" class="bg-slate-800 border border-slate-700 rounded-xl px-3 py-2 text-sm text-white" />
          <select id="p-log-cat" class="bg-slate-800 border border-slate-700 rounded-xl px-3 py-2 text-sm text-white"></select>
          <input id="p-log-desc" type="text" placeholder="Description" class="bg-slate-800 border border-slate-700 rounded-xl px-3 py-2 text-sm text-white" />
          <div class="flex gap-2">
            <input id="p-log-amt" type="number" step="0.01" placeholder="Amount ($)" class="w-full bg-slate-800 border border-slate-700 rounded-xl px-3 py-2 text-sm text-white" />
            <button onclick="addExpense('p')" class="px-4 py-2 bg-blue-600 hover:bg-blue-500 text-white font-semibold rounded-xl text-sm whitespace-nowrap">Add</button>
          </div>
        </div>

        <div class="overflow-x-auto">
          <table class="w-full text-xs sm:text-sm text-left">
            <thead class="text-slate-200 bg-blue-950/70 border-b border-blue-900 uppercase text-[11px]">
              <tr>
                <th class="py-2.5 px-3 rounded-l-lg">Date</th>
                <th class="py-2.5 px-3">Category</th>
                <th class="py-2.5 px-3">Description</th>
                <th class="py-2.5 px-3 text-right">Amount</th>
                <th class="py-2.5 px-3 text-right rounded-r-lg">Action</th>
              </tr>
            </thead>
            <tbody id="p-log-tbody" class="divide-y divide-slate-800/70"></tbody>
            <tfoot class="border-t-2 border-slate-700 font-bold text-white">
              <tr>
                <td colspan="3" class="py-3 px-3">Total Personal Logged Spend</td>
                <td id="p-log-total" class="py-3 px-3 text-right text-emerald-400">$0.00</td>
                <td></td>
              </tr>
            </tfoot>
          </table>
        </div>
      </div>
    </section>

  </div>

  <script>
    // Default Joint / Household Categories
    const defaultHhCategories = [
      { id: 'hh-1', name: 'Mortgage', group: 'Housing', monthly: 2450.00, icon: '🏠' },
      { id: 'hh-2', name: 'Groceries', group: 'Essentials', monthly: 1275.00, icon: '🛒' },
      { id: 'hh-3', name: 'Ollie Daycare', group: 'Family', monthly: 1205.00, icon: '👶' },
      { id: 'hh-4', name: 'Power', group: 'Utilities', monthly: 450.00, icon: '⚡' },
      { id: 'hh-5', name: 'Take Out', group: 'Lifestyle', monthly: 350.00, icon: '🍔' },
      { id: 'hh-6', name: 'Cleaner', group: 'Upkeep', monthly: 305.00, icon: '🧹' },
      { id: 'hh-7', name: 'House Insurance', group: 'Protection', monthly: 245.00, icon: '🛡️' },
      { id: 'hh-8', name: 'Mum Repayment', group: 'Liabilities', monthly: 160.00, icon: '🤝' },
      { id: 'hh-9', name: 'Lilly Food', group: 'Pets', monthly: 160.00, icon: '🐶' },
      { id: 'hh-10', name: 'Petrol', group: 'Transport', monthly: 130.00, icon: '⛽' },
      { id: 'hh-11', name: 'Internet', group: 'Utilities', monthly: 113.00, icon: '📡' },
      { id: 'hh-12', name: 'Christmas Savings', group: 'Savings', monthly: 88.00, icon: '🎄' },
      { id: 'hh-13', name: 'Contents Insurance', group: 'Protection', monthly: 76.00, icon: '📦' },
      { id: 'hh-14', name: 'Lilly Insurance', group: 'Pets', monthly: 72.00, icon: '🐾' },
      { id: 'hh-15', name: 'Rubbish', group: 'Utilities', monthly: 50.00, icon: '🗑️' },
      { id: 'hh-16', name: 'RockGas Annual Fee', group: 'Utilities', monthly: 12.00, icon: '🔥' },
      { id: 'hh-17', name: 'Emby', group: 'Subscriptions', monthly: 10.25, icon: '💻' }
    ];

    // Default Personal Categories
    const defaultPCategories = [
      { id: 'p-1', name: 'Joint Household Contribution', account: 'Joint', monthly: 4062.50, icon: '🏡' },
      { id: 'p-2', name: 'Loan Repayments', account: 'Bills', monthly: 780.00, icon: '💳' },
      { id: 'p-3', name: 'Personal Dining, Coffee & Social', account: 'Spending', monthly: 650.00, icon: '☕' },
      { id: 'p-4', name: 'Health, Gym & Medical Insurance', account: 'Bills', monthly: 545.00, icon: '💪' },
      { id: 'p-5', name: 'Petrol', account: 'Spending', monthly: 542.00, icon: '⛽' },
      { id: 'p-6', name: 'Car Rego, Servicing & Insurance', account: 'Bills', monthly: 520.00, icon: '🚗' },
      { id: 'p-7', name: 'Clothing, Grooming & Hobby', account: 'Spending', monthly: 443.00, icon: '🛍️' },
      { id: 'p-8', name: 'Smokes', account: 'Spending', monthly: 364.00, icon: '🚬' },
      { id: 'p-9', name: 'Mobile Phone & Personal Apps', account: 'Bills', monthly: 240.00, icon: '📱' },
      { id: 'p-10', name: 'Lunches', account: 'Spending', monthly: 260.00, icon: '🥪' },
      { id: 'p-11', name: 'Parking', account: 'Spending', monthly: 130.00, icon: '🅿️' },
      { id: 'p-12', name: 'Barber', account: 'Spending', monthly: 130.00, icon: '✂️' },
      { id: 'p-13', name: 'Alcohol', account: 'Spending', monthly: 87.00, icon: '🍷' },
      { id: 'p-14', name: 'Emby', account: 'Spending', monthly: 40.00, icon: '💻' }
    ];

    // Load from localStorage or defaults
    let hhCategories = JSON.parse(localStorage.getItem('hh_categories')) || defaultHhCategories;
    let pCategories = JSON.parse(localStorage.getItem('p_categories')) || defaultPCategories;
    let hhExpenses = JSON.parse(localStorage.getItem('hh_expenses')) || [];
    let pExpenses = JSON.parse(localStorage.getItem('p_expenses')) || [
      { id: 1, date: '2025-02-14', cat: 'Personal Dining, Coffee & Social', desc: 'Friday team lunch & coffee', amt: 24.50 },
      { id: 2, date: '2025-02-16', cat: 'Mobile Phone & Personal Apps', desc: 'Spotify Family plan', amt: 18.99 },
      { id: 3, date: '2025-02-18', cat: 'Personal Dining, Coffee & Social', desc: 'Morning flat white', amt: 6.50 },
      { id: 4, date: '2025-02-20', cat: 'Clothing, Grooming & Hobby', desc: 'Weekend book purchase', amt: 35.00 },
      { id: 5, date: '2025-02-22', cat: 'Clothing, Grooming & Hobby', desc: 'Electronics parts for DIY project', amt: 42.50 }
    ];
    let liamBaseline = localStorage.getItem('liam_baseline') ? parseFloat(localStorage.getItem('liam_baseline')) : 1875.00;
    let amyBaseline = localStorage.getItem('amy_baseline') ? parseFloat(localStorage.getItem('amy_baseline')) : 1450.00;
    let personalPay = localStorage.getItem('personal_pay') ? parseFloat(localStorage.getItem('personal_pay')) : 3400.00;

    // Set initial input values
    document.getElementById('liam-baseline').value = liamBaseline.toFixed(2);
    document.getElementById('amy-baseline').value = amyBaseline.toFixed(2);
    document.getElementById('p-pay-input').value = personalPay.toFixed(2);
    document.getElementById('hh-log-date').value = new Date().toISOString().slice(0, 10);
    document.getElementById('p-log-date').value = new Date().toISOString().slice(0, 10);

    function saveData() {
      localStorage.setItem('hh_categories', JSON.stringify(hhCategories));
      localStorage.setItem('p_categories', JSON.stringify(pCategories));
      localStorage.setItem('hh_expenses', JSON.stringify(hhExpenses));
      localStorage.setItem('p_expenses', JSON.stringify(pExpenses));
      localStorage.setItem('liam_baseline', document.getElementById('liam-baseline').value);
      localStorage.setItem('amy_baseline', document.getElementById('amy-baseline').value);
      localStorage.setItem('personal_pay', document.getElementById('p-pay-input').value);
    }

    const fmt = (n) => '$' + Number(n || 0).toLocaleString('en-US', { minimumFractionDigits: 2, maximumFractionDigits: 2 });

    function getCategoryIcon(type, catName) {
      const list = type === 'hh' ? hhCategories : pCategories;
      const found = list.find(c => c.name === catName);
      return found ? found.icon : '📌';
    }

    function switchTab(tab) {
      ['household', 'personal', 'hh-log', 'p-log'].forEach(t => {
        document.getElementById('tab-' + t).classList.toggle('hidden', t !== tab);
        const btn = document.getElementById('tab-btn-' + t);
        btn.className = (t === tab ? 'tab-active' : 'tab-inactive') + ' py-3 px-4 rounded-xl font-semibold text-xs sm:text-sm transition flex items-center justify-center gap-2';
      });
    }

    // Render Joint Household Table
    function renderHousehold() {
      const tbody = document.getElementById('hh-category-tbody');
      tbody.innerHTML = '';

      let totMo = 0, totFn = 0, totWk = 0, totAct = 0;

      hhCategories.forEach((cat, idx) => {
        const mo = cat.monthly;
        const fn = (mo * 12) / 26;
        const wk = (mo * 12) / 52;
        const actual = hhExpenses.filter(e => e.cat === cat.name).reduce((s, e) => s + e.amt, 0);
        const rem = mo - actual;

        totMo += mo;
        totFn += fn;
        totWk += wk;
        totAct += actual;

        tbody.innerHTML += `
          <tr class="hover:bg-slate-800/30 transition">
            <td class="py-3 px-3 font-medium text-white">
              <div class="flex items-center gap-2.5">
                <span class="w-8 h-8 rounded-lg bg-slate-800 border border-slate-700 flex items-center justify-center text-base shrink-0">${cat.icon}</span>
                <div>
                  <div>${cat.name}</div>
                  <span class="text-[10px] uppercase tracking-wider px-1.5 py-0.5 rounded bg-slate-800 text-slate-400">${cat.group}</span>
                </div>
              </div>
            </td>
            <td class="py-3 px-3 text-right">
              <input type="number" step="0.01" value="${mo.toFixed(2)}" onchange="updateHhCat(${idx}, 'mo', this.value)"
                class="w-28 bg-slate-800 border border-slate-700 rounded-lg px-2 py-1 text-right text-white focus:outline-none focus:border-blue-500" />
            </td>
            <td class="py-3 px-3 text-right">
              <input type="number" step="0.01" value="${fn.toFixed(2)}" onchange="updateHhCat(${idx}, 'fn', this.value)"
                class="w-28 bg-slate-800 border border-slate-700 rounded-lg px-2 py-1 text-right text-blue-300 focus:outline-none focus:border-blue-500" />
            </td>
            <td class="py-3 px-3 text-right">
              <input type="number" step="0.01" value="${wk.toFixed(2)}" onchange="updateHhCat(${idx}, 'wk', this.value)"
                class="w-28 bg-slate-800 border border-slate-700 rounded-lg px-2 py-1 text-right text-indigo-300 focus:outline-none focus:border-blue-500" />
            </td>
            <td class="py-3 px-3 text-right text-slate-300">${fmt(actual)}</td>
            <td class="py-3 px-3 text-right font-semibold ${rem >= 0 ? 'text-emerald-400' : 'text-rose-400'}">${fmt(rem)}</td>
          </tr>
        `;
      });

      const totRem = totMo - totAct;
      document.getElementById('hh-tot-mo').textContent = fmt(totMo);
      document.getElementById('hh-tot-fn').textContent = fmt(totFn);
      document.getElementById('hh-tot-wk').textContent = fmt(totWk);
      document.getElementById('hh-tot-act').textContent = fmt(totAct);
      document.getElementById('hh-tot-rem').textContent = fmt(totRem);

      document.getElementById('hh-kpi-monthly').textContent = fmt(totRem);
      document.getElementById('hh-kpi-fortnightly').textContent = fmt(totFn);
      document.getElementById('hh-kpi-weekly').textContent = fmt(totWk);

      updateContributors(totFn);
      saveData();
    }

    function updateHhCat(idx, period, val) {
      const num = parseFloat(val) || 0;
      if (period === 'mo') {
        hhCategories[idx].monthly = num;
      } else if (period === 'fn') {
        hhCategories[idx].monthly = (num * 26) / 12;
      } else if (period === 'wk') {
        hhCategories[idx].monthly = (num * 52) / 12;
      }
      renderHousehold();
    }

    function updateContributors(fnRequiredOverride) {
      const liam = parseFloat(document.getElementById('liam-baseline').value) || 0;
      const amy = parseFloat(document.getElementById('amy-baseline').value) || 0;
      const pool = liam + amy;

      const totMo = hhCategories.reduce((s, c) => s + c.monthly, 0);
      const fnReq = fnRequiredOverride !== undefined ? fnRequiredOverride : (totMo * 12) / 26;

      const liamPct = pool > 0 ? (liam / pool) : 0;
      const amyPct = pool > 0 ? (amy / pool) : 0;

      document.getElementById('liam-split-pct').textContent = (liamPct * 100).toFixed(1) + '%';
      document.getElementById('amy-split-pct').textContent = (amyPct * 100).toFixed(1) + '%';
      document.getElementById('liam-dynamic-req').textContent = fmt(fnReq * liamPct);
      document.getElementById('amy-dynamic-req').textContent = fmt(fnReq * amyPct);
      document.getElementById('pool-baseline-total').textContent = fmt(pool);
      document.getElementById('pool-dynamic-total').textContent = fmt(fnReq);

      const fnBuffer = pool - fnReq;
      const moBuffer = (fnBuffer * 26) / 12;
      document.getElementById('rec-pool').textContent = fmt(pool);
      document.getElementById('rec-req').textContent = fmt(fnReq);
      document.getElementById('rec-fn-buffer').textContent = fmt(fnBuffer);
      document.getElementById('rec-mo-buffer').textContent = fmt(moBuffer);
      saveData();
    }

    // Render Personal Table
    function renderPersonal() {
      const tbody = document.getElementById('p-category-tbody');
      tbody.innerHTML = '';

      let totMo = 0, totFn = 0, totWk = 0, totAct = 0;
      let spendMo = 0, spendFn = 0, spendWk = 0, spendAct = 0;
      let billsMo = 0, billsFn = 0, billsWk = 0, billsAct = 0;
      let hhFnBud = 0, hhFnAct = 0;

      pCategories.forEach((cat, idx) => {
        const mo = cat.monthly;
        const fn = (mo * 12) / 26;
        const wk = (mo * 12) / 52;
        const actual = pExpenses.filter(e => e.cat === cat.name).reduce((s, e) => s + e.amt, 0);
        const rem = fn - actual;

        totMo += mo;
        totFn += fn;
        totWk += wk;
        totAct += actual;

        if (cat.account === 'Spending') {
          spendMo += mo; spendFn += fn; spendWk += wk; spendAct += actual;
        } else if (cat.account === 'Bills') {
          billsMo += mo; billsFn += fn; billsWk += wk; billsAct += actual;
        } else {
          hhFnBud += fn; hhFnAct += actual;
        }

        tbody.innerHTML += `
          <tr class="hover:bg-slate-800/30 transition">
            <td class="py-3 px-3 font-medium text-white">
              <div class="flex items-center gap-2.5">
                <span class="w-8 h-8 rounded-lg bg-slate-800 border border-slate-700 flex items-center justify-center text-base shrink-0">${cat.icon}</span>
                <div>
                  <div>${cat.name}</div>
                  <span class="text-[10px] uppercase tracking-wider px-1.5 py-0.5 rounded bg-slate-800 text-slate-400">${cat.account}</span>
                </div>
              </div>
            </td>
            <td class="py-3 px-3 text-right">
              <input type="number" step="0.01" value="${mo.toFixed(2)}" onchange="updatePCat(${idx}, 'mo', this.value)"
                class="w-28 bg-slate-800 border border-slate-700 rounded-lg px-2 py-1 text-right text-white focus:outline-none focus:border-blue-500" />
            </td>
            <td class="py-3 px-3 text-right">
              <input type="number" step="0.01" value="${fn.toFixed(2)}" onchange="updatePCat(${idx}, 'fn', this.value)"
                class="w-28 bg-slate-800 border border-slate-700 rounded-lg px-2 py-1 text-right text-blue-300 focus:outline-none focus:border-blue-500" />
            </td>
            <td class="py-3 px-3 text-right">
              <input type="number" step="0.01" value="${wk.toFixed(2)}" onchange="updatePCat(${idx}, 'wk', this.value)"
                class="w-28 bg-slate-800 border border-slate-700 rounded-lg px-2 py-1 text-right text-indigo-300 focus:outline-none focus:border-blue-500" />
            </td>
            <td class="py-3 px-3 text-right text-slate-300">${fmt(actual)}</td>
            <td class="py-3 px-3 text-right font-semibold ${rem >= 0 ? 'text-emerald-400' : 'text-rose-400'}">${fmt(rem)}</td>
          </tr>
        `;
      });

      document.getElementById('p-tot-mo').textContent = fmt(totMo);
      document.getElementById('p-tot-fn').textContent = fmt(totFn);
      document.getElementById('p-tot-wk').textContent = fmt(totWk);
      document.getElementById('p-tot-act').textContent = fmt(totAct);
      document.getElementById('p-tot-rem').textContent = fmt(totFn - totAct);

      // Account Splits
      document.getElementById('acc-spend-mo').textContent = fmt(spendMo);
      document.getElementById('acc-spend-fn').textContent = fmt(spendFn);
      document.getElementById('acc-spend-wk').textContent = fmt(spendWk);
      document.getElementById('acc-spend-act').textContent = fmt(spendAct);
      document.getElementById('acc-spend-rem').textContent = fmt(spendFn - spendAct);

      document.getElementById('acc-bills-mo').textContent = fmt(billsMo);
      document.getElementById('acc-bills-fn').textContent = fmt(billsFn);
      document.getElementById('acc-bills-wk').textContent = fmt(billsWk);
      document.getElementById('acc-bills-act').textContent = fmt(billsAct);
      document.getElementById('acc-bills-rem').textContent = fmt(billsFn - billsAct);

      const discMo = spendMo + billsMo, discFn = spendFn + billsFn, discWk = spendWk + billsWk, discAct = spendAct + billsAct;
      document.getElementById('acc-tot-mo').textContent = fmt(discMo);
      document.getElementById('acc-tot-fn').textContent = fmt(discFn);
      document.getElementById('acc-tot-wk').textContent = fmt(discWk);
      document.getElementById('acc-tot-act').textContent = fmt(discAct);
      document.getElementById('acc-tot-rem').textContent = fmt(discFn - discAct);

      updatePersonalPay(hhFnBud, hhFnAct, discFn, discAct);
      saveData();
    }

    function updatePCat(idx, period, val) {
      const num = parseFloat(val) || 0;
      if (period === 'mo') {
        pCategories[idx].monthly = num;
      } else if (period === 'fn') {
        pCategories[idx].monthly = (num * 26) / 12;
      } else if (period === 'wk') {
        pCategories[idx].monthly = (num * 52) / 12;
      }
      renderPersonal();
    }

    function updatePersonalPay(hhFnBudOverride, hhFnActOverride, discFnOverride, discActOverride) {
      const fnPay = parseFloat(document.getElementById('p-pay-input').value) || 0;
      const wkPay = fnPay / 2;
      const moPay = (fnPay * 26) / 12;
      const yrPay = fnPay * 26;

      const totMoExp = pCategories.reduce((s, c) => s + c.monthly, 0);
      const totFnExp = (totMoExp * 12) / 26;
      const totWkExp = totFnExp / 2;
      const totYrExp = totFnExp * 26;

      const fnSurplus = fnPay - totFnExp;
      const wkSurplus = wkPay - totWkExp;
      const moSurplus = moPay - totMoExp;
      const yrSurplus = yrPay - totYrExp;

      const hhCat = pCategories.find(c => c.account === 'Joint');
      const hhFnBud = hhFnBudOverride !== undefined ? hhFnBudOverride : (hhCat ? (hhCat.monthly * 12) / 26 : 0);
      const hhFnAct = hhFnActOverride !== undefined ? hhFnActOverride : (hhCat ? pExpenses.filter(e => e.cat === hhCat.name).reduce((s, e) => s + e.amt, 0) : 0);
      const discFnBud = discFnOverride !== undefined ? discFnOverride : (totFnExp - hhFnBud);
      const discFnAct = discActOverride !== undefined ? discActOverride : (pExpenses.reduce((s, e) => s + e.amt, 0) - hhFnAct);

      document.getElementById('p-kpi-expenses').textContent = fmt(totFnExp);
      document.getElementById('p-kpi-expenses-sub').textContent = `Fixed (${fmt(hhFnBud)}) + Discretionary`;
      document.getElementById('p-kpi-fn-surplus').textContent = fmt(fnSurplus);
      document.getElementById('p-kpi-wk-surplus').textContent = fmt(wkSurplus);
      document.getElementById('p-kpi-wk-sub').textContent = 'Equiv. Pay: ' + fmt(wkPay);
      document.getElementById('p-kpi-mo-surplus').textContent = fmt(moSurplus);
      document.getElementById('p-kpi-mo-sub').textContent = 'Equiv. Pay: ' + fmt(moPay);

      document.getElementById('freq-wk-pay').textContent = fmt(wkPay);
      document.getElementById('freq-wk-exp').textContent = fmt(totWkExp);
      document.getElementById('freq-wk-sur').textContent = fmt(wkSurplus);

      document.getElementById('freq-fn-pay').textContent = fmt(fnPay);
      document.getElementById('freq-fn-exp').textContent = fmt(totFnExp);
      document.getElementById('freq-fn-sur').textContent = fmt(fnSurplus);

      document.getElementById('freq-mo-pay').textContent = fmt(moPay);
      document.getElementById('freq-mo-exp').textContent = fmt(totMoExp);
      document.getElementById('freq-mo-sur').textContent = fmt(moSurplus);

      document.getElementById('freq-yr-pay').textContent = fmt(yrPay);
      document.getElementById('freq-yr-exp').textContent = fmt(totYrExp);
      document.getElementById('freq-yr-sur').textContent = fmt(yrSurplus);

      // Reconciliation Table
      const totOutAct = hhFnAct + discFnAct;
      document.getElementById('p-rec-pay-bud').textContent = fmt(fnPay);
      document.getElementById('p-rec-pay-act').textContent = fmt(fnPay);
      document.getElementById('p-rec-hh-bud').textContent = fmt(hhFnBud);
      document.getElementById('p-rec-hh-act').textContent = fmt(hhFnAct);
      document.getElementById('p-rec-hh-var').textContent = fmt(hhFnBud - hhFnAct);
      document.getElementById('p-rec-disc-bud').textContent = fmt(discFnBud);
      document.getElementById('p-rec-disc-act').textContent = fmt(discFnAct);
      document.getElementById('p-rec-disc-var').textContent = fmt(discFnBud - discFnAct);
      document.getElementById('p-rec-out-bud').textContent = fmt(totFnExp);
      document.getElementById('p-rec-out-act').textContent = fmt(totOutAct);
      document.getElementById('p-rec-out-var').textContent = fmt(totFnExp - totOutAct);
      document.getElementById('p-rec-net-bud').textContent = fmt(fnSurplus);
      document.getElementById('p-rec-net-act').textContent = fmt(fnPay - totOutAct);
      document.getElementById('p-rec-net-var').textContent = fmt((fnPay - totOutAct) - fnSurplus);
      saveData();
    }

    function populateDropdowns() {
      const hhSel = document.getElementById('hh-log-cat');
      hhSel.innerHTML = hhCategories.map(c => `<option value="${c.name}">${c.icon} ${c.name}</option>`).join('');

      const pSel = document.getElementById('p-log-cat');
      pSel.innerHTML = pCategories.map(c => `<option value="${c.name}">${c.icon} ${c.name}</option>`).join('');
    }

    function addExpense(type) {
      const prefix = type === 'hh' ? 'hh-log' : 'p-log';
      const date = document.getElementById(prefix + '-date').value || new Date().toISOString().slice(0, 10);
      const cat = document.getElementById(prefix + '-cat').value;
      const desc = document.getElementById(prefix + '-desc').value || 'Logged transaction';
      const amt = parseFloat(document.getElementById(prefix + '-amt').value) || 0;
      if (amt <= 0) return;

      if (type === 'hh') {
        hhExpenses.push({ id: Date.now(), date, cat, desc, amt });
        renderExpenseLogs('hh');
        renderHousehold();
      } else {
        pExpenses.push({ id: Date.now(), date, cat, desc, amt });
        renderExpenseLogs('p');
        renderPersonal();
      }
      document.getElementById(prefix + '-desc').value = '';
      document.getElementById(prefix + '-amt').value = '';
      saveData();
    }

    function deleteExpense(type, id) {
      if (type === 'hh') {
        hhExpenses = hhExpenses.filter(e => e.id !== id);
        renderExpenseLogs('hh');
        renderHousehold();
      } else {
        pExpenses = pExpenses.filter(e => e.id !== id);
        renderExpenseLogs('p');
        renderPersonal();
      }
      saveData();
    }

    function renderExpenseLogs(type) {
      const list = type === 'hh' ? hhExpenses : pExpenses;
      const tbody = document.getElementById(type === 'hh' ? 'hh-log-tbody' : 'p-log-tbody');

      if (list.length === 0) {
        tbody.innerHTML = `
          <tr>
            <td colspan="5" class="py-8 text-center text-slate-500">
              <div class="flex flex-col items-center gap-2">
                <span class="text-2xl">🧾</span>
                <span>No transactions logged yet. Add an expense above to see it here.</span>
              </div>
            </td>
          </tr>
        `;
      } else {
        tbody.innerHTML = list.map(item => `
          <tr>
            <td class="py-2.5 px-3 text-slate-400">${item.date}</td>
            <td class="py-2.5 px-3 font-medium text-white">
              <span class="mr-1.5">${getCategoryIcon(type, item.cat)}</span>${item.cat}
            </td>
            <td class="py-2.5 px-3 text-slate-300">${item.desc}</td>
            <td class="py-2.5 px-3 text-right font-semibold text-white">${fmt(item.amt)}</td>
            <td class="py-2.5 px-3 text-right">
              <button onclick="deleteExpense('${type}', ${item.id})" class="text-rose-400 hover:text-rose-300 text-xs font-semibold">Remove</button>
            </td>
          </tr>
        `).join('');
      }

      if (type === 'p') {
        const total = pExpenses.reduce((s, e) => s + e.amt, 0);
        document.getElementById('p-log-total').textContent = fmt(total);
      }
    }

    // Initialize App
    populateDropdowns();
    renderHousehold();
    renderPersonal();
    renderExpenseLogs('hh');
    renderExpenseLogs('p');
  </script>
</body>
</html>
```
