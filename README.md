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
            <button onclick="switchTab('personal')" id="btn-personal" class="px-4 py-2 bg-white text-gray-700 font-semibold rounded-lg
