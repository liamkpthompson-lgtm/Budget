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
            <button onclick="switchTab('personal')" id="btn-personal" class="px-4 py-2 bg-white text-gray-700 font-semibold rounded-lg text-sm border">Personal Budget</button>
            <button onclick="switchTab('expenses')" id="btn-expenses" class="px-4 py-2 bg-white text-gray-700 font-semibold rounded-lg text-sm border">Expense Log</button>
            <button onclick="switchTab('github')" id="btn-github" class="px-4 py-2 bg-white text-gray-700 font-semibold rounded-lg text-sm border">Hosting Guide</button>
        </div>

        <!-- TAB 1: DASHBOARD -->
        <div id="tab-dashboard" class="space-y-6">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <div class="bg-white p-5 rounded-xl shadow border">
                    <p class="text-xs uppercase font-bold text-gray-400">Fortnightly Surplus</p>
                    <h3 class="text-2xl font-extrabold text-emerald-600 mt-1">$3,295.85</h3>
                </div>
                <div class="bg-white p-5 rounded-xl shadow border">
                    <p class="text-xs uppercase font-bold text-gray-400">Total Fortnight Pool</p>
                    <h3 class="text-2xl font-extrabold text-indigo-600 mt-1">$3,325.00</h3>
                </div>
                <div class="bg-white p-5 rounded-xl shadow border">
                    <p class="text-xs uppercase font-bold text-gray-400">Buffer to Savings</p>
                    <h3 class="text-2xl font-extrabold text-blue-600 mt-1">$29.15</h3>
                </div>
            </div>

            <div class="bg-white p-6 rounded-xl shadow border overflow-x-auto">
                <h3 class="text-lg font-bold mb-4">Household Joint Budget Categories</h3>
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
            <div class="bg-white p-6 rounded-xl shadow border overflow-x-auto">
                <h3 class="text-lg font-bold mb-4">Personal Budget & Accounts</h3>
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
                            <select id="exp-cat" class="w-full p-2 border rounded text-sm">
                                <option value="Groceries">Groceries</option>
                                <option value="Petrol">Petrol</option>
                                <option value="Coffee & Lunches">Coffee & Lunches</option>
                                <option value="Take Out">Take Out</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-bold uppercase text-gray-500 mb-1">Description</label>
                            <input type="text" id="exp-desc" placeholder="Description" required class="w-full p-2 border rounded text-sm">
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

        <!-- TAB 4: GITHUB GUIDE -->
        <div id="tab-github" class="space-y-6 hidden">
            <div class="bg-white p-6 rounded-xl shadow border space-y-4">
                <h3 class="text-lg font-bold">GitHub Pages Hosting Checklist</h3>
                <ol class="list-decimal list-inside space-y-2 text-sm text-gray-700">
                    <li>Create a public repository on GitHub.</li>
                    <li>Upload this exact file named <strong>index.html</strong> to the root folder.</li>
                    <li>Go to repository <strong>Settings > Pages</strong>, set branch to <strong>main</strong> / root, and save.</li>
                    <li>Wait 1 minute and your live app URL will be ready!</li>
                </ol>
            </div>
        </div>

    </div>

    <script>
        const dashboardData = [
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
            { cat: "Rubbish", m: 50, f: 23.08, w: 11.54, rem: 50 }
        ];

        const personalData = [
            { cat: "Spending Account", m: 1513, f: 698.31, w: 349.15, rem: 698.31 },
            { cat: "Bills Account", m: 1395, f: 643.85, w: 321.92, rem: 643.85 },
            { cat: "Joint Household Contribution", m: 4062.50, f: 1875.00, w: 937.50, rem: 1875.00 },
            { cat: "Petrol", m: 542, f: 250.15, w: 125.08, rem: 250.15 },
            { cat: "Smokes", m: 364, f: 168.00, w: 84.00, rem: 168.00 },
            { cat: "Parking", m: 130, f: 60.00, w: 30.00, rem: 60.00 },
            { cat: "Lunches", m: 260, f: 120.00, w: 60.00, rem: 120.00 },
            { cat: "Barber", m: 130, f: 60.00, w: 30.00, rem: 60.00 },
            { cat: "Loan Repayments", m: 780, f: 360.00, w: 180.00, rem: 360.00 },
            { cat: "Rates", m: 335, f: 154.62, w: 77.31, rem: 154.62 }
        ];

        let currentMonth = "2026-10";
        let expenses = JSON.parse(localStorage.getItem('my_expenses') || '[]');

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
            ['dashboard', 'personal', 'expenses', 'github'].forEach(t => {
                document.getElementById(`tab-${t}`).classList.add('hidden');
                document.getElementById(`btn-${t}`).className = "px-4 py-2 bg-white text-gray-700 font-semibold rounded-lg text-sm border";
            });
            document.getElementById(`tab-${tab}`).classList.remove('hidden');
            document.getElementById(`btn-${tab}`).className = "px-4 py-2 bg-indigo-600 text-white font-semibold rounded-lg text-sm shadow";
        }

        function renderTables() {
            const dBody = document.getElementById('dashboard-tbody');
            dBody.innerHTML = '';
            dashboardData.forEach(r => {
                dBody.innerHTML += `<tr class="hover:bg-gray-50"><td class="py-2 px-3 font-medium">${r.cat}</td><td class="py-2 px-3">$${r.m.toFixed(2)}</td><td class="py-2 px-3">$${r.f.toFixed(2)}</td><td class="py-2 px-3">$${r.w.toFixed(2)}</td><td class="py-2 px-3 text-emerald-600 font-semibold">$${r.rem.toFixed(2)}</td></tr>`;
            });

            const pBody = document.getElementById('personal-tbody');
            pBody.innerHTML = '';
            personalData.forEach(r => {
                pBody.innerHTML += `<tr class="hover:bg-gray-50"><td class="py-2 px-3 font-medium">${r.cat}</td><td class="py-2 px-3">$${r.m.toFixed(2)}</td><td class="py-2 px-3">$${r.f.toFixed(2)}</td><td class="py-2 px-3">$${r.w.toFixed(2)}</td><td class="py-2 px-3 text-emerald-600 font-semibold">$${r.rem.toFixed(2)}</td></tr>`;
            });

            renderExpenses();
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
