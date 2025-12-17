<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OneKeel XDP - Everything Data Platform</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    
    <!-- Font -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">

    <style>
        body { font-family: 'Inter', sans-serif; }
        
        /* Custom Scrollbar for Sidebar */
        .scrollbar-hide::-webkit-scrollbar {
            display: none;
        }
        .scrollbar-hide {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }

        /* Smooth transitions for sections */
        .section-view {
            animation: fadeIn 0.3s ease-in-out;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(5px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        slate: {
                            850: '#1e293b', 
                            900: '#0f172a',
                        }
                    }
                }
            }
        }
    </script>
</head>
<body class="bg-slate-50 text-slate-900 overflow-hidden">

    <!-- Mobile Overlay -->
    <div id="mobile-overlay" onclick="toggleSidebar()" class="fixed inset-0 bg-black/50 z-40 hidden lg:hidden"></div>

    <!-- Sidebar -->
    <aside id="sidebar" class="fixed inset-y-0 left-0 z-50 bg-[#0f172a] text-slate-300 w-64 transition-transform duration-300 ease-in-out transform -translate-x-full lg:translate-x-0 flex flex-col">
        <!-- Logo -->
        <div class="h-16 flex items-center px-6 border-b border-slate-800 bg-[#0b1120]">
            <div class="flex items-center gap-2">
                <div class="w-8 h-8 bg-blue-500 rounded-lg flex items-center justify-center text-white font-bold text-xl">K</div>
                <div>
                    <span class="text-white font-bold text-lg tracking-tight block leading-none">ONE KEEL</span>
                    <span class="text-xs text-blue-400 font-medium tracking-widest">XDP PLATFORM</span>
                </div>
            </div>
        </div>

        <!-- Nav Links -->
        <nav class="flex-1 overflow-y-auto py-6 space-y-1 scrollbar-hide">
            <div class="px-4 mb-2 text-xs font-semibold text-slate-500 uppercase tracking-wider">Platform</div>
            <button onclick="switchSection('dashboard')" class="nav-item w-full flex items-center gap-3 px-4 py-3 text-sm font-medium transition-colors hover:bg-slate-800 hover:text-white text-slate-400" id="nav-dashboard">
                <i data-lucide="layout-dashboard" class="w-5 h-5"></i>
                <span>Dashboard</span>
            </button>
            <button onclick="switchSection('mydata')" class="nav-item w-full flex items-center gap-3 px-4 py-3 text-sm font-medium transition-colors hover:bg-slate-800 hover:text-white text-slate-400" id="nav-mydata">
                <i data-lucide="database" class="w-5 h-5"></i>
                <span>My Data</span>
            </button>
            
            <div class="px-4 mt-6 mb-2 text-xs font-semibold text-slate-500 uppercase tracking-wider">Products</div>
            <button onclick="switchSection('gseo')" class="nav-item w-full flex items-center gap-3 px-4 py-3 text-sm font-medium transition-colors hover:bg-slate-800 hover:text-white text-slate-400" id="nav-gseo">
                <i data-lucide="search" class="w-5 h-5"></i>
                <span>GSEO Hub</span>
            </button>
            <button onclick="switchSection('veeotto')" class="nav-item w-full flex items-center gap-3 px-4 py-3 text-sm font-medium transition-colors hover:bg-slate-800 hover:text-white text-slate-400" id="nav-veeotto">
                <i data-lucide="shopping-bag" class="w-5 h-5"></i>
                <span>VeeOtto</span>
            </button>
            <button onclick="switchSection('gsem')" class="nav-item w-full flex items-center gap-3 px-4 py-3 text-sm font-medium transition-colors hover:bg-slate-800 hover:text-white text-slate-400" id="nav-gsem">
                <i data-lucide="globe" class="w-5 h-5"></i>
                <span>GSEM Assistant</span>
            </button>
            <button onclick="switchSection('keelconnect')" class="nav-item w-full flex items-center gap-3 px-4 py-3 text-sm font-medium transition-colors hover:bg-slate-800 hover:text-white text-slate-400" id="nav-keelconnect">
                <i data-lucide="share-2" class="w-5 h-5"></i>
                <span>Keel Connect</span>
            </button>
            <button onclick="switchSection('watchdog')" class="nav-item w-full flex items-center gap-3 px-4 py-3 text-sm font-medium transition-colors hover:bg-slate-800 hover:text-white text-slate-400" id="nav-watchdog">
                <i data-lucide="shield-alert" class="w-5 h-5"></i>
                <span>Keel Watchdog</span>
            </button>
            <button onclick="switchSection('reporting')" class="nav-item w-full flex items-center gap-3 px-4 py-3 text-sm font-medium transition-colors hover:bg-slate-800 hover:text-white text-slate-400" id="nav-reporting">
                <i data-lucide="file-bar-chart" class="w-5 h-5"></i>
                <span>Reporting Suite</span>
            </button>

            <!-- AI Special Button -->
            <button onclick="switchSection('ai')" class="nav-item w-auto flex items-center gap-3 px-4 py-3 text-sm font-medium transition-colors mt-6 mx-2 rounded-lg shadow-lg bg-gradient-to-r from-purple-600 to-indigo-600 text-white hover:from-purple-700 hover:to-indigo-700" id="nav-ai">
                <i data-lucide="bot" class="w-5 h-5"></i>
                <span>AI Assistant</span>
            </button>
        </nav>

        <!-- User Profile -->
        <div class="p-4 border-t border-slate-800 bg-[#0b1120]">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-full bg-gradient-to-tr from-blue-500 to-cyan-400 flex items-center justify-center text-white font-bold shadow-md">
                    JD
                </div>
                <div class="flex-1 overflow-hidden">
                    <p class="text-sm font-medium text-white truncate">John Doe</p>
                    <p className="text-xs text-slate-400 truncate">Admin • OneKeel</p>
                </div>
            </div>
        </div>
    </aside>

    <!-- Main Content Wrapper -->
    <div class="flex-1 lg:ml-64 flex flex-col min-h-screen transition-all duration-300">
        
        <!-- Header -->
        <header class="h-16 bg-white border-b border-slate-200 flex items-center justify-between px-6 sticky top-0 z-40 shadow-sm">
            <div class="flex items-center gap-4">
                <button onclick="toggleSidebar()" class="lg:hidden p-2 text-slate-600 hover:bg-slate-100 rounded-md">
                    <i data-lucide="menu" class="w-6 h-6"></i>
                </button>
                <div class="flex items-center gap-2 text-sm text-slate-500">
                   <span>Platform</span> 
                   <i data-lucide="chevron-right" class="w-4 h-4"></i>
                   <span id="header-title" class="font-semibold text-slate-900">Executive Overview</span>
                </div>
            </div>

            <div class="flex items-center gap-4">
                <div class="hidden md:flex items-center bg-slate-100 rounded-full px-4 py-1.5 w-64 border border-transparent focus-within:border-blue-300 focus-within:ring-2 focus-within:ring-blue-100 transition-all">
                    <i data-lucide="search" class="w-4 h-4 text-slate-400"></i>
                    <input type="text" placeholder="Search data..." class="bg-transparent border-none focus:ring-0 text-sm ml-2 w-full outline-none text-slate-700 placeholder:text-slate-400">
                </div>

                <button class="p-2 text-slate-500 hover:bg-slate-100 rounded-full relative">
                    <i data-lucide="bell" class="w-5 h-5"></i>
                    <span class="absolute top-2 right-2 w-2 h-2 bg-red-500 rounded-full border-2 border-white"></span>
                </button>
                
                <div class="h-8 w-px bg-slate-200 mx-2 hidden sm:block"></div>

                <div class="text-right hidden sm:block">
                    <p class="text-xs font-semibold text-slate-900">OneKeel Team</p>
                    <p class="text-[10px] text-slate-500">Enterprise Plan</p>
                </div>
            </div>
        </header>

        <!-- Main Content Area -->
        <main class="p-8 flex-1 overflow-x-hidden overflow-y-auto h-[calc(100vh-64px)]">
            <div class="max-w-7xl mx-auto">
                
                <!-- SECTION: DASHBOARD -->
                <div id="section-dashboard" class="section-view space-y-6">
                    <!-- KPI Cards -->
                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                        <!-- Card 1 -->
                        <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm hover:shadow-md transition-shadow">
                            <div class="flex justify-between items-start mb-4">
                                <div class="p-2 bg-slate-50 rounded-lg">
                                    <i data-lucide="dollar-sign" class="text-slate-600 w-6 h-6"></i>
                                </div>
                                <span class="flex items-center text-xs font-medium px-2 py-1 rounded-full bg-slate-100 text-green-500">
                                    <i data-lucide="arrow-up-right" class="w-3 h-3 mr-1"></i> +18.2%
                                </span>
                            </div>
                            <h3 class="text-slate-500 text-sm font-medium uppercase tracking-wide">Total Revenue Impact</h3>
                            <p class="text-3xl font-bold mt-1 text-slate-900">$3.4M</p>
                            <p class="text-slate-400 text-xs mt-2">Attributed to XDP + AI</p>
                        </div>
                        <!-- Card 2 -->
                        <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm hover:shadow-md transition-shadow">
                            <div class="flex justify-between items-start mb-4">
                                <div class="p-2 bg-slate-50 rounded-lg">
                                    <i data-lucide="database" class="text-slate-600 w-6 h-6"></i>
                                </div>
                                <span class="flex items-center text-xs font-medium px-2 py-1 rounded-full bg-slate-100 text-blue-500">
                                    <i data-lucide="arrow-up-right" class="w-3 h-3 mr-1"></i> +2.4M
                                </span>
                            </div>
                            <h3 class="text-slate-500 text-sm font-medium uppercase tracking-wide">Data Records Ingested</h3>
                            <p class="text-3xl font-bold mt-1 text-slate-900">61.2M</p>
                            <p class="text-slate-400 text-xs mt-2">Identity Graph + CRM + DMS</p>
                        </div>
                        <!-- Card 3 -->
                        <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm hover:shadow-md transition-shadow">
                            <div class="flex justify-between items-start mb-4">
                                <div class="p-2 bg-slate-50 rounded-lg">
                                    <i data-lucide="bot" class="text-slate-600 w-6 h-6"></i>
                                </div>
                                <span class="flex items-center text-xs font-medium px-2 py-1 rounded-full bg-slate-100 text-purple-500">
                                    <i data-lucide="arrow-up-right" class="w-3 h-3 mr-1"></i> +45%
                                </span>
                            </div>
                            <h3 class="text-slate-500 text-sm font-medium uppercase tracking-wide">AI Leads Engaged</h3>
                            <p class="text-3xl font-bold mt-1 text-slate-900">8,942</p>
                            <p class="text-slate-400 text-xs mt-2">Last 30 Days</p>
                        </div>
                        <!-- Card 4 -->
                        <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm hover:shadow-md transition-shadow">
                            <div class="flex justify-between items-start mb-4">
                                <div class="p-2 bg-slate-50 rounded-lg">
                                    <i data-lucide="activity" class="text-slate-600 w-6 h-6"></i>
                                </div>
                                <span class="flex items-center text-xs font-medium px-2 py-1 rounded-full bg-slate-100 text-slate-500">
                                    Stable
                                </span>
                            </div>
                            <h3 class="text-slate-500 text-sm font-medium uppercase tracking-wide">Active Campaigns</h3>
                            <p class="text-3xl font-bold mt-1 text-slate-900">14</p>
                            <p class="text-slate-400 text-xs mt-2">Across 5 Channels</p>
                        </div>
                    </div>

                    <!-- Revenue Chart -->
                    <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                        <h3 class="text-lg font-bold text-slate-900 mb-4">Revenue Impact Analysis</h3>
                        <div class="relative h-72 w-full">
                            <canvas id="revenueChart"></canvas>
                        </div>
                    </div>
                </div>

                <!-- SECTION: GSEO -->
                <div id="section-gseo" class="section-view hidden space-y-6">
                     <div class="border-b border-slate-200 flex gap-4 mb-6">
                        <button class="px-4 py-2 text-sm font-medium border-b-2 border-blue-600 text-blue-600">SEO Center</button>
                        <button class="px-4 py-2 text-sm font-medium border-b-2 border-transparent text-slate-500 hover:text-slate-700">SEO Chat</button>
                        <button class="px-4 py-2 text-sm font-medium border-b-2 border-transparent text-slate-500 hover:text-slate-700">Insights</button>
                     </div>

                     <div class="flex justify-between items-center">
                        <div>
                          <h2 class="text-2xl font-bold text-slate-900">SEO Center</h2>
                          <p class="text-slate-500">Manage SEO tasks, track progress, and implement optimization recommendations</p>
                        </div>
                        <div class="flex gap-2">
                           <button class="flex items-center gap-2 px-4 py-2 bg-white border border-slate-300 rounded-lg text-slate-700 hover:bg-slate-50 text-sm">
                             <i data-lucide="refresh-cw" class="w-4 h-4"></i> Refresh
                           </button>
                           <button class="flex items-center gap-2 px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 text-sm">
                             <i data-lucide="plus" class="w-4 h-4"></i> New Task
                           </button>
                        </div>
                      </div>

                      <div class="grid grid-cols-1 md:grid-cols-4 gap-6">
                        <!-- Page Stats -->
                        <div class="p-5 bg-white rounded-xl border border-slate-200 shadow-sm">
                            <h4 class="text-sm font-medium text-slate-500 mb-2">Pages</h4>
                            <div class="flex items-end gap-2">
                               <span class="text-3xl font-bold text-slate-900">5/5</span>
                               <span class="text-xs text-green-600 font-medium mb-1">Complete</span>
                            </div>
                            <div class="w-full bg-slate-100 h-2 mt-3 rounded-full overflow-hidden">
                               <div class="bg-green-500 h-full w-full"></div>
                            </div>
                        </div>
                         <!-- Blogs Stats -->
                         <div class="p-5 bg-white rounded-xl border border-slate-200 shadow-sm">
                            <h4 class="text-sm font-medium text-slate-500 mb-2">Blogs</h4>
                            <div class="flex items-end gap-2">
                               <span class="text-3xl font-bold text-slate-900">3/6</span>
                               <span class="text-xs text-blue-600 font-medium mb-1">In Progress</span>
                            </div>
                            <div class="w-full bg-slate-100 h-2 mt-3 rounded-full overflow-hidden">
                               <div class="bg-blue-500 h-full w-1/2"></div>
                            </div>
                        </div>
                        <!-- GBP Stats -->
                        <div class="p-5 bg-white rounded-xl border border-slate-200 shadow-sm">
                            <h4 class="text-sm font-medium text-slate-500 mb-2">GBP Posts</h4>
                            <div class="flex items-end gap-2">
                               <span class="text-3xl font-bold text-slate-900">7/12</span>
                            </div>
                            <div class="w-full bg-slate-100 h-2 mt-3 rounded-full overflow-hidden">
                               <div class="bg-purple-500 h-full w-[58%]"></div>
                            </div>
                        </div>
                        <!-- SEO Changes -->
                        <div class="p-5 bg-white rounded-xl border border-slate-200 shadow-sm">
                            <h4 class="text-sm font-medium text-slate-500 mb-2">SEO/GEO Changes</h4>
                            <div class="flex items-end gap-2">
                               <span class="text-3xl font-bold text-slate-900">5/10</span>
                            </div>
                            <div class="w-full bg-slate-100 h-2 mt-3 rounded-full overflow-hidden">
                               <div class="bg-orange-500 h-full w-1/2"></div>
                            </div>
                        </div>
                      </div>

                      <div class="bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
                        <table class="w-full text-left text-sm">
                           <thead class="bg-slate-50 text-slate-500 font-medium">
                              <tr>
                                 <th class="px-6 py-3">Type</th>
                                 <th class="px-6 py-3">Task Name</th>
                                 <th class="px-6 py-3">Date</th>
                                 <th class="px-6 py-3">Status</th>
                                 <th class="px-6 py-3">Action</th>
                              </tr>
                           </thead>
                           <tbody class="divide-y divide-slate-100">
                                <tr class="hover:bg-slate-50">
                                    <td class="px-6 py-4"><span class="px-2 py-1 rounded-full text-xs font-bold bg-blue-100 text-blue-700">BLOG</span></td>
                                    <td class="px-6 py-4 font-medium text-slate-900">2026 Jeep Wrangler near Washington</td>
                                    <td class="px-6 py-4 text-slate-500">12/16/2025</td>
                                    <td class="px-6 py-4 text-green-600 font-medium">Complete</td>
                                    <td class="px-6 py-4 text-blue-600 cursor-pointer hover:underline">View</td>
                                </tr>
                                <tr class="hover:bg-slate-50">
                                    <td class="px-6 py-4"><span class="px-2 py-1 rounded-full text-xs font-bold bg-purple-100 text-purple-700">GBP</span></td>
                                    <td class="px-6 py-4 font-medium text-slate-900">2026 Jeep Wrangler near Washington</td>
                                    <td class="px-6 py-4 text-slate-500">12/17/2025</td>
                                    <td class="px-6 py-4 text-green-600 font-medium">Completed</td>
                                    <td class="px-6 py-4 text-blue-600 cursor-pointer hover:underline">View</td>
                                </tr>
                                <tr class="hover:bg-slate-50">
                                    <td class="px-6 py-4"><span class="px-2 py-1 rounded-full text-xs font-bold bg-green-100 text-green-700">Page</span></td>
                                    <td class="px-6 py-4 font-medium text-slate-900">2025 Ram 1500 Towing Capacity</td>
                                    <td class="px-6 py-4 text-slate-500">12/15/2025</td>
                                    <td class="px-6 py-4 text-orange-600 font-medium">Pending</td>
                                    <td class="px-6 py-4 text-blue-600 cursor-pointer hover:underline">View</td>
                                </tr>
                           </tbody>
                        </table>
                     </div>
                </div>

                <!-- SECTION: VeeOtto -->
                <div id="section-veeotto" class="section-view hidden space-y-6">
                    <div class="flex justify-between items-center">
                        <h2 class="text-2xl font-bold text-slate-900">VeeOtto Dashboard</h2>
                        <div class="text-sm text-slate-500 bg-white px-3 py-1.5 rounded-lg border border-slate-200">
                           Current Range: This Month (2025-12-01 to 2025-12-31)
                        </div>
                     </div>
              
                     <!-- Top Stats -->
                     <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                        <div class="bg-slate-900 text-white p-5 rounded-xl shadow-lg">
                           <div class="text-slate-400 text-xs font-bold uppercase mb-1">Total Vehicles</div>
                           <div class="text-3xl font-bold">4,232</div>
                        </div>
                        <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
                           <div class="text-slate-500 text-xs font-bold uppercase mb-1">Descriptions Updated</div>
                           <div class="text-3xl font-bold text-slate-900">2,919</div>
                        </div>
                        <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
                           <div class="text-slate-500 text-xs font-bold uppercase mb-1">Features Marked</div>
                           <div class="text-3xl font-bold text-slate-900">19,125</div>
                        </div>
                        <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
                           <div class="text-slate-500 text-xs font-bold uppercase mb-1">Time Saved</div>
                           <div class="text-3xl font-bold text-slate-900">767 <span class="text-sm font-normal text-slate-500">hours</span></div>
                        </div>
                     </div>
              
                     <!-- Automation Impact -->
                     <div>
                        <h3 class="text-lg font-bold text-slate-900 mb-4 uppercase text-sm tracking-wider">Automation Impact (Book Value Changes)</h3>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                           <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                              <div class="text-slate-500 font-medium mb-2">Black Book</div>
                              <div class="text-2xl font-bold text-green-500">+$1,305,237</div>
                           </div>
                           <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                              <div class="text-slate-500 font-medium mb-2">KBB.com</div>
                              <div class="text-2xl font-bold text-green-500">+$761,816</div>
                           </div>
                           <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                              <div class="text-slate-500 font-medium mb-2">J.D. Power</div>
                              <div class="text-2xl font-bold text-green-500">+$418,765</div>
                           </div>
                        </div>
                     </div>
                </div>

                <!-- SECTION: Reporting Suite -->
                <div id="section-reporting" class="section-view hidden space-y-6">
                    <!-- Header Controls -->
                    <div class="flex flex-col md:flex-row justify-between items-center gap-4 bg-white p-4 rounded-xl border border-slate-200 shadow-sm">
                        <div>
                        <h2 class="text-xl font-bold text-slate-900">Campaign Performance</h2>
                        <p class="text-sm text-slate-500">Cross-channel marketing analytics and ROI tracking</p>
                        </div>
                        <div class="flex gap-3">
                            <button class="flex items-center gap-2 px-4 py-2 bg-slate-50 border border-slate-200 rounded-lg text-sm font-medium text-slate-700 hover:bg-slate-100">
                                <i data-lucide="calendar" class="w-4 h-4"></i> Last 30 Days
                            </button>
                            <button class="flex items-center gap-2 px-4 py-2 bg-blue-600 text-white rounded-lg text-sm font-medium hover:bg-blue-700">
                                <i data-lucide="download" class="w-4 h-4"></i> Export Report
                            </button>
                        </div>
                    </div>

                    <!-- Reporting KPIs -->
                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                        <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                            <h3 class="text-slate-500 text-sm font-medium uppercase tracking-wide">Total Ad Spend</h3>
                            <p class="text-3xl font-bold mt-1 text-slate-900">$272,100</p>
                            <span class="text-xs font-medium px-2 py-1 rounded-full bg-slate-100 text-red-500 mt-2 inline-block">+12% vs last mo</span>
                        </div>
                        <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                            <h3 class="text-slate-500 text-sm font-medium uppercase tracking-wide">Revenue Generated</h3>
                            <p class="text-3xl font-bold mt-1 text-slate-900">$1,101,800</p>
                            <span class="text-xs font-medium px-2 py-1 rounded-full bg-slate-100 text-green-500 mt-2 inline-block">+24.5%</span>
                        </div>
                        <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                            <h3 class="text-slate-500 text-sm font-medium uppercase tracking-wide">Blended ROAS</h3>
                            <p class="text-3xl font-bold mt-1 text-slate-900">4.05x</p>
                            <span class="text-xs font-medium px-2 py-1 rounded-full bg-slate-100 text-blue-500 mt-2 inline-block">+0.4x</span>
                        </div>
                        <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                            <h3 class="text-slate-500 text-sm font-medium uppercase tracking-wide">Cost Per Lead (CPA)</h3>
                            <p class="text-3xl font-bold mt-1 text-slate-900">$19.87</p>
                            <span class="text-xs font-medium px-2 py-1 rounded-full bg-slate-100 text-green-500 mt-2 inline-block">-5.2%</span>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                         <!-- Spend vs Revenue Chart -->
                        <div class="lg:col-span-2 bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                            <h3 class="text-lg font-bold text-slate-900 mb-6">Spend vs. Revenue Trend</h3>
                            <div class="h-80 w-full relative">
                                <canvas id="reportingChart"></canvas>
                            </div>
                        </div>

                         <!-- Allocation Donut -->
                         <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm flex flex-col">
                            <h3 class="text-lg font-bold text-slate-900 mb-2">Spend Allocation</h3>
                            <div class="flex-1 min-h-[250px] relative flex items-center justify-center">
                                <div class="w-full h-64 relative">
                                    <canvas id="allocationChart"></canvas>
                                    <!-- Center Text -->
                                    <div class="absolute inset-0 flex items-center justify-center pointer-events-none">
                                        <div class="text-center">
                                            <span class="block text-2xl font-bold text-slate-900">100%</span>
                                            <span class="text-xs text-slate-500">Allocation</span>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                 <!-- SECTION: Keel Connect -->
                 <div id="section-keelconnect" class="section-view hidden space-y-6">
                    <div class="flex justify-between items-center mb-2">
                        <h2 class="text-2xl font-bold text-slate-900">Keel Connect</h2>
                        <div class="text-sm font-medium text-slate-500">Welcome back, Josh!</div>
                     </div>
                     <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                        <div class="bg-white p-8 rounded-2xl border border-slate-200 shadow-sm flex flex-col justify-center items-center text-center h-64">
                           <div class="mb-4 p-4 bg-blue-50 rounded-full text-blue-600"><i data-lucide="zap" class="w-8 h-8"></i></div>
                           <div class="text-4xl font-extrabold text-slate-900 mb-1">132</div>
                           <div class="text-sm font-bold text-slate-500 uppercase tracking-wide">Total Campaigns</div>
                           <div class="text-xs text-green-500 font-medium mt-1">11 active</div>
                        </div>
                        <div class="bg-white p-8 rounded-2xl border border-slate-200 shadow-sm flex flex-col justify-center items-center text-center h-64">
                            <div class="mb-4 p-4 bg-purple-50 rounded-full text-purple-600"><i data-lucide="users" class="w-8 h-8"></i></div>
                            <div class="text-4xl font-extrabold text-slate-900 mb-1">15,215</div>
                            <div class="text-sm font-bold text-slate-500 uppercase tracking-wide">Total Leads</div>
                            <div class="text-xs text-slate-400 mt-1">Across all campaigns</div>
                        </div>
                        <div class="bg-white p-8 rounded-2xl border border-slate-200 shadow-sm flex flex-col justify-center items-center text-center h-64">
                            <div class="mb-4 p-4 bg-orange-50 rounded-full text-orange-600"><i data-lucide="message-square" class="w-8 h-8"></i></div>
                            <div class="text-4xl font-extrabold text-slate-900 mb-1">14,913</div>
                            <div class="text-sm font-bold text-slate-500 uppercase tracking-wide">Conversations</div>
                            <div class="text-xs text-slate-400 mt-1">Total active threads</div>
                        </div>
                        <div class="bg-white p-8 rounded-2xl border border-slate-200 shadow-sm flex flex-col justify-center items-center text-center h-64">
                            <div class="mb-4 p-4 bg-green-50 rounded-full text-green-600"><i data-lucide="send" class="w-8 h-8"></i></div>
                            <div class="text-4xl font-extrabold text-slate-900 mb-1">23,499</div>
                            <div class="text-sm font-bold text-slate-500 uppercase tracking-wide">Messages Sent</div>
                            <div class="text-xs text-slate-400 mt-1">Email & SMS combined</div>
                        </div>
                    </div>
                </div>

                <!-- SECTION: Watchdog -->
                <div id="section-watchdog" class="section-view hidden h-full flex flex-col">
                    <div class="flex-1 bg-white rounded-xl border border-slate-200 shadow-sm flex flex-col overflow-hidden">
                        <div class="flex-1 p-8 flex flex-col items-center justify-center text-center max-w-2xl mx-auto w-full">
                           <div class="w-16 h-16 bg-gradient-to-br from-indigo-500 to-purple-600 rounded-2xl flex items-center justify-center text-white mb-6 shadow-lg">
                              <i data-lucide="shield-alert" class="w-8 h-8"></i>
                           </div>
                           <h2 class="text-2xl font-bold text-slate-900 mb-2">Keel Watchdog Assistant</h2>
                           <div class="px-3 py-1 bg-slate-100 rounded-full text-xs font-bold text-slate-600 uppercase tracking-wider mb-6">Facts Only</div>
                           <p class="text-slate-500 mb-8 max-w-md">Your data reporter for paid search analytics at ABC Motors. I provide metrics, trend analysis, and citations without strategic advice.</p>
                           
                           <div class="grid grid-cols-1 md:grid-cols-2 gap-4 w-full mb-8">
                              <button class="p-4 bg-slate-50 border border-slate-200 rounded-xl text-left text-sm text-slate-700 hover:bg-blue-50 hover:border-blue-200 transition-colors">
                                 What is my CPC trend for the last 60 days?
                              </button>
                              <button class="p-4 bg-slate-50 border border-slate-200 rounded-xl text-left text-sm text-slate-700 hover:bg-blue-50 hover:border-blue-200 transition-colors">
                                 How many conversions did I get from Meta last month?
                              </button>
                           </div>
                        </div>
                        <div class="p-6 border-t border-slate-100 bg-slate-50">
                           <div class="relative max-w-3xl mx-auto">
                              <input type="text" placeholder="Ask about metrics, trends, or comparisons (facts only)..." class="w-full pl-6 pr-12 py-4 rounded-full border border-slate-300 shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                              <button class="absolute right-3 top-3 p-2 bg-blue-600 text-white rounded-full hover:bg-blue-700">
                                 <i data-lucide="arrow-up-right" class="w-5 h-5"></i>
                              </button>
                           </div>
                        </div>
                     </div>
                </div>

                <!-- SECTION: GSEM -->
                <div id="section-gsem" class="section-view hidden">
                    <div class="flex flex-col items-center justify-center min-h-[600px] bg-gradient-to-b from-white to-slate-50 rounded-2xl border border-slate-200 text-center p-8">
                        <div class="w-20 h-20 bg-blue-100 rounded-full flex items-center justify-center mb-8">
                           <i data-lucide="globe" class="w-10 h-10 text-blue-600"></i>
                        </div>
                        <h2 class="text-4xl font-extrabold text-slate-900 mb-4">GSEM Assistant</h2>
                        <p class="text-xl text-slate-600 mb-2">Google Ads Management for Automotive Dealerships</p>
                        <p class="text-slate-500 max-w-lg mb-10">AI-powered insights and optimization for your Google Ads campaigns. Connect your accounts, chat with AI, and grow your dealership.</p>
                        <div class="flex gap-4">
                           <button class="px-8 py-3 bg-blue-600 text-white font-bold rounded-lg shadow-lg hover:bg-blue-700 transition-colors">
                              Start Free Trial →
                           </button>
                           <button class="px-8 py-3 bg-white text-slate-700 font-bold border border-slate-300 rounded-lg hover:bg-slate-50 transition-colors">
                              Watch Demo
                           </button>
                        </div>
                     </div>
                </div>

                <!-- GENERIC PLACEHOLDER FOR OTHERS -->
                <div id="section-generic" class="section-view hidden flex flex-col items-center justify-center min-h-[400px] text-slate-400">
                    <i data-lucide="settings" class="w-12 h-12 mb-4 opacity-50"></i>
                    <h2 class="text-xl font-medium">Coming Soon</h2>
                    <p class="text-sm">This module is under development.</p>
                </div>

            </div>
        </main>

    </div>

    <!-- JavaScript Logic -->
    <script>
        // --- 1. Navigation Logic ---
        const sections = ['dashboard', 'gseo', 'veeotto', 'keelconnect', 'watchdog', 'gsem', 'reporting', 'mydata', 'ai'];
        
        function switchSection(sectionId) {
            // Update Header Title
            const titles = {
                'dashboard': 'Executive Overview',
                'gseo': 'GSEO Hub',
                'veeotto': 'VeeOtto Automation',
                'keelconnect': 'Keel Connect',
                'watchdog': 'Keel Watchdog',
                'gsem': 'GSEM Assistant',
                'reporting': 'Reporting Suite',
                'mydata': 'My Data',
                'ai': 'AI Assistant'
            };
            document.getElementById('header-title').innerText = titles[sectionId] || 'Platform';

            // Hide all sections
            document.querySelectorAll('.section-view').forEach(el => el.classList.add('hidden'));

            // Show target section (or generic if not implemented in HTML)
            const target = document.getElementById(`section-${sectionId}`);
            if (target) {
                target.classList.remove('hidden');
            } else {
                document.getElementById('section-generic').classList.remove('hidden');
            }

            // Update Sidebar Active State
            document.querySelectorAll('.nav-item').forEach(el => {
                // Reset styles
                if (el.id === 'nav-ai') {
                    // AI button special style reset? It stays special. 
                } else {
                    el.classList.remove('bg-slate-800', 'text-blue-400', 'border-r-4', 'border-blue-400');
                    el.classList.add('text-slate-400');
                }
            });

            // Set Active Style
            const activeNav = document.getElementById(`nav-${sectionId}`);
            if (activeNav && sectionId !== 'ai') {
                activeNav.classList.remove('text-slate-400');
                activeNav.classList.add('bg-slate-800', 'text-blue-400', 'border-r-4', 'border-blue-400');
            }

            // Mobile: Close sidebar if open
            if(window.innerWidth < 1024) {
                document.getElementById('sidebar').classList.add('-translate-x-full');
                document.getElementById('mobile-overlay').classList.add('hidden');
            }

            // Trigger Chart renders if needed
            if (sectionId === 'dashboard') renderDashboardCharts();
            if (sectionId === 'reporting') renderReportingCharts();
        }

        function toggleSidebar() {
            const sidebar = document.getElementById('sidebar');
            const overlay = document.getElementById('mobile-overlay');
            
            if (sidebar.classList.contains('-translate-x-full')) {
                sidebar.classList.remove('-translate-x-full');
                overlay.classList.remove('hidden');
            } else {
                sidebar.classList.add('-translate-x-full');
                overlay.classList.add('hidden');
            }
        }

        // --- 2. Chart Logic (Chart.js) ---
        let revenueChartInstance = null;
        let reportingChartInstance = null;
        let allocationChartInstance = null;

        function renderDashboardCharts() {
            const ctx = document.getElementById('revenueChart');
            if (!ctx) return;
            if (revenueChartInstance) return; // Already rendered

            revenueChartInstance = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
                    datasets: [{
                        label: 'XDP Impact',
                        data: [240000, 139800, 380000, 290000, 450000, 550000],
                        borderColor: '#3b82f6',
                        backgroundColor: 'rgba(59, 130, 246, 0.1)',
                        fill: true,
                        tension: 0.4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: {
                        y: { display: false, grid: { display: false } },
                        x: { grid: { display: false }, ticks: { color: '#94a3b8' } }
                    }
                }
            });
        }

        function renderReportingCharts() {
            // Spend vs Revenue
            const ctx1 = document.getElementById('reportingChart');
            if (ctx1 && !reportingChartInstance) {
                reportingChartInstance = new Chart(ctx1, {
                    type: 'line',
                    data: {
                        labels: ['Dec 01', 'Dec 05', 'Dec 10', 'Dec 15', 'Dec 20', 'Dec 25', 'Dec 30'],
                        datasets: [
                            {
                                label: 'Revenue',
                                data: [18000, 22000, 21500, 28000, 25000, 35000, 31000],
                                borderColor: '#3b82f6',
                                backgroundColor: 'rgba(59, 130, 246, 0.1)',
                                fill: true,
                                tension: 0.4,
                                order: 1
                            },
                            {
                                label: 'Ad Spend',
                                data: [4500, 5200, 4800, 6100, 5500, 7000, 6800],
                                borderColor: '#ef4444',
                                borderDash: [5, 5],
                                fill: false,
                                tension: 0.4,
                                order: 2
                            }
                        ]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: { legend: { position: 'top' } },
                        scales: {
                            y: { display: true, grid: { color: '#f1f5f9' }, ticks: { color: '#94a3b8' } },
                            x: { grid: { display: false }, ticks: { color: '#94a3b8' } }
                        }
                    }
                });
            }

            // Allocation Donut
            const ctx2 = document.getElementById('allocationChart');
            if (ctx2 && !allocationChartInstance) {
                allocationChartInstance = new Chart(ctx2, {
                    type: 'doughnut',
                    data: {
                        labels: ['Google Ads', 'Social', 'Email', 'SMS', 'Amazon'],
                        datasets: [{
                            data: [45, 25, 15, 10, 5],
                            backgroundColor: ['#3b82f6', '#8b5cf6', '#10b981', '#f59e0b', '#ef4444'],
                            borderWidth: 0,
                            hoverOffset: 4
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        cutout: '75%',
                        plugins: { legend: { position: 'bottom', labels: { usePointStyle: true, padding: 20 } } }
                    }
                });
            }
        }

        // --- 3. Initialization ---
        document.addEventListener('DOMContentLoaded', () => {
            // Initialize Icons
            lucide.createIcons();
            
            // Start at Dashboard
            switchSection('dashboard');
        });

    </script>
</body>
</html>
