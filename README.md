<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Household Budget & Savings Tracker</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 text-gray-900 font-sans min-h-screen p-4 md:p-8">
    <div class="max-w-5xl mx-auto space-y-6">
        
        <!-- Header -->
        <div class="bg-indigo-900 text-white p-6 rounded-2xl shadow flex flex-col md:flex-row justify-between items-center gap-4">
            <div>
                <h1 class="text-2xl font-bold">Household & Personal Budget Tracker</h1>
                <p class="text-indigo-200 text-sm mt-1">Active Month: <span id="active-month" class="font-semibold text-white">2026-10</span></p>
            </div>
            <div class="flex items-center gap-2 bg-indigo-800 p-2 rounded-xl">
                <label class="text-xs uppercase font-bold text-indigo-200">Month:</label>
                <input type="month" id="month-input" value="2026-10" class="bg-indigo-950 text-white px-3 py-1 rounded border border-indigo-700 text-sm">
            </div>
        </div>

        <!-- Navigation Tabs -->
        <div class="flex gap-2 border-b border-gray-300 pb-2">
            <button onclick="switchTab('dashboard')" id="btn-dashboard" class="px-4 py-2 bg-indigo-600 text-white font-semibold rounded-lg text-sm shadow">Household Dashboard</button>
            <button onclick="switchTab('personal')" id="btn-personal" class="px-4 py-2 bg-white text-gray-700 font-semibold rounded-lg text-sm border">Personal Budget & Pay</button>
            <button onclick="switchTab('expenses')" id="btn-expenses" class="px-4 py-2 bg-white text-gray-700 font-semibold rounded-lg text-sm border">Expense Log</button>
        </div>

        <!-- TAB 1: HOUSEHOLD DASHBOARD -->
        <div id="tab-dashboard" class="space-y-6">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-4">
                <div class="bg-white p-5 rounded-xl shadow border">
                    <p class="text-xs uppercase font-bold text-gray-400">Total Fortnight Budget</p>
                    <h3 class="text-2xl font-extrabold text-indigo-600 mt-1" id="h-total-budget">$3,295.85</h3>
                </div>
                <div class="bg-white p-5 rounded-xl shadow border">
                    <p class="text-xs uppercase font-bold text-gray-400">Total Income Pool</p>
                    <h3 class="text-2xl font-extrabold text-emerald-600 mt-1" id="h-income-pool">$3,325.00</h3>
                </div>
                <div class="bg-white p-5 rounded-xl shadow border">
                    <p class="text-xs uppercase font-bold text-gray-400">Fortnightly Buffer</p>
                    <h3 class="text-2xl font-extrabold text-blue-600 mt-1" id="h-buffer">$29.15</h3>
                </div>
                <div class="bg-white p-5 rounded-xl shadow border">
                    <p class="text-xs uppercase font-bold text-gray-400">Monthly Surplus</p>
                    <h3 class="text-2xl font-extrabold text-purple-600 mt-1" id="h-monthly-surplus">$63.17</h3>
                </div>
            </div>

            <!-- Contributor Split Box -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div class="bg-white p-5 rounded-xl shadow border flex justify-between items-center">
                    <div>
                        <p class="text-xs uppercase font-bold text-gray-400">Liam (Baseline: $<span id="liam-base">1875</span>)</p>
                        <h4 class="text-xl font-bold text-indigo-900 mt-1" id="liam-dynamic">$1,858.56 <span class="text-xs font-normal text-gray-500">(<span id="liam-pct">56.4</span>%)</span></h4>
                    </div>
                    <button onclick="editBaseline('liam')" class="text-xs bg-gray-100 hover:bg-gray-200 px-3 py-1.5 rounded font-semibold border">Edit Baseline</button>
                </div>
                <div class="bg-white p-5 rounded-xl shadow border flex justify-between items-center">
                    <div>
                        <p class="text-xs uppercase font-bold text-gray-400">Amy (Baseline: $<span id="amy-base">1450</span>)</p>
                        <h4 class="text-xl font-bold text-indigo-900 mt-1" id="amy-dynamic">$1,437.29 <span class="text-xs font-normal text-gray-500">(<span id="amy-pct">43.6</span>%)</span></h4>
                    </div>
                    <button onclick="editBaseline('amy')" class="text-xs bg-gray-100 hover:bg-gray-200 px-3 py-1.5 rounded font-semibold border">Edit Baseline</button>
                </div>
            </div>

            <div class="bg-white p-6 rounded-xl shadow border overflow-x-auto">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="text-lg font-bold">Household Joint Budget Categories (Click any value to edit)</h3>
                    <button onclick="resetDashboardBudget()" class="text-xs bg-gray-200 hover:bg-gray-300 text-gray-700 px-3 py-1.5 rounded font-semibold">Reset Defaults</button>
                </div>
                <table class="w-full text-left border-collapse text-sm">
                    <thead>
                        <tr class="border-b text-xs text-gray-400 uppercase">
                            <th class="py-2 px-3">Category</th>
                            <th class="py-2 px-3">Monthly</th>
                            <th class="py-2 px-3">Fortnightly</th>
                            <th class="py-2 px-3">Weekly</th>
                            <th class="py-2 px-3">Remaining</th>
                        </tr>
                    </thead>
                    <tbody id="dashboard-tbody" class="divide-y"></tbody>
                </table>
            </div>
        </div>

        <!-- TAB 2: PERSONAL BUDGET -->
        <div id="tab-personal" class="space-y-6 hidden">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <div class="bg-white p-5 rounded-xl shadow border">
                    <p class="text-xs uppercase font-bold text-gray-400">Fortnightly Take-Home Pay (Editable)</p>
                    <h3 class="text-2xl font-extrabold text-indigo-600 mt-1" id="p-income-card">$3,400.00</h3>
                </div>
                <div class="bg-white p-5 rounded-xl shadow border">
                    <p class="text-xs uppercase font-bold text-gray-400">Total Fortnightly Outflows</p>
                    <h3 class="text-2xl font-extrabold text-rose-600 mt-1" id="p-outflow-card">$3,217.15</h3>
                </div>
                <div class="bg-white p-5 rounded-xl shadow border">
                    <p class="text-xs uppercase font-bold text-gray-400">Fortnightly Surplus to Save</p>
                    <h3 class="text-2xl font-extrabold text-emerald-600 mt-1" id="p-surplus-card">$182.85</h3>
                </div>
            </div>

            <div class="bg-white p-6 rounded-xl shadow border overflow-x-auto">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="text-lg font-bold">Personal Budget, Pay & Accounts (Click any value to edit)</h3>
                    <button onclick="resetPersonalBudget()" class="text-xs bg-gray-200 hover:bg-gray-300 text-gray-700 px-3 py-1.5 rounded font-semibold">Reset Defaults</button>
                </div>
                <table class="w-full text-left border-collapse text-sm">
                    <thead>
                        <tr class="border-b text-xs text-gray-400 uppercase">
                            <th class="py-2 px-3">Category / Account</th>
                            <th class="py-2 px-3">Monthly</th>
                            <th class="py-2 px-3">Fortnightly</th>
                            <th class="py-2 px-3">Weekly</th>
                            <th class="py-2 px-3">Remaining</th>
                        </tr>
                    </thead>
                    <tbody id="personal-tbody" class="divide-y"></tbody>
                </table>
            </div>
        </div>

        <!-- TAB 3: EXPENSES -->
        <div id="tab-expenses" class="space-y-6 hidden">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <div class="bg-white p-6 rounded-xl shadow border h-fit">
                    <h3 class="text-lg font-bold mb-4">Log Expense</h3>
                    <form onsubmit="addExpense(event)" class="space-y-4">
                        <div>
                            <label class="block text-xs font-bold uppercase text-gray-500 mb-1">Date</label>
                            <input type="date" id="exp-date" required class="w-full p-2 border rounded text-sm">
                        </div>
                        <div>
                            <label class="block text-xs font-bold uppercase text-gray-500 mb-1">Category</label>
                            <select id="exp-cat" class="w-full p-2 border rounded text-sm bg-white">
                                <optgroup label="🏠 Household Joint Budget" id="household-optgroup"></optgroup>
                                <optgroup label="👤 Personal Budget & Accounts" id="personal-optgroup"></optgroup>
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-bold uppercase text-gray-500 mb-1">Description</label>
                            <input type="text" id="exp-desc" placeholder="e.g. Weekly shop" required class="w-full p-2 border rounded text-sm">
                        </div>
                        <div>
                            <label class="block text-xs font-bold uppercase text-gray-500 mb-1">Amount ($)</label>
                            <input type="number" step="0.01" id="exp-amt" placeholder="0.00" required class="w-full p-2 border rounded text-sm">
                        </div>
                        <button type="submit" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-semibold py-2 rounded text-sm">Add Transaction</button>
                    </form>
                </div>
                <div class="bg-white p-6 rounded-xl shadow border md:col-span-2 overflow-x-auto">
                    <div class="flex justify-between items-center mb-4">
                        <h3 class="text-lg font-bold">Expense Log (<span id="log-month-label">2026-10</span>)</h3>
                        <span id="total-badge" class="bg-indigo-100 text-indigo-800 text-xs font-bold px-3 py-1 rounded-full">Total: $0.00</span>
                    </div>
                    <table class="w-full text-left border-collapse text-sm">
                        <thead>
                            <tr class="border-b text-xs text-gray-400 uppercase">
                                <th class="py-2 px-3">Date</th>
                                <th class="py-2 px-3">Category</th>
                                <th class="py-2 px-3">Description</th>
                                <th class="py-2 px-3">Amount</th>
                                <th class="py-2 px-3 text-right">Action</th>
                            </tr>
                        </thead>
                        <tbody id="expense-tbody" class="divide-y"></tbody>
                    </table>
                </div>
            </div>
        </div>

    </div>

    <script>
        const defaultDashboardData = [
            { cat: "Mortgage", m: 2450, f: 1130.77, w: 565.39, rem: 2450 },
            { cat: "Groceries", m: 1275, f: 588.46, w: 294.23, rem: 1275 },
            { cat: "Ollie Daycare", m: 1205, f: 556.15, w: 278.08, rem: 1205 },
            { cat: "Power", m: 450, f: 207.69, w: 103.85, rem: 450 },
            { cat: "Take Out", m: 350, f: 161.54, w: 80.77, rem: 350 },
            { cat: "Cleaner", m: 305, f: 140.77, w: 70.38, rem: 305 },
            { cat: "House Insurance", m: 245, f: 113.08, w: 56.54, rem: 245 },
            { cat: "Mum Repayment", m: 160, f: 73.85, w: 36.92, rem: 160 },
            { cat: "Lilly Food", m: 160, f: 73.85, w: 36.92, rem: 160 },
            { cat: "Petrol", m: 130, f: 60.00, w: 30.00, rem: 130 },
            { cat: "Internet", m: 113, f: 52.15, w: 26.08, rem: 113 },
            { cat: "Christmas Savings", m: 88, f: 40.62, w: 20.31, rem: 88 },
            { cat: "Contents Insurance", m: 76, f: 35.08, w: 17.54, rem: 76 },
            { cat: "Lilly Insurance", m: 72, f: 33.23, w: 16.62, rem: 72 },
            { cat: "Rubbish", m: 50, f: 23.08, w: 11.54, rem: 50 },
            { cat: "RockGas Annual Fee", m: 12, f: 5.54, w: 2.77, rem: 12 },
            { cat: "Emby", m: 10.25, f: 4.73, w: 2.37, rem: 10.25 }
        ];

        const defaultPersonalData = [
            { cat: "Fortnightly Take-Home Pay (Income)", m: 7366.67, f: 3400.00, w: 1700.00, rem: 3400.00, isIncome: true },
            { cat: "Spending Account", m: 1513, f: 698.31, w: 349.15, rem: 698.31 },
            { cat: "Bills Account", m: 1395, f: 643.85, w: 321.92, rem: 643.85 },
            { cat: "Joint Household Contribution", m: 4062.50, f: 1875.00, w: 937.50, rem: 1875.00 },
            { cat: "Petrol", m: 542, f: 250.15, w: 125.08, rem: 250.15 },
            { cat: "Smokes", m: 364, f: 168.00, w: 84.00, rem: 168.00 },
            { cat: "Parking", m: 130, f: 60.00, w: 30.00, rem: 60.00 },
            { cat: "Lunches", m: 260, f: 120.00, w: 60.00, rem: 120.00 },
            { cat: "Barber", m: 130, f: 60.00, w: 30.00, rem: 60.00 },
            { cat: "Alcohol", m: 87, f: 40.15, w: 20.08, rem: 40.15 },
            { cat: "Emby", m: 40, f: 18.46, w: 9.23, rem: 18.46 },
            { cat: "Loan Repayments", m: 780, f: 360.00, w: 180.00, rem: 360.00 },
            { cat: "Rates", m: 335, f: 154.62, w: 77.31, rem: 154.62 },
            { cat: "Mobile Phone", m: 240, f: 110.77, w: 55.38, rem: 110.77 }
        ];

        let currentMonth = "2026-10";
        let expenses = JSON.parse(localStorage.getItem('my_expenses') || '[]');
        let dashboardData = JSON.parse(localStorage.getItem('my_dashboard_budget') || JSON.stringify(defaultDashboardData));
        let personalData = JSON.parse(localStorage.getItem('my_personal_budget') || JSON.stringify(defaultPersonalData));
        let contributorBaselines = JSON.parse(localStorage.getItem('my_baselines') || JSON.stringify({ liam: 1875, amy: 1450 }));

        document.addEventListener('DOMContentLoaded', () => {
            document.getElementById('exp-date').value = new Date().toISOString().split('T')[0];
            
            const monthInput = document.getElementById('month-input');
            monthInput.value = currentMonth;
            monthInput.addEventListener('change', (e) => {
                currentMonth = e.target.value;
                document.getElementById('active-month').textContent = currentMonth;
                document.getElementById('log-month-label').textContent = currentMonth;
                renderExpenses();
            });

            renderTables();
        });

        function switchTab(tab) {
            ['dashboard', 'personal', 'expenses'].forEach(t => {
                document.getElementById(`tab-${t}`).classList.add('hidden');
                document.getElementById(`btn-${t}`).className = "px-4 py-2 bg-white text-gray-700 font-semibold rounded-lg text-sm border";
            });
            document.getElementById(`tab-${tab}`).classList.remove('hidden');
            document.getElementById(`btn-${tab}`).className = "px-4 py-2 bg-indigo-600 text-white font-semibold rounded-lg text-sm shadow";
        }

        function populateCategoryDropdowns() {
            const hGroup = document.getElementById('household-optgroup');
            const pGroup = document.getElementById('personal-optgroup');
            hGroup.innerHTML = '';
            pGroup.innerHTML = '';

            dashboardData.forEach(r => {
                hGroup.innerHTML += `<option value="${r.cat}">${r.cat}</option>`;
            });
            personalData.forEach(r => {
                if(!r.isIncome) {
                    pGroup.innerHTML += `<option value="${r.cat}">${r.cat}</option>`;
                }
            });
        }

        function renderTables() {
            populateCategoryDropdowns();

            // Render Dashboard Budget
            const dBody = document.getElementById('dashboard-tbody');
            dBody.innerHTML = '';
            let totalDashboardF = 0;

            dashboardData.forEach((r, idx) => {
                totalDashboardF += r.f;
                dBody.innerHTML += `
                    <tr class="hover:bg-gray-50">
                        <td class="py-2.5 px-3 font-medium">${r.cat}</td>
                        <td class="py-2.5 px-3 cursor-pointer hover:bg-yellow-50" onclick="editDashboardBudget(${idx}, 'm')" title="Click to edit">$${r.m.toFixed(2)}</td>
                        <td class="py-2.5 px-3 cursor-pointer hover:bg-yellow-50" onclick="editDashboardBudget(${idx}, 'f')" title="Click to edit">$${r.f.toFixed(2)}</td>
                        <td class="py-2.5 px-3 cursor-pointer hover:bg-yellow-50" onclick="editDashboardBudget(${idx}, 'w')" title="Click to edit">$${r.w.toFixed(2)}</td>
                        <td class="py-2.5 px-3 text-emerald-600 font-semibold">$${r.rem.toFixed(2)}</td>
                    </tr>`;
            });

            // Calculate Contributors dynamic split
            let totalPool = contributorBaselines.liam + contributorBaselines.amy;
            let liamPct = (contributorBaselines.liam / totalPool) * 100;
            let amyPct = (contributorBaselines.amy / totalPool) * 100;
            let liamReq = totalDashboardF * (liamPct / 100);
            let amyReq = totalDashboardF * (amyPct / 100);
            let bufferF = totalPool - totalDashboardF;
            let monthlySurplus = bufferF * 2.166;

            document.getElementById('h-total-budget').textContent = `$${totalDashboardF.toFixed(2)}`;
            document.getElementById('h-income-pool').textContent = `$${totalPool.toFixed(2)}`;
            document.getElementById('h-buffer').textContent = `$${bufferF.toFixed(2)}`;
            document.getElementById('h-monthly-surplus').textContent = `$${monthlySurplus.toFixed(2)}`;

            document.getElementById('liam-base').textContent = contributorBaselines.liam;
            document.getElementById('amy-base').textContent = contributorBaselines.amy;
            document.getElementById('liam_dynamic').innerHTML = `$${liamReq.toFixed(2)} <span class="text-xs font-normal text-gray-500">(${liamPct.toFixed(1)}%)</span>`;
            document.getElementById('amy_dynamic').innerHTML = `$${amyReq.toFixed(2)} <span class="text-xs font-normal text-gray-500">(${amyPct.toFixed(1)}%)</span>`;

            // Render Personal Budget
            const pBody = document.getElementById('personal-tbody');
            pBody.innerHTML = '';
            let totalIncomeF = 0;
            let totalOutflowF = 0;

            personalData.forEach((r, idx) => {
                if (r.isIncome) {
                    totalIncomeF = r.f;
                } else {
                    totalOutflowF += r.f;
                }
                const rowStyle = r.isIncome ? 'bg-indigo-50/60 font-bold text-indigo-900' : 'hover:bg-gray-50';
                pBody.innerHTML += `
                    <tr class="${rowStyle}">
                        <td class="py-2.5 px-3">${r.cat}</td>
                        <td class="py-2.5 px-3 cursor-pointer hover:bg-yellow-50" onclick="editPersonalBudget(${idx}, 'm')" title="Click to edit">$${r.m.toFixed(2)}</td>
                        <td class="py-2.5 px-3 cursor-pointer hover:bg-yellow-50" onclick="editPersonalBudget(${idx}, 'f')" title="Click to edit">$${r.f.toFixed(2)}</td>
                        <td class="py-2.5 px-3 cursor-pointer hover:bg-yellow-50" onclick="editPersonalBudget(${idx}, 'w')" title="Click to edit">$${r.w.toFixed(2)}</td>
                        <td class="py-2.5 px-3 text-emerald-600 font-semibold">$${r.rem.toFixed(2)}</td>
                    </tr>`;
            });

            let savingsSurplusF = totalIncomeF - totalOutflowF;
            document.getElementById('p-income-card').textContent = `$${totalIncomeF.toFixed(2)}`;
            document.getElementById('p-outflow-card').textContent = `$${totalOutflowF.toFixed(2)}`;
            document.getElementById('p-surplus-card').textContent = `$${savingsSurplusF.toFixed(2)}`;

            renderExpenses();
        }

        function editDashboardBudget(index, field) {
            let item = dashboardData[index];
            let currentVal = field === 'm' ? item.m : (field === 'f' ? item.f : item.w);
            let newVal = prompt(`Edit ${field.toUpperCase()} amount for "${item.cat}":`, currentVal);
            
            if (newVal !== null && !isNaN(newVal) && newVal.trim() !== "") {
                let val = parseFloat(newVal);
                if (field === 'm') {
                    item.m = val;
                    item.f = val / 2.166;
                    item.w = val / 4.333;
                } else if (field === 'f') {
                    item.f = val;
                    item.m = val * 2.166;
                    item.w = val / 2;
                } else {
                    item.w = val;
                    item.f = val * 2;
                    item.m = val * 4.333;
                }
                item.rem = item.f;
                localStorage.setItem('my_dashboard_budget', JSON.stringify(dashboardData));
                renderTables();
            }
        }

        function editPersonalBudget(index, field) {
            let item = personalData[index];
            let currentVal = field === 'm' ? item.m : (field === 'f' ? item.f : item.w);
            let newVal = prompt(`Edit ${field.toUpperCase()} amount for "${item.cat}":`, currentVal);
            
            if (newVal !== null && !isNaN(newVal) && newVal.trim() !== "") {
                let val = parseFloat(newVal);
                if (field === 'm') {
                    item.m = val;
                    item.f = val / 2.166;
                    item.w = val / 4.333;
                } else if (field === 'f') {
                    item.f = val;
                    item.m = val * 2.166;
                    item.w = val / 2;
                } else {
                    item.w = val;
                    item.f = val * 2;
                    item.m = val * 4.333;
                }
                item.rem = item.f;
                localStorage.setItem('my_personal_budget', JSON.stringify(personalData));
                renderTables();
            }
        }

        function editBaseline(person) {
            let current = contributorBaselines[person];
            let newVal = prompt(`Enter new baseline input for ${person}:`, current);
            if (newVal !== null && !isNaN(newVal) && newVal.trim() !== "") {
                contributorBaselines[person] = parseFloat(newVal);
                localStorage.setItem('my_baselines', JSON.stringify(contributorBaselines));
                renderTables();
            }
        }

        function resetDashboardBudget() {
            if (confirm("Reset household dashboard budget values to original defaults?")) {
                localStorage.removeItem('my_dashboard_budget');
                localStorage.removeItem('my_baselines');
                dashboardData = JSON.parse(JSON.stringify(defaultDashboardData));
                contributorBaselines = { liam: 1875, amy: 1450 };
                renderTables();
            }
        }

        function resetPersonalBudget() {
            if (confirm("Reset personal budget values to original defaults?")) {
                localStorage.removeItem('my_personal_budget');
                personalData = JSON.parse(JSON.stringify(defaultPersonalData));
                renderTables();
            }
        }

        function addExpense(e) {
            e.preventDefault();
            const date = document.getElementById('exp-date').value;
            const category = document.getElementById('exp-cat').value;
            const description = document.getElementById('exp-desc').value;
            const amount = parseFloat(document.getElementById('exp-amt').value);
            const month = date.substring(0, 7);

            expenses.push({ id: Date.now(), date, month, category, description, amount });
            localStorage.setItem('my_expenses', JSON.stringify(expenses));

            document.getElementById('exp-desc').value = '';
            document.getElementById('exp-amt').value = '';
            renderExpenses();
        }

        function deleteExp(id) {
            expenses = expenses.filter(x => x.id !== id);
            localStorage.setItem('my_expenses', JSON.stringify(expenses));
            renderExpenses();
        }

        function renderExpenses() {
            const tbody = document.getElementById('expense-tbody');
            tbody.innerHTML = '';
            const filtered = expenses.filter(x => x.month === currentMonth);
            let total = 0;

            filtered.forEach(x => {
                total += x.amount;
                tbody.innerHTML += `<tr class="hover:bg-gray-50"><td class="py-2 px-3 text-gray-500">${x.date}</td><td class="py-2 px-3 font-medium">${x.category}</td><td class="py-2 px-3">${x.description}</td><td class="py-2 px-3 text-rose-600 font-semibold">-$${x.amount.toFixed(2)}</td><td class="py-2 px-3 text-right"><button onclick="deleteExp(${x.id})" class="text-gray-400 hover:text-rose-600">✕</button></td></tr>`;
            });

            if(filtered.length === 0) {
                tbody.innerHTML = `<tr><td colspan="5" class="py-4 text-center text-gray-400 text-sm">No expenses logged for ${currentMonth}</td></tr>`;
            }

            document.getElementById('total-badge').textContent = `Total: $${total.toFixed(2)}`;
        }
    </script>
</body>
</html>
