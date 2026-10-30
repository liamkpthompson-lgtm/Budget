<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Household & Personal Budget Tracker</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      background-color: #0f172a;
      color: #f8fafc;
    }
    .tab-active {
      background-color: #2563eb;
      color: #ffffff;
      box-shadow: 0 4px 12px rgba(37, 99, 235, 0.35);
    }
    .tab-inactive {
      background-color: #1e293b;
      color: #94a3b8;
    }
    .tab-inactive:hover {
      background-color: #334155;
      color: #e2e8f0;
    }
    input[type="number"]::-webkit-inner-spin-button,
    input[type="number"]::-webkit-outer-spin-button {
      opacity: 1;
    }
  </style>
</head>
<body class="min-h-screen p-3 sm:p-6">

  <div class="max-w-7xl mx-auto space-y-6">
    <!-- Header & Controls -->
    <header class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-6 flex flex-col md:flex-row md:items-center md:justify-between gap-4 shadow-lg">
      <div>
        <h1 class="text-xl sm:text-2xl font-bold tracking-tight text-white">Budget & Dynamic Surplus Tracker</h1>
        <p class="text-xs sm:text-sm text-slate-400 mt-1">
          Self-contained Household & Personal Budget with dynamic splits, expense logging, and local persistence.
        </p>
      </div>
      <div class="flex flex-wrap items-center gap-2">
        <button onclick="rolloverMonth()" class="px-3.5 py-2 text-xs font-semibold rounded-xl bg-amber-600/20 text-amber-300 border border-amber-500/30 hover:bg-amber-600/30 transition">
          Monthly Rollover (Clear Logs)
        </button>
        <button onclick="resetAllDefaults()" class="px-3.5 py-2 text-xs font-semibold rounded-xl bg-rose-600/20 text-rose-300 border border-rose-500/30 hover:bg-rose-600/30 transition">
          Reset Defaults
        </button>
      </div>
    </header>

    <!-- Navigation Tabs -->
    <nav class="grid grid-cols-2 sm:grid-cols-4 gap-2">
      <button id="tab-btn-household" onclick="switchTab('household')" class="tab-active py-3 px-4 rounded-xl font-semibold text-xs sm:text-sm transition text-center">
        Household Dashboard
      </button>
      <button id="tab-btn-personal" onclick="switchTab('personal')" class="tab-inactive py-3 px-4 rounded-xl font-semibold text-xs sm:text-sm transition text-center">
        Personal Budget
      </button>
      <button id="tab-btn-hh-log" onclick="switchTab('hh-log')" class="tab-inactive py-3 px-4 rounded-xl font-semibold text-xs sm:text-sm transition text-center">
        Household Expense Log
      </button>
      <button id="tab-btn-p-log" onclick="switchTab('p-log')" class="tab-inactive py-3 px-4 rounded-xl font-semibold text-xs sm:text-sm transition text-center">
        Personal Expense Log
      </button>
    </nav>

    <!-- ==================== TAB 1: HOUSEHOLD DASHBOARD ==================== -->
    <section id="tab-household" class="space-y-6">
      <!-- Top Surplus Cards -->
      <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5">
          <div class="text-xs font-semibold uppercase tracking-wider text-slate-400">Monthly Budget Remaining</div>
          <div id="hh-kpi-monthly" class="text-2xl sm:text-3xl font-bold text-emerald-400 mt-1">$7,151.25</div>
          <div class="text-xs text-slate-500 mt-1">Total monthly unspent budget</div>
        </div>
        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5">
          <div class="text-xs font-semibold uppercase tracking-wider text-slate-400">Fortnightly Budget Required</div>
          <div id="hh-kpi-fortnightly" class="text-2xl sm:text-3xl font-bold text-blue-400 mt-1">$3,295.85</div>
          <div class="text-xs text-slate-500 mt-1">Equivalent per fortnight</div>
        </div>
        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5">
          <div class="text-xs font-semibold uppercase tracking-wider text-slate-400">Weekly Budget Required</div>
          <div id="hh-kpi-weekly" class="text-2xl sm:text-3xl font-bold text-indigo-400 mt-1">$1,647.92</div>
          <div class="text-xs text-slate-500 mt-1">Equivalent per week</div>
        </div>
      </div>

      <!-- Income Split & Reconciliation Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <!-- Income Contributions & Fortnightly Split -->
        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5 overflow-x-auto">
          <h2 class="text-base font-bold text-white mb-3">Income Contributions & Fortnightly Split</h2>
          <table class="w-full text-xs sm:text-sm text-left">
            <thead class="text-slate-400 border-b border-slate-800 uppercase text-[11px]">
              <tr>
                <th class="py-2">Contributor</th>
                <th class="py-2 text-right">Baseline Input</th>
                <th class="py-2 text-right">% Split</th>
                <th class="py-2 text-right">Dynamic Required</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-slate-800/70">
              <tr>
                <td class="py-2.5 font-semibold text-white">Liam</td>
                <td class="py-2.5 text-right">
                  <input id="liam-baseline" type="number" step="0.01" onchange="updateContributors()" class="w-24 bg-slate-800 border border-slate-700 rounded-lg px-2 py-1 text-right text-white focus:outline-none focus:border-blue-500" />
                </td>
                <td id="liam-split-pct" class="py-2.5 text-right text-slate-300">56.4%</td>
                <td id="liam-dynamic-req" class="py-2.5 text-right font-semibold text-blue-400">$1,858.56</td>
              </tr>
              <tr>
                <td class="py-2.5 font-semibold text-white">Amy</td>
                <td class="py-2.5 text-right">
                  <input id="amy-baseline" type="number" step="0.01" onchange="updateContributors()" class="w-24 bg-slate-800 border border-slate-700 rounded-lg px-2 py-1 text-right text-white focus:outline-none focus:border-blue-500" />
                </td>
                <td id="amy-split-pct" class="py-2.5 text-right text-slate-300">43.6%</td>
                <td id="amy-dynamic-req" class="py-2.5 text-right font-semibold text-blue-400">$1,437.29</td>
              </tr>
              <tr class="font-bold bg-slate-800/40">
                <td class="py-2.5 text-white">Total Fortnightly Income Pool</td>
                <td id="pool-baseline-total" class="py-2.5 text-right text-emerald-400">$3,325.00</td>
                <td class="py-2.5 text-right text-slate-300">100.0%</td>
                <td id="pool-dynamic-total" class="py-2.5 text-right text-blue-400">$3,295.85</td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- Budget Reconciliation & Buffer -->
        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5">
          <h2 class="text-base font-bold text-white mb-3">Budget Reconciliation & Buffer</h2>
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

      <!-- Household Category Table -->
      <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-6 overflow-x-auto">
        <div class="flex items-center justify-between mb-4">
          <h2 class="text-base sm:text-lg font-bold text-white">Household Budget Categories</h2>
          <span class="text-xs text-slate-400">Edit monthly amounts to dynamically recalculate splits</span>
        </div>
        <table class="w-full text-xs sm:text-sm text-left">
          <thead class="text-slate-400 border-b border-slate-800 uppercase text-[11px]">
            <tr>
              <th class="py-3 px-2">Category</th>
              <th class="py-3 px-2 text-right">Monthly Budget</th>
              <th class="py-3 px-2 text-right">Fortnightly Budget</th>
              <th class="py-3 px-2 text-right">Weekly Budget</th>
              <th class="py-3 px-2 text-right">Actual Spend</th>
              <th class="py-3 px-2 text-right">Surplus / Remaining</th>
            </tr>
          </thead>
          <tbody id="hh-category-tbody" class="divide-y divide-slate-800/70"></tbody>
          <tfoot class="border-t-2 border-slate-700 font-bold bg-slate-800/50 text-white">
            <tr>
              <td class="py-3 px-2">Total</td>
              <td id="hh-tot-mo" class="py-3 px-2 text-right">$7,151.25</td>
              <td id="hh-tot-fn" class="py-3 px-2 text-right">$3,295.85</td>
              <td id="hh-tot-wk" class="py-3 px-2 text-right">$1,647.92</td>
              <td id="hh-tot-act" class="py-3 px-2 text-right">$0.00</td>
              <td id="hh-tot-rem" class="py-3 px-2 text-right text-emerald-400">$7,151.25</td>
            </tr>
          </tfoot>
        </table>
      </div>
    </section>

    <!-- ==================== TAB 2: PERSONAL BUDGET ==================== -->
    <section id="tab-personal" class="hidden space-y-6">
      <!-- Top 5 Personal KPI Cards -->
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-4">
        <div class="bg-slate-900 border border-blue-500/40 rounded-2xl p-4">
          <div class="text-[11px] font-semibold uppercase tracking-wider text-blue-300">✏️ Fortnightly Pay (Input)</div>
          <div class="mt-2 flex items-center">
            <span class="text-xl font-bold text-blue-400 mr-1">$</span>
            <input id="p-pay-input" type="number" step="0.01" onchange="updatePersonalPay()" class="w-full bg-slate-800 border border-slate-700 rounded-xl px-2.5 py-1.5 text-xl font-bold text-white focus:outline-none focus:border-blue-400" />
          </div>
          <div class="text-xs text-slate-400 mt-1.5">Base / cycle take-home pay</div>
        </div>

        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4">
          <div class="text-[11px] font-semibold uppercase tracking-wider text-slate-400">Total Fortnightly Expenses</div>
          <div id="p-kpi-expenses" class="text-2xl font-bold text-white mt-2">$3,217.15</div>
          <div id="p-kpi-expenses-sub" class="text-xs text-slate-400 mt-1.5">Fixed ($1,875) + Discretionary</div>
        </div>

        <div class="bg-emerald-950/30 border border-emerald-500/40 rounded-2xl p-4">
          <div class="text-[11px] font-semibold uppercase tracking-wider text-emerald-300">Fortnightly Surplus To Save</div>
          <div id="p-kpi-fn-surplus" class="text-2xl font-bold text-emerald-400 mt-2">$182.85</div>
          <div class="text-xs text-emerald-300/70 mt-1.5">Target surplus to savings</div>
        </div>

        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4">
          <div class="text-[11px] font-semibold uppercase tracking-wider text-slate-400">Weekly Surplus Equivalent</div>
          <div id="p-kpi-wk-surplus" class="text-2xl font-bold text-indigo-400 mt-2">$91.42</div>
          <div id="p-kpi-wk-sub" class="text-xs text-slate-400 mt-1.5">Equiv. Pay: $1,700.00</div>
        </div>

        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4">
          <div class="text-[11px] font-semibold uppercase tracking-wider text-slate-400">Monthly Surplus Equivalent</div>
          <div id="p-kpi-mo-surplus" class="text-2xl font-bold text-blue-400 mt-2">$396.17</div>
          <div id="p-kpi-mo-sub" class="text-xs text-slate-400 mt-1.5">Equiv. Pay: $7,366.67</div>
        </div>
      </div>

      <!-- Personal Budget Category Table -->
      <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-6 overflow-x-auto">
        <div class="flex items-center justify-between mb-4">
          <h2 class="text-base sm:text-lg font-bold text-white">Personal Budget Breakdown</h2>
          <span class="text-xs text-slate-400">Edit Monthly Budget to dynamically adjust Fortnightly & Weekly targets</span>
        </div>
        <table class="w-full text-xs sm:text-sm text-left">
          <thead class="text-slate-400 border-b border-slate-800 uppercase text-[11px]">
            <tr>
              <th class="py-3 px-2">Category</th>
              <th class="py-3 px-2 text-right">Monthly Budget</th>
              <th class="py-3 px-2 text-right">Fortnightly Budget</th>
              <th class="py-3 px-2 text-right">Weekly Budget</th>
              <th class="py-3 px-2 text-right">Actual Spend (FN)</th>
              <th class="py-3 px-2 text-right">Surplus / Remaining (FN)</th>
            </tr>
          </thead>
          <tbody id="p-category-tbody" class="divide-y divide-slate-800/70"></tbody>
          <tfoot class="border-t-2 border-slate-700 font-bold bg-slate-800/50 text-white">
            <tr>
              <td class="py-3 px-2">Total</td>
              <td id="p-tot-mo" class="py-3 px-2 text-right">$6,970.50</td>
              <td id="p-tot-fn" class="py-3 px-2 text-right">$3,217.15</td>
              <td id="p-tot-wk" class="py-3 px-2 text-right">$1,608.58</td>
              <td id="p-tot-act" class="py-3 px-2 text-right">$0.00</td>
              <td id="p-tot-rem" class="py-3 px-2 text-right text-emerald-400">$3,217.15</td>
            </tr>
          </tfoot>
        </table>
      </div>

      <!-- Account Distribution Split & Reconciliation Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <!-- Account Distribution Split -->
        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5 overflow-x-auto">
          <h2 class="text-base font-bold text-white mb-3">Account Distribution Split (Discretionary & Bills)</h2>
          <table class="w-full text-xs sm:text-sm text-left">
            <thead class="text-slate-400 border-b border-slate-800 uppercase text-[11px]">
              <tr>
                <th class="py-2">Account</th>
                <th class="py-2 text-right">Monthly</th>
                <th class="py-2 text-right">Fortnightly</th>
                <th class="py-2 text-right">Weekly</th>
                <th class="py-2 text-right">Actual</th>
                <th class="py-2 text-right">Remaining</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-slate-800/70">
              <tr>
                <td class="py-2.5 font-semibold text-white">Spending Account</td>
                <td id="acc-spend-mo" class="py-2.5 text-right">$1,513.00</td>
                <td id="acc-spend-fn" class="py-2.5 text-right">$698.31</td>
                <td id="acc-spend-wk" class="py-2.5 text-right">$349.15</td>
                <td id="acc-spend-act" class="py-2.5 text-right">$0.00</td>
                <td id="acc-spend-rem" class="py-2.5 text-right text-emerald-400">$698.31</td>
              </tr>
              <tr>
                <td class="py-2.5 font-semibold text-white">Bills Account</td>
                <td id="acc-bills-mo" class="py-2.5 text-right">$1,395.00</td>
                <td id="acc-bills-fn" class="py-2.5 text-right">$643.85</td>
                <td id="acc-bills-wk" class="py-2.5 text-right">$321.92</td>
                <td id="acc-bills-act" class="py-2.5 text-right">$0.00</td>
                <td id="acc-bills-rem" class="py-2.5 text-right text-emerald-400">$643.85</td>
              </tr>
              <tr class="font-bold bg-slate-800/40 text-white">
                <td class="py-2.5">Total Personal (Excl. Joint)</td>
                <td id="acc-tot-mo" class="py-2.5 text-right">$2,908.00</td>
                <td id="acc-tot-fn" class="py-2.5 text-right">$1,342.15</td>
                <td id="acc-tot-wk" class="py-2.5 text-right">$671.08</td>
                <td id="acc-tot-act" class="py-2.5 text-right">$0.00</td>
                <td id="acc-tot-rem" class="py-2.5 text-right text-emerald-400">$1,342.15</td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- Annualized & Multi-Frequency Savings Overview -->
        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5 overflow-x-auto">
          <h2 class="text-base font-bold text-white mb-3">Annualized & Multi-Frequency Savings Overview</h2>
          <table class="w-full text-xs sm:text-sm text-left">
            <thead class="text-slate-400 border-b border-slate-800 uppercase text-[11px]">
              <tr>
                <th class="py-2">Frequency</th>
                <th class="py-2 text-right">Take-Home Pay</th>
                <th class="py-2 text-right">Budget Expenses</th>
                <th class="py-2 text-right">Target Surplus</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-slate-800/70">
              <tr>
                <td class="py-2.5 font-semibold text-white">Weekly</td>
                <td id="freq-wk-pay" class="py-2.5 text-right">$1,700.00</td>
                <td id="freq-wk-exp" class="py-2.5 text-right">$1,608.58</td>
                <td id="freq-wk-sur" class="py-2.5 text-right font-semibold text-emerald-400">$91.42</td>
              </tr>
              <tr>
                <td class="py-2.5 font-semibold text-white">Fortnightly</td>
                <td id="freq-fn-pay" class="py-2.5 text-right">$3,400.00</td>
                <td id="freq-fn-exp" class="py-2.5 text-right">$3,217.15</td>
                <td id="freq-fn-sur" class="py-2.5 text-right font-semibold text-emerald-400">$182.85</td>
              </tr>
              <tr>
                <td class="py-2.5 font-semibold text-white">Monthly</td>
                <td id="freq-mo-pay" class="py-2.5 text-right">$7,366.67</td>
                <td id="freq-mo-exp" class="py-2.5 text-right">$6,970.50</td>
                <td id="freq-mo-sur" class="py-2.5 text-right font-semibold text-emerald-400">$396.17</td>
              </tr>
              <tr class="font-bold bg-slate-800/40 text-white">
                <td class="py-2.5">Annual (26 Pays)</td>
                <td id="freq-yr-pay" class="py-2.5 text-right">$88,400.00</td>
                <td id="freq-yr-exp" class="py-2.5 text-right">$83,646.00</td>
                <td id="freq-yr-sur" class="py-2.5 text-right text-emerald-400">$4,754.00</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>

      <!-- Fortnightly Pay Reconciliation & Surplus Buffer -->
      <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5 overflow-x-auto">
        <h2 class="text-base font-bold text-white mb-3">Fortnightly Pay Reconciliation & Surplus Buffer</h2>
        <table class="w-full text-xs sm:text-sm text-left">
          <thead class="text-slate-400 border-b border-slate-800 uppercase text-[11px]">
            <tr>
              <th class="py-2">Component</th>
              <th class="py-2 text-right">Budgeted</th>
              <th class="py-2 text-right">Actual to Date</th>
              <th class="py-2 text-right">Variance / Buffer</th>
            </tr>
          </thead>
          <tbody class="divide-y divide-slate-800/70">
            <tr>
              <td class="py-2.5 font-semibold text-white">Fortnightly Take-Home Pay</td>
              <td id="p-rec-pay-bud" class="py-2.5 text-right">$3,400.00</td>
              <td id="p-rec-pay-act" class="py-2.5 text-right">$3,400.00</td>
              <td class="py-2.5 text-right">$0.00</td>
            </tr>
            <tr>
              <td class="py-2.5 text-slate-300">Less: Fixed Household Transfer</td>
              <td id="p-rec-hh-bud" class="py-2.5 text-right">$1,875.00</td>
              <td id="p-rec-hh-act" class="py-2.5 text-right">$0.00</td>
              <td id="p-rec-hh-var" class="py-2.5 text-right">$1,875.00</td>
            </tr>
            <tr>
              <td class="py-2.5 text-slate-300">Less: Personal Discretionary Spending</td>
              <td id="p-rec-disc-bud" class="py-2.5 text-right">$1,342.15</td>
              <td id="p-rec-disc-act" class="py-2.5 text-right">$0.00</td>
              <td id="p-rec-disc-var" class="py-2.5 text-right">$1,342.15</td>
            </tr>
            <tr class="font-semibold">
              <td class="py-2.5 text-white">Total Fortnightly Outflows</td>
              <td id="p-rec-out-bud" class="py-2.5 text-right">$3,217.15</td>
              <td id="p-rec-out-act" class="py-2.5 text-right">$0.00</td>
              <td id="p-rec-out-var" class="py-2.5 text-right">$3,217.15</td>
            </tr>
            <tr class="font-bold bg-emerald-950/30 text-emerald-400">
              <td class="py-2.5">Net Surplus Available to Transfer to Savings</td>
              <td id="p-rec-net-bud" class="py-2.5 text-right">$182.85</td>
              <td id="p-rec-net-act" class="py-2.5 text-right">$3,400.00</td>
              <td id="p-rec-net-var" class="py-2.5 text-right">$3,217.15</td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <!-- ==================== TAB 3: HOUSEHOLD EXPENSE LOG ==================== -->
    <section id="tab-hh-log" class="hidden space-y-6">
      <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-6">
        <h2 class="text-base sm:text-lg font-bold text-white mb-1">Household Quick Expense Log</h2>
        <p class="text-xs text-slate-400 mb-4">Log purchases below to automatically update Household Dashboard actual spend and remaining surplus.</p>
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
            <thead class="text-slate-400 border-b border-slate-800 uppercase text-[11px]">
              <tr>
                <th class="py-2.5">Date</th>
                <th class="py-2.5">Category</th>
                <th class="py-2.5">Description</th>
                <th class="py-2.5 text-right">Amount</th>
                <th class="py-2.5 text-right">Action</th>
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
        <h2 class="text-base sm:text-lg font-bold text-white mb-1">Personal Expense Log</h2>
        <p class="text-xs text-slate-400 mb-4">Select a category for each personal transaction to automatically sync with your Personal Budget actual spend.</p>
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
            <thead class="text-slate-400 border-b border-slate-800 uppercase text-[11px]">
              <tr>
                <th class="py-2.5">Date</th>
                <th class="py-2.5">Category</th>
                <th class="py-2.5">Description</th>
                <th class="py-2.5 text-right">Amount</th>
                <th class="py-2.5 text-right">Action</th>
              </tr>
            </thead>
            <tbody id="p-log-tbody" class="divide-y divide-slate-800/70"></tbody>
            <tfoot class="border-t-2 border-slate-700 font-bold text-white">
              <tr>
                <td colspan="3" class="py-3">Total Personal Logged Spend</td>
                <td id="p-log-total" class="py-3 text-right text-emerald-400">$0.00</td>
                <td></td>
              </tr>
            </tfoot>
          </table>
        </div>
      </div>
    </section>
  </div>

  <script>
    const STORAGE_KEY = 'liam_unified_budget_tracker_v1';

    const DEFAULT_STATE = {
      liamBaseline: 1875.00,
      amyBaseline: 1450.00,
      personalFortnightlyPay: 3400.00,
      householdCategories: [
        { name: 'Mortgage', monthly: 2450.00 },
        { name: 'Groceries', monthly: 1275.00 },
        { name: 'Ollie Daycare', monthly: 1205.00 },
        { name: 'Power', monthly: 450.00 },
        { name: 'Take Out', monthly: 350.00 },
        { name: 'Cleaner', monthly: 305.00 },
        { name: 'House Insurance', monthly: 245.00 },
        { name: 'Mum Repayment', monthly: 160.00 },
        { name: 'Lilly Food', monthly: 160.00 },
        { name: 'Petrol', monthly: 130.00 },
        { name: 'Internet', monthly: 113.00 },
        { name: 'Christmas Savings', monthly: 88.00 },
        { name: 'Contents Insurance', monthly: 76.00 },
        { name: 'Lilly Insurance', monthly: 72.00 },
        { name: 'Rubbish', monthly: 50.00 },
        { name: 'RockGas Annual Fee', monthly: 12.00 },
        { name: 'Emby', monthly: 10.25 }
      ],
      personalCategories: [
        { name: 'Joint Household Contribution', monthly: 4062.50, account: 'Joint' },
        { name: 'Petrol', monthly: 542.00, account: 'Spending' },
        { name: 'Smokes', monthly: 364.00, account: 'Spending' },
        { name: 'Parking', monthly: 130.00, account: 'Spending' },
        { name: 'Lunches', monthly: 260.00, account: 'Spending' },
        { name: 'Barber', monthly: 130.00, account: 'Spending' },
        { name: 'Alcohol', monthly: 87.00, account: 'Spending' },
        { name: 'Emby', monthly: 40.00, account: 'Bills' },
        { name: 'Loan Repayments', monthly: 780.00, account: 'Bills' },
        { name: 'Rates', monthly: 335.00, account: 'Bills' },
        { name: 'Mobile Phone', monthly: 240.00, account: 'Bills' }
      ],
      hhExpenses: [],
      pExpenses: []
    };

    let state = loadState();

    function loadState() {
      const saved = localStorage.getItem(STORAGE_KEY);
      if (saved) {
        try {
          return JSON.parse(saved);
        } catch (e) {
          console.error('Error loading state:', e);
        }
      }
      return JSON.parse(JSON.stringify(DEFAULT_STATE));
    }

    function saveState() {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
    }

    function fmt(num) {
      return '$' + Number(num || 0).toLocaleString('en-NZ', { minimumFractionDigits: 2, maximumFractionDigits: 2 });
    }

    function switchTab(tab) {
      const tabs = ['household', 'personal', 'hh-log', 'p-log'];
      tabs.forEach(t => {
        document.getElementById('tab-' + t).classList.toggle('hidden', t !== tab);
        const btn = document.getElementById('tab-btn-' + t);
        if (t === tab) {
          btn.className = 'tab-active py-3 px-4 rounded-xl font-semibold text-xs sm:text-sm transition text-center';
        } else {
          btn.className = 'tab-inactive py-3 px-4 rounded-xl font-semibold text-xs sm:text-sm transition text-center';
        }
      });
    }

    function updateContributors() {
      state.liamBaseline = parseFloat(document.getElementById('liam-baseline').value) || 0;
      state.amyBaseline = parseFloat(document.getElementById('amy-baseline').value) || 0;
      saveState();
      renderAll();
    }

    function updatePersonalPay() {
      state.personalFortnightlyPay = parseFloat(document.getElementById('p-pay-input').value) || 0;
      saveState();
      renderAll();
    }

    function updateHhMonthly(idx, val) {
      state.householdCategories[idx].monthly = parseFloat(val) || 0;
      saveState();
      renderAll();
    }

    function updatePersonalMonthly(idx, val) {
      state.personalCategories[idx].monthly = parseFloat(val) || 0;
      saveState();
      renderAll();
    }

    function addExpense(type) {
      const prefix = type === 'hh' ? 'hh-log' : 'p-log';
      const date = document.getElementById(prefix + '-date').value || new Date().toISOString().slice(0, 10);
      const category = document.getElementById(prefix + '-cat').value;
      const desc = document.getElementById(prefix + '-desc').value.trim() || 'Expense';
      const amount = parseFloat(document.getElementById(prefix + '-amt').value);

      if (!amount || amount <= 0) return;

      const entry = { id: Date.now(), date, category, desc, amount };
      if (type === 'hh') {
        state.hhExpenses.push(entry);
      } else {
        state.pExpenses.push(entry);
      }

      document.getElementById(prefix + '-desc').value = '';
      document.getElementById(prefix + '-amt').value = '';
      saveState();
      renderAll();
    }

    function deleteExpense(type, id) {
      if (type === 'hh') {
        state.hhExpenses = state.hhExpenses.filter(e => e.id !== id);
      } else {
        state.pExpenses = state.pExpenses.filter(e => e.id !== id);
      }
      saveState();
      renderAll();
    }

    function rolloverMonth() {
      if (confirm('Clear all logged expenses for a new cycle while keeping your custom budget targets?')) {
        state.hhExpenses = [];
        state.pExpenses = [];
        saveState();
        renderAll();
      }
    }

    function resetAllDefaults() {
      if (confirm('Reset all household and personal budget figures and logs back to original defaults?')) {
        state = JSON.parse(JSON.stringify(DEFAULT_STATE));
        saveState();
        renderAll();
      }
    }

    function renderAll() {
      // 1. Render Household Dashboard
      document.getElementById('liam-baseline').value = state.liamBaseline.toFixed(2);
      document.getElementById('amy-baseline').value = state.amyBaseline.toFixed(2);

      const hhTbody = document.getElementById('hh-category-tbody');
      hhTbody.innerHTML = '';

      let hhTotMo = 0, hhTotFn = 0, hhTotWk = 0, hhTotAct = 0, hhTotRem = 0;

      state.householdCategories.forEach((cat, idx) => {
        const mo = cat.monthly;
        const fn = (mo * 12) / 26;
        const wk = (mo * 12) / 52;
        const act = state.hhExpenses
          .filter(e => e.category === cat.name)
          .reduce((sum, e) => sum + e.amount, 0);
        const rem = mo - act;

        hhTotMo += mo;
        hhTotFn += fn;
        hhTotWk += wk;
        hhTotAct += act;
        hhTotRem += rem;

        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td class="py-2.5 px-2 font-medium text-white">${cat.name}</td>
          <td class="py-2.5 px-2 text-right">
            <input type="number" step="0.01" value="${mo.toFixed(2)}" onchange="updateHhMonthly(${idx}, this.value)"
              class="w-24 bg-slate-800 border border-slate-700 rounded-lg px-2 py-1 text-right text-white focus:outline-none focus:border-blue-500" />
          </td>
          <td class="py-2.5 px-2 text-right text-slate-300">${fmt(fn)}</td>
          <td class="py-2.5 px-2 text-right text-slate-300">${fmt(wk)}</td>
          <td class="py-2.5 px-2 text-right text-amber-300">${fmt(act)}</td>
          <td class="py-2.5 px-2 text-right font-semibold ${rem >= 0 ? 'text-emerald-400' : 'text-rose-400'}">${fmt(rem)}</td>
        `;
        hhTbody.appendChild(tr);
      });

      document.getElementById('hh-tot-mo').textContent = fmt(hhTotMo);
      document.getElementById('hh-tot-fn').textContent = fmt(hhTotFn);
      document.getElementById('hh-tot-wk').textContent = fmt(hhTotWk);
      document.getElementById('hh-tot-act').textContent = fmt(hhTotAct);
      document.getElementById('hh-tot-rem').textContent = fmt(hhTotRem);

      document.getElementById('hh-kpi-monthly').textContent = fmt(hhTotRem);
      document.getElementById('hh-kpi-fortnightly').textContent = fmt(hhTotFn);
      document.getElementById('hh-kpi-weekly').textContent = fmt(hhTotWk);

      const poolTotal = state.liamBaseline + state.amyBaseline;
      const liamPct = poolTotal > 0 ? (state.liamBaseline / poolTotal) : 0;
      const amyPct = poolTotal > 0 ? (state.amyBaseline / poolTotal) : 0;

      document.getElementById('liam-split-pct').textContent = (liamPct * 100).toFixed(1) + '%';
      document.getElementById('amy-split-pct').textContent = (amyPct * 100).toFixed(1) + '%';
      document.getElementById('liam-dynamic-req').textContent = fmt(hhTotFn * liamPct);
      document.getElementById('amy-dynamic-req').textContent = fmt(hhTotFn * amyPct);
      document.getElementById('pool-baseline-total').textContent = fmt(poolTotal);
      document.getElementById('pool-dynamic-total').textContent = fmt(hhTotFn);

      const fnBuffer = poolTotal - hhTotFn;
      const moBuffer = (fnBuffer * 26) / 12;
      document.getElementById('rec-pool').textContent = fmt(poolTotal);
      document.getElementById('rec-req').textContent = fmt(hhTotFn);
      document.getElementById('rec-fn-buffer').textContent = fmt(fnBuffer);
      document.getElementById('rec-mo-buffer').textContent = fmt(moBuffer);

      // 2. Render Personal Budget
      document.getElementById('p-pay-input').value = state.personalFortnightlyPay.toFixed(2);
      const pTbody = document.getElementById('p-category-tbody');
      pTbody.innerHTML = '';

      let pTotMo = 0, pTotFn = 0, pTotWk = 0, pTotAct = 0, pTotRem = 0;
      let spendMo = 0, spendFn = 0, spendWk = 0, spendAct = 0;
      let billsMo = 0, billsFn = 0, billsWk = 0, billsAct = 0;
      let jointFnBud = 0, jointFnAct = 0;

      state.personalCategories.forEach((cat, idx) => {
        const mo = cat.monthly;
        const fn = (mo * 12) / 26;
        const wk = (mo * 12) / 52;
        const act = state.pExpenses
          .filter(e => e.category === cat.name)
          .reduce((sum, e) => sum + e.amount, 0);
        const rem = fn - act;

        pTotMo += mo;
        pTotFn += fn;
        pTotWk += wk;
        pTotAct += act;
        pTotRem += rem;

        if (cat.account === 'Spending') {
          spendMo += mo; spendFn += fn; spendWk += wk; spendAct += act;
        } else if (cat.account === 'Bills') {
          billsMo += mo; billsFn += fn; billsWk += wk; billsAct += act;
        } else if (cat.account === 'Joint') {
          jointFnBud += fn; jointFnAct += act;
        }

        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td class="py-2.5 px-2 font-medium text-white">${cat.name}</td>
          <td class="py-2.5 px-2 text-right">
            <input type="number" step="0.01" value="${mo.toFixed(2)}" onchange="updatePersonalMonthly(${idx}, this.value)"
              class="w-24 bg-slate-800 border border-slate-700 rounded-lg px-2 py-1 text-right text-white focus:outline-none focus:border-blue-500" />
          </td>
          <td class="py-2.5 px-2 text-right text-slate-300">${fmt(fn)}</td>
          <td class="py-2.5 px-2 text-right text-slate-300">${fmt(wk)}</td>
          <td class="py-2.5 px-2 text-right text-amber-300">${fmt(act)}</td>
          <td class="py-2.5 px-2 text-right font-semibold ${rem >= 0 ? 'text-emerald-400' : 'text-rose-400'}">${fmt(rem)}</td>
        `;
        pTbody.appendChild(tr);
      });

      document.getElementById('p-tot-mo').textContent = fmt(pTotMo);
      document.getElementById('p-tot-fn').textContent = fmt(pTotFn);
      document.getElementById('p-tot-wk').textContent = fmt(pTotWk);
      document.getElementById('p-tot-act').textContent = fmt(pTotAct);
      document.getElementById('p-tot-rem').textContent = fmt(pTotRem);

      const fnPay = state.personalFortnightlyPay;
      const fnSurplus = fnPay - pTotFn;
      const wkPay = fnPay / 2;
      const wkSurplus = fnSurplus / 2;
      const moPay = (fnPay * 26) / 12;
      const moSurplus = moPay - pTotMo;

      document.getElementById('p-kpi-expenses').textContent = fmt(pTotFn);
      document.getElementById('p-kpi-expenses-sub').textContent = `Fixed (${fmt(jointFnBud)}) + Discretionary`;
      document.getElementById('p-kpi-fn-surplus').textContent = fmt(fnSurplus);
      document.getElementById('p-kpi-wk-surplus').textContent = fmt(wkSurplus);
      document.getElementById('p-kpi-wk-sub').textContent = `Equiv. Pay: ${fmt(wkPay)}`;
      document.getElementById('p-kpi-mo-surplus').textContent = fmt(moSurplus);
      document.getElementById('p-kpi-mo-sub').textContent = `Equiv. Pay: ${fmt(moPay)}`;

      // Account Distribution Table
      const spendRem = spendFn - spendAct;
      const billsRem = billsFn - billsAct;
      document.getElementById('acc-spend-mo').textContent = fmt(spendMo);
      document.getElementById('acc-spend-fn').textContent = fmt(spendFn);
      document.getElementById('acc-spend-wk').textContent = fmt(spendWk);
      document.getElementById('acc-spend-act').textContent = fmt(spendAct);
      document.getElementById('acc-spend-rem').textContent = fmt(spendRem);

      document.getElementById('acc-bills-mo').textContent = fmt(billsMo);
      document.getElementById('acc-bills-fn').textContent = fmt(billsFn);
      document.getElementById('acc-bills-wk').textContent = fmt(billsWk);
      document.getElementById('acc-bills-act').textContent = fmt(billsAct);
      document.getElementById('acc-bills-rem').textContent = fmt(billsRem);

      document.getElementById('acc-tot-mo').textContent = fmt(spendMo + billsMo);
      document.getElementById('acc-tot-fn').textContent = fmt(spendFn + billsFn);
      document.getElementById('acc-tot-wk').textContent = fmt(spendWk + billsWk);
      document.getElementById('acc-tot-act').textContent = fmt(spendAct + billsAct);
      document.getElementById('acc-tot-rem').textContent = fmt(spendRem + billsRem);

      // Multi-Frequency Overview
      document.getElementById('freq-wk-pay').textContent = fmt(wkPay);
      document.getElementById('freq-wk-exp').textContent = fmt(pTotWk);
      document.getElementById('freq-wk-sur').textContent = fmt(wkSurplus);

      document.getElementById('freq-fn-pay').textContent = fmt(fnPay);
      document.getElementById('freq-fn-exp').textContent = fmt(pTotFn);
      document.getElementById('freq-fn-sur').textContent = fmt(fnSurplus);

      document.getElementById('freq-mo-pay').textContent = fmt(moPay);
      document.getElementById('freq-mo-exp').textContent = fmt(pTotMo);
      document.getElementById('freq-mo-sur').textContent = fmt(moSurplus);

      document.getElementById('freq-yr-pay').textContent = fmt(fnPay * 26);
      document.getElementById('freq-yr-exp').textContent = fmt(pTotFn * 26);
      document.getElementById('freq-yr-sur').textContent = fmt(fnSurplus * 26);

      // Personal Reconciliation Table
      const discFnBud = spendFn + billsFn;
      const discFnAct = spendAct + billsAct;
      document.getElementById('p-rec-pay-bud').textContent = fmt(fnPay);
      document.getElementById('p-rec-pay-act').textContent = fmt(fnPay);
      document.getElementById('p-rec-hh-bud').textContent = fmt(jointFnBud);
      document.getElementById('p-rec-hh-act').textContent = fmt(jointFnAct);
      document.getElementById('p-rec-hh-var').textContent = fmt(jointFnBud - jointFnAct);

      document.getElementById('p-rec-disc-bud').textContent = fmt(discFnBud);
      document.getElementById('p-rec-disc-act').textContent = fmt(discFnAct);
      document.getElementById('p-rec-disc-var').textContent = fmt(discFnBud - discFnAct);

      document.getElementById('p-rec-out-bud').textContent = fmt(pTotFn);
      document.getElementById('p-rec-out-act').textContent = fmt(pTotAct);
      document.getElementById('p-rec-out-var').textContent = fmt(pTotFn - pTotAct);

      document.getElementById('p-rec-net-bud').textContent = fmt(fnSurplus);
      document.getElementById('p-rec-net-act').textContent = fmt(fnPay - pTotAct);
      document.getElementById('p-rec-net-var').textContent = fmt(pTotFn - pTotAct);

      // 3. Populate Dropdowns & Expense Logs
      const hhSelect = document.getElementById('hh-log-cat');
      hhSelect.innerHTML = state.householdCategories.map(c => `<option value="${c.name}">${c.name}</option>`).join('');

      const pSelect = document.getElementById('p-log-cat');
      pSelect.innerHTML = state.personalCategories.map(c => `<option value="${c.name}">${c.name}</option>`).join('');

      const hhLogTbody = document.getElementById('hh-log-tbody');
      hhLogTbody.innerHTML = state.hhExpenses.map(e => `
        <tr>
          <td class="py-2.5 text-slate-300">${e.date}</td>
          <td class="py-2.5 font-medium text-white">${e.category}</td>
          <td class="py-2.5 text-slate-300">${e.desc}</td>
          <td class="py-2.5 text-right font-semibold text-amber-300">${fmt(e.amount)}</td>
          <td class="py-2.5 text-right">
            <button onclick="deleteExpense('hh', ${e.id})" class="text-rose-400 hover:text-rose-300 text-xs font-semibold">Delete</button>
          </td>
        </tr>
      `).join('');

      const pLogTbody = document.getElementById('p-log-tbody');
      pLogTbody.innerHTML = state.pExpenses.map(e => `
        <tr>
          <td class="py-2.5 text-slate-300">${e.date}</td>
          <td class="py-2.5 font-medium text-white">${e.category}</td>
          <td class="py-2.5 text-slate-300">${e.desc}</td>
          <td class="py-2.5 text-right font-semibold text-amber-300">${fmt(e.amount)}</td>
          <td class="py-2.5 text-right">
            <button onclick="deleteExpense('p', ${e.id})" class="text-rose-400 hover:text-rose-300 text-xs font-semibold">Delete</button>
          </td>
        </tr>
      `).join('');

      document.getElementById('p-log-total').textContent = fmt(pTotAct);
    }

    // Initialize date inputs and render
    document.getElementById('hh-log-date').value = new Date().toISOString().slice(0, 10);
    document.getElementById('p-log-date').value = new Date().toISOString().slice(0, 10);
    renderAll();
  </script>
</body>
</html>
