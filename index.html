<!DOCTYPE html>
<html lang="en" class="h-full">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>SpendWise — Smart Fintech & AI Expense Tracker</title>
  
  <!-- Tailwind CSS & Lucide Icons & Chart.js -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <script src="https://unpkg.com/lucide@latest"></script>

  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            brand: {
              50: '#eef2ff',
              100: '#e0e7ff',
              500: '#6366f1',
              600: '#4f46e5',
              700: '#4338ca',
              900: '#312e81',
            },
            surface: {
              light: '#f8fafc',
              dark: '#0b0f19',
              cardLight: '#ffffff',
              cardDark: '#131b2e',
              borderLight: '#e2e8f0',
              borderDark: '#1e293b'
            }
          }
        }
      }
    }
  </script>

  <style>
    @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap');
    body {
      font-family: 'Plus Jakarta Sans', sans-serif;
    }
    .custom-scrollbar::-webkit-scrollbar {
      width: 5px;
      height: 5px;
    }
    .custom-scrollbar::-webkit-scrollbar-thumb {
      background: rgba(156, 163, 175, 0.4);
      border-radius: 9999px;
    }
    .pulse-glow {
      box-shadow: 0 0 25px rgba(99, 102, 241, 0.45);
    }
  </style>
</head>

<body class="h-full bg-slate-50 dark:bg-[#0b0f19] text-slate-800 dark:text-slate-100 transition-colors duration-200">
  <div id="app" class="h-full flex flex-col"></div>

  <!-- Main Application Script -->
  <script>
    // ==========================================
    // DATA LAYER & INITIAL LOCALSTORAGE SEED
    // ==========================================
    const DEFAULT_USER = {
      name: "Alex Morgan",
      email: "alex@spendwise.io",
      password: "password123",
      currency: "₹",
      currencyCode: "INR",
      monthlyBudget: 25000,
      darkMode: false,
      notifications: true,
      apiKey: ""
    };

    const DEFAULT_TRANSACTIONS = [
      { id: "tx-1", title: "Freelance Client Retainer", amount: 35000, type: "income", category: "Salary", paymentMethod: "UPI", date: "2026-09-28", time: "10:00 AM", note: "Web App deliverable" },
      { id: "tx-2", title: "Grocery & Provisions", amount: 3200, type: "expense", category: "Food", paymentMethod: "Credit Card", date: "2026-09-28", time: "06:30 PM", note: "Supermarket trip" },
      { id: "tx-3", title: "Metro SmartCard Recharge", amount: 800, type: "expense", category: "Travel", paymentMethod: "UPI", date: "2026-09-27", time: "09:15 AM", note: "Monthly commute" },
      { id: "tx-4", title: "Cloud Hosting & Domains", amount: 1450, type: "expense", category: "Bills", paymentMethod: "Debit Card", date: "2026-09-26", time: "02:20 PM", note: "AWS & Vercel bills" },
      { id: "tx-5", title: "Weekend Movie & Snacks", amount: 950, type: "expense", category: "Entertainment", paymentMethod: "UPI", date: "2026-09-25", time: "08:45 PM", note: "IMAX screening" }
    ];

    // Core State Container
    const state = {
      user: JSON.parse(localStorage.getItem('spendwise_user')) || DEFAULT_USER,
      transactions: JSON.parse(localStorage.getItem('spendwise_transactions')) || DEFAULT_TRANSACTIONS,
      isLoggedIn: localStorage.getItem('spendwise_auth') === 'true',
      currentPage: 'dashboard', // landing, login, signup, dashboard, analytics, budget, transactions, settings
      activeModal: null, // 'expense', 'income', 'budget', 'aiKey', 'editTx'
      editingTx: null,
      filterType: 'all',
      filterCategory: 'all',
      searchQuery: '',
      sortField: 'date-desc',
      aiChatOpen: false,
      aiApiKey: localStorage.getItem('spendwise_gemini_api_key') || '',
      aiMessages: [
        {
          role: 'model',
          text: "Hi Alex! I'm your SpendWise Financial Copilot powered by Gemini 3.5 Flash-Lite. You can ask me to log expenses, check your remaining budget, analyze categories, or navigate the dashboard.",
          timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
        }
      ],
      aiThinking: false
    };

    function persistState() {
      localStorage.setItem('spendwise_user', JSON.stringify(state.user));
      localStorage.setItem('spendwise_transactions', JSON.stringify(state.transactions));
      localStorage.setItem('spendwise_auth', state.isLoggedIn);
      localStorage.setItem('spendwise_gemini_api_key', state.aiApiKey);
    }

    // Apply Dark Mode Class
    function applyTheme() {
      if (state.user.darkMode) {
        document.documentElement.classList.add('dark');
      } else {
        document.documentElement.classList.remove('dark');
      }
    }
    applyTheme();

    // ==========================================
    // COMPUTED FINANCIAL ENGINE
    // ==========================================
    function getFinancials() {
      const income = state.transactions
        .filter(t => t.type === 'income')
        .reduce((sum, t) => sum + Number(t.amount), 0);

      const expenses = state.transactions
        .filter(t => t.type === 'expense')
        .reduce((sum, t) => sum + Number(t.amount), 0);

      const balance = income - expenses;
      const budget = Number(state.user.monthlyBudget) || 1;
      const budgetUsedPercent = ((expenses / budget) * 100).toFixed(1);
      const remainingBudget = budget - expenses;

      let suggestion = "You're comfortably within your planned budget.";
      let suggestionLevel = "success";
      const pct = Number(budgetUsedPercent);

      if (pct > 100) {
        suggestion = "You have exceeded your planned monthly budget.";
        suggestionLevel = "danger";
      } else if (pct >= 90) {
        suggestion = "Your budget is almost fully used. Consider limiting non-essential spending.";
        suggestionLevel = "danger";
      } else if (pct >= 75) {
        suggestion = "You are approaching your monthly expense limit. Consider reviewing upcoming expenses.";
        suggestionLevel = "warning";
      } else if (pct >= 50) {
        suggestion = `You have used ${budgetUsedPercent}% of your monthly budget. Keep tracking your expenses.`;
        suggestionLevel = "info";
      }

      return {
        income,
        expenses,
        balance,
        budget,
        budgetUsedPercent,
        remainingBudget,
        suggestion,
        suggestionLevel
      };
    }

    function formatCurrency(amount) {
      return `${state.user.currency}${Number(amount).toLocaleString('en-IN')}`;
    }

    function showToast(message, type = 'info') {
      const existing = document.getElementById('toast-notification');
      if (existing) existing.remove();

      const toast = document.createElement('div');
      toast.id = 'toast-notification';
      const color = type === 'success' ? 'bg-emerald-600' : type === 'error' ? 'bg-rose-600' : 'bg-indigo-600';
      toast.className = `fixed top-6 right-6 z-50 ${color} text-white px-5 py-3 rounded-xl shadow-2xl flex items-center gap-3 transition-all duration-300 transform translate-y-0 text-sm font-medium animate-bounce`;
      toast.innerHTML = `<i data-lucide="${type === 'success' ? 'check-circle-2' : type === 'error' ? 'alert-circle' : 'info'}" class="w-5 h-5"></i> <span>${message}</span>`;
      document.body.appendChild(toast);
      lucide.createIcons();

      setTimeout(() => {
        toast.style.opacity = '0';
        setTimeout(() => toast.remove(), 300);
      }, 3500);
    }

    // ==========================================
    // GEMINI 3.5 FLASH-LITE FUNCTION DEFINITIONS
    // ==========================================
    const GEMINI_TOOLS_DECLARATION = {
      function_declarations: [
        {
          name: "addExpense",
          description: "Add a new expense transaction to SpendWise.",
          parameters: {
            type: "OBJECT",
            properties: {
              title: { type: "STRING", description: "Expense description or item name (e.g., Grocery, Uber, Starbucks coffee)" },
              amount: { type: "NUMBER", description: "Expense amount in user's currency" },
              category: { 
                type: "STRING", 
                enum: ["Food", "Travel", "Shopping", "Education", "Bills", "Entertainment", "Health", "Other"],
                description: "Category of the expense" 
              },
              paymentMethod: { 
                type: "STRING", 
                enum: ["Cash", "UPI", "Debit Card", "Credit Card", "Other"],
                description: "Payment method used" 
              },
              note: { type: "STRING", description: "Optional note or additional detail" }
            },
            required: ["title", "amount", "category"]
          }
        },
        {
          name: "addIncome",
          description: "Add a new income transaction to SpendWise.",
          parameters: {
            type: "OBJECT",
            properties: {
              title: { type: "STRING", description: "Income source title (e.g., Salary, Dividend, Freelance gig)" },
              amount: { type: "NUMBER", description: "Income amount" },
              category: { type: "STRING", description: "Category (e.g., Salary, Investment, Pocket Money, Bonus)" },
              paymentMethod: { type: "STRING", enum: ["UPI", "Bank Transfer", "Cash", "Cheque", "Other"] },
              note: { type: "STRING", description: "Optional income note" }
            },
            required: ["title", "amount"]
          }
        },
        {
          name: "setMonthlyBudget",
          description: "Update the user's monthly expense budget limit.",
          parameters: {
            type: "OBJECT",
            properties: {
              amount: { type: "NUMBER", description: "New monthly budget limit" }
            },
            required: ["amount"]
          }
        },
        {
          name: "getFinancialSummary",
          description: "Retrieve available balance, total income, total expenses, remaining budget, and financial health suggestions.",
          parameters: {
            type: "OBJECT",
            properties: {}
          }
        },
        {
          name: "searchTransactions",
          description: "Search or filter transactions by keyword, type (income/expense), or category.",
          parameters: {
            type: "OBJECT",
            properties: {
              query: { type: "STRING", description: "Search keyword" },
              type: { type: "STRING", enum: ["all", "income", "expense"] },
              category: { type: "STRING", description: "Optional category filter" }
            }
          }
        },
        {
          name: "deleteTransaction",
          description: "Delete a transaction given its title or ID.",
          parameters: {
            type: "OBJECT",
            properties: {
              identifier: { type: "STRING", description: "The exact ID or title of the transaction to delete" }
            },
            required: ["identifier"]
          }
        },
        {
          name: "navigateToPage",
          description: "Navigate to a specific view in SpendWise.",
          parameters: {
            type: "OBJECT",
            properties: {
              page: { 
                type: "STRING", 
                enum: ["dashboard", "analytics", "budget", "transactions", "settings"],
                description: "Target view" 
              }
            },
            required: ["page"]
          }
        },
        {
          name: "toggleTheme",
          description: "Switch between dark mode and light mode.",
          parameters: {
            type: "OBJECT",
            properties: {
              mode: { type: "STRING", enum: ["dark", "light"], description: "Desired theme" }
            },
            required: ["mode"]
          }
        }
      ]
    };

    // ==========================================
    // DISPATCHER: EXECUTES APPS ACTIONS VIA TOOLS
    // ==========================================
    async function executeAppTool(name, args) {
      const now = new Date();
      const dateStr = now.toISOString().split('T')[0];
      const timeStr = now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });

      switch (name) {
        case 'addExpense': {
          const newTx = {
            id: 'tx-' + Date.now(),
            title: args.title,
            amount: Number(args.amount),
            type: 'expense',
            category: args.category || 'Other',
            paymentMethod: args.paymentMethod || 'UPI',
            date: dateStr,
            time: timeStr,
            note: args.note || 'Logged via Gemini 3.5 AI Copilot'
          };
          state.transactions.unshift(newTx);
          persistState();
          renderApp();
          showToast(`Expense added: ${formatCurrency(newTx.amount)} for ${newTx.title}`, 'success');
          return {
            success: true,
            message: `Expense '${newTx.title}' of ${formatCurrency(newTx.amount)} recorded successfully in ${newTx.category}.`,
            currentFinancials: getFinancials()
          };
        }

        case 'addIncome': {
          const newTx = {
            id: 'tx-' + Date.now(),
            title: args.title,
            amount: Number(args.amount),
            type: 'income',
            category: args.category || 'Salary',
            paymentMethod: args.paymentMethod || 'UPI',
            date: dateStr,
            time: timeStr,
            note: args.note || 'Logged via Gemini 3.5 AI Copilot'
          };
          state.transactions.unshift(newTx);
          persistState();
          renderApp();
          showToast(`Income added: ${formatCurrency(newTx.amount)} from ${newTx.title}`, 'success');
          return {
            success: true,
            message: `Income '${newTx.title}' of ${formatCurrency(newTx.amount)} successfully credited.`,
            currentFinancials: getFinancials()
          };
        }

        case 'setMonthlyBudget': {
          state.user.monthlyBudget = Number(args.amount);
          persistState();
          renderApp();
          showToast(`Monthly budget updated to ${formatCurrency(state.user.monthlyBudget)}`, 'success');
          return {
            success: true,
            newBudget: state.user.monthlyBudget,
            currentFinancials: getFinancials()
          };
        }

        case 'getFinancialSummary': {
          return {
            success: true,
            summary: getFinancials(),
            currency: state.user.currency,
            totalTransactions: state.transactions.length
          };
        }

        case 'searchTransactions': {
          const q = (args.query || '').toLowerCase();
          const t = args.type || 'all';
          const c = (args.category || '').toLowerCase();

          const matches = state.transactions.filter(item => {
            const matchesQuery = !q || item.title.toLowerCase().includes(q) || item.category.toLowerCase().includes(q);
            const matchesType = t === 'all' || item.type === t;
            const matchesCategory = !c || item.category.toLowerCase() === c;
            return matchesQuery && matchesType && matchesCategory;
          });

          return {
            success: true,
            matchCount: matches.length,
            results: matches.slice(0, 5).map(m => ({
              id: m.id,
              title: m.title,
              amount: m.amount,
              type: m.type,
              category: m.category,
              date: m.date
            }))
          };
        }

        case 'deleteTransaction': {
          const idOrTitle = String(args.identifier).toLowerCase();
          const idx = state.transactions.findIndex(t => 
            t.id.toLowerCase() === idOrTitle || t.title.toLowerCase().includes(idOrTitle)
          );
          if (idx !== -1) {
            const removed = state.transactions.splice(idx, 1)[0];
            persistState();
            renderApp();
            showToast(`Deleted transaction: ${removed.title}`, 'info');
            return { success: true, deleted: removed };
          } else {
            return { success: false, error: `Could not find transaction matching "${args.identifier}"` };
          }
        }

        case 'navigateToPage': {
          state.currentPage = args.page;
          renderApp();
          return { success: true, navigatedTo: args.page };
        }

        case 'toggleTheme': {
          state.user.darkMode = args.mode === 'dark';
          applyTheme();
          persistState();
          renderApp();
          return { success: true, theme: state.user.darkMode ? 'dark' : 'light' };
        }

        default:
          return { success: false, error: `Unknown tool: ${name}` };
      }
    }

    // ==========================================
    // GEMINI 3.5 FLASH-LITE API CALLER
    // ==========================================
    async function sendPromptToGemini(userText) {
      state.aiMessages.push({
        role: 'user',
        text: userText,
        timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
      });
      state.aiThinking = true;
      renderApp();

      const apiKey = state.aiApiKey.trim();

      // If user has not yet entered an API key, fallback to local intelligent simulation agent
      if (!apiKey) {
        setTimeout(async () => {
          await runSimulationFallback(userText);
        }, 600);
        return;
      }

      try {
        const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3.5-flash-lite:generateContent?key=${apiKey}`;

        // Build conversation contents in Gemini REST format
        const contents = [
          {
            role: "user",
            parts: [{
              text: `You are SpendWise AI, an autonomous financial intelligence copilot in SpendWise personal finance app.
The current date is ${new Date().toLocaleDateString('en-GB', { day: 'numeric', month: 'long', year: 'numeric' })}.
The user currency is ${state.user.currency}.
You have direct tool access to manipulate transactions, adjust budgets, inspect financials, switch views, and toggle dark/light theme.
Always call tools when the user's intent is to perform an action or retrieve dynamic real-time data.
Keep responses concise, helpful, and fintech-focused.`
            }]
          }
        ];

        // Append recent chat turns
        state.aiMessages.slice(-6).forEach(m => {
          if (m.toolExec) return;
          contents.push({
            role: m.role === 'model' ? 'model' : 'user',
            parts: [{ text: m.text }]
          });
        });

        // Request 1: Send prompt + tool declarations
        const res = await fetch(url, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({
            contents,
            tools: [{ functionDeclarations: GEMINI_TOOLS_DECLARATION.function_declarations }],
            generationConfig: {
              temperature: 0.2,
              maxOutputTokens: 1024
            }
          })
        });

        if (!res.ok) {
          const errData = await res.json().catch(() => ({}));
          throw new Error(errData.error?.message || `HTTP ${res.status}: Failed to reach Gemini API`);
        }

        const data = await res.json();
        const candidate = data.candidates?.[0];
        const contentPart = candidate?.content?.parts?.[0];

        // Check if Gemini invoked a function/tool
        if (contentPart?.functionCall) {
          const { name, args } = contentPart.functionCall;
          
          // Render tool execution pill
          state.aiMessages.push({
            role: 'model',
            toolExec: { name, args },
            text: `⚡ Executing: ${name}(${JSON.stringify(args)})`,
            timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
          });
          renderApp();

          // Execute tool locally
          const toolResult = await executeAppTool(name, args);

          // Request 2: Send functionResponse back to Gemini for natural final answer
          const followUpContents = [
            ...contents,
            {
              role: 'model',
              parts: [{ functionCall: { name, args } }]
            },
            {
              role: 'function',
              parts: [{
                functionResponse: {
                  name,
                  response: toolResult
                }
              }]
            }
          ];

          const followUpRes = await fetch(url, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
              contents: followUpContents,
              tools: [{ functionDeclarations: GEMINI_TOOLS_DECLARATION.function_declarations }]
            })
          });

          if (followUpRes.ok) {
            const followUpData = await followUpRes.json();
            const finalReply = followUpData.candidates?.[0]?.content?.parts?.[0]?.text;
            state.aiMessages.push({
              role: 'model',
              text: finalReply || `Done! ${name} completed successfully.`,
              timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
            });
          } else {
            state.aiMessages.push({
              role: 'model',
              text: `Executed ${name} successfully!`,
              timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
            });
          }
        } else if (contentPart?.text) {
          state.aiMessages.push({
            role: 'model',
            text: contentPart.text,
            timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
          });
        }
      } catch (err) {
        console.error("Gemini Error:", err);
        state.aiMessages.push({
          role: 'model',
          isError: true,
          text: `⚠️ Gemini 3.5 API Error: ${err.message}. (Tip: Check your Google AI Studio API key in settings or use the simulation mode).`,
          timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
        });
      } finally {
        state.aiThinking = false;
        renderApp();
      }
    }

    // Local Simulation Fallback (runs if user hasn't added an AI Studio Key yet)
    async function runSimulationFallback(userText) {
      const lower = userText.toLowerCase();

      let reply = "";
      if (lower.includes("expense") || lower.includes("spent") || lower.includes("bought") || lower.includes("paid")) {
        const amtMatch = userText.match(/\d+(\.\d+)?/);
        const amt = amtMatch ? parseFloat(amtMatch[0]) : 250;
        let category = "Food";
        if (lower.includes("uber") || lower.includes("cab") || lower.includes("travel") || lower.includes("flight")) category = "Travel";
        else if (lower.includes("shop") || lower.includes("amazon") || lower.includes("clothes")) category = "Shopping";
        else if (lower.includes("bill") || lower.includes("wifi") || lower.includes("rent")) category = "Bills";

        await executeAppTool('addExpense', {
          title: userText.replace(/add|expense|spent|bought|paid|\d+|₹|\$/gi, '').trim() || "Quick Expense",
          amount: amt,
          category,
          paymentMethod: "UPI"
        });
        reply = `I have logged this expense of ${formatCurrency(amt)} under ${category}. Your available balance and budget progress have been updated. (Running in Simulation Mode — add your AI Studio API key for full Gemini 3.5 reasoning!)`;
      } else if (lower.includes("income") || lower.includes("salary") || lower.includes("received")) {
        const amtMatch = userText.match(/\d+(\.\d+)?/);
        const amt = amtMatch ? parseFloat(amtMatch[0]) : 15000;
        await executeAppTool('addIncome', {
          title: "Received Funds",
          amount: amt,
          category: "Salary",
          paymentMethod: "UPI"
        });
        reply = `Added income of ${formatCurrency(amt)}. Your balance has increased accordingly!`;
      } else if (lower.includes("budget") && (lower.includes("set") || lower.includes("change"))) {
        const amtMatch = userText.match(/\d+(\.\d+)?/);
        const amt = amtMatch ? parseFloat(amtMatch[0]) : 30000;
        await executeAppTool('setMonthlyBudget', { amount: amt });
        reply = `Monthly expense budget has been updated to ${formatCurrency(amt)}.`;
      } else if (lower.includes("analytics") || lower.includes("report") || lower.includes("chart")) {
        await executeAppTool('navigateToPage', { page: 'analytics' });
        reply = `Switched to the Analytics dashboard. You can inspect category breakdowns and cashflow trends.`;
      } else if (lower.includes("dark") || lower.includes("light") || lower.includes("theme")) {
        const mode = lower.includes("dark") ? 'dark' : 'light';
        await executeAppTool('toggleTheme', { mode });
        reply = `Theme switched to ${mode} mode.`;
      } else {
        const fin = getFinancials();
        reply = `Here is your quick summary: Available Balance: ${formatCurrency(fin.balance)} | Monthly Budget: ${formatCurrency(fin.budget)} (${fin.budgetUsedPercent}% used). Remaining: ${formatCurrency(fin.remainingBudget)}. How can I assist you next?`;
      }

      state.aiMessages.push({
        role: 'model',
        text: reply,
        timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
      });
      state.aiThinking = false;
      renderApp();
    }

    // ==========================================
    // UI COMPONENTS & TEMPLATES
    // ==========================================

    function renderNavbar() {
      if (!state.isLoggedIn) {
        return `
          <nav class="bg-white/80 dark:bg-[#131b2e]/80 backdrop-blur-md sticky top-0 z-30 border-b border-slate-200 dark:border-slate-800">
            <div class="max-w-7xl mx-auto px-6 h-20 flex items-center justify-between">
              <div class="flex items-center gap-3 cursor-pointer" onclick="navigateTo('landing')">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-indigo-600 to-violet-500 flex items-center justify-center text-white shadow-lg shadow-indigo-500/30">
                  <i data-lucide="wallet" class="w-5 h-5"></i>
                </div>
                <span class="text-xl font-bold tracking-tight bg-gradient-to-r from-indigo-600 to-violet-600 bg-clip-text text-transparent dark:from-indigo-400 dark:to-violet-400">SpendWise</span>
              </div>
              
              <div class="hidden md:flex items-center gap-8 text-sm font-semibold text-slate-600 dark:text-slate-300">
                <a href="#features" class="hover:text-indigo-600 dark:hover:text-indigo-400 transition">Features</a>
                <a href="#about" class="hover:text-indigo-600 dark:hover:text-indigo-400 transition">About</a>
                <a href="#copilot" class="hover:text-indigo-600 dark:hover:text-indigo-400 transition flex items-center gap-1.5 text-indigo-600 dark:text-indigo-400">
                  <span class="inline-block w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span> Gemini 3.5 AI
                </a>
              </div>

              <div class="flex items-center gap-3">
                <button onclick="toggleThemeGlobal()" class="p-2.5 rounded-xl border border-slate-200 dark:border-slate-800 text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 transition">
                  <i data-lucide="${state.user.darkMode ? 'sun' : 'moon'}" class="w-4 h-4"></i>
                </button>
                <button onclick="navigateTo('login')" class="px-5 py-2.5 rounded-xl text-sm font-semibold text-slate-700 dark:text-slate-200 hover:bg-slate-100 dark:hover:bg-slate-800 transition">Log In</button>
                <button onclick="navigateTo('signup')" class="px-5 py-2.5 rounded-xl text-sm font-semibold bg-indigo-600 hover:bg-indigo-700 text-white shadow-md shadow-indigo-600/20 transition">Get Started</button>
              </div>
            </div>
          </nav>
        `;
      }
      return '';
    }

    function renderLandingPage() {
      return `
        <div class="flex-1 overflow-y-auto custom-scrollbar">
          ${renderNavbar()}
          
          <!-- Hero Section -->
          <section class="max-w-7xl mx-auto px-6 pt-20 pb-28 text-center relative">
            <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-indigo-50 dark:bg-indigo-950/60 border border-indigo-200 dark:border-indigo-800 text-indigo-700 dark:text-indigo-300 text-xs font-bold uppercase tracking-wider mb-8">
              <i data-lucide="sparkles" class="w-3.5 h-3.5"></i>
              Powered by Google Gemini 3.5 Flash-Lite Agent
            </div>
            
            <h1 class="text-5xl md:text-7xl font-extrabold tracking-tight max-w-4xl mx-auto leading-[1.1] mb-6">
              Take Control of Your <br/>
              <span class="bg-gradient-to-r from-indigo-600 via-violet-600 to-pink-600 bg-clip-text text-transparent">Money with Intelligence</span>
            </h1>
            
            <p class="text-lg md:text-xl text-slate-600 dark:text-slate-400 max-w-2xl mx-auto mb-10 leading-relaxed">
              Track your income, expenses and monthly budget in one simple dashboard with an autonomous AI financial assistant that executes actions for you.
            </p>

            <div class="flex flex-col sm:flex-row items-center justify-center gap-4 max-w-md mx-auto mb-16">
              <button onclick="navigateTo('signup')" class="w-full sm:w-auto px-8 py-4 rounded-xl text-base font-bold bg-indigo-600 hover:bg-indigo-700 text-white shadow-xl shadow-indigo-600/25 transition transform hover:-translate-y-0.5">
                Get Started Free
              </button>
              <button onclick="navigateTo('login')" class="w-full sm:w-auto px-8 py-4 rounded-xl text-base font-bold border border-slate-300 dark:border-slate-700 hover:bg-slate-100 dark:hover:bg-slate-800 transition">
                Live Demo Login
              </button>
            </div>

            <!-- Dashboard Preview Glass Card -->
            <div class="relative max-w-5xl mx-auto rounded-3xl p-3 bg-gradient-to-b from-indigo-500/20 to-transparent border border-slate-200 dark:border-slate-800 shadow-2xl">
              <div class="rounded-2xl bg-white dark:bg-[#131b2e] p-6 text-left overflow-hidden border border-slate-100 dark:border-slate-800">
                <div class="flex items-center justify-between pb-6 border-b border-slate-100 dark:border-slate-800">
                  <div class="flex items-center gap-3">
                    <div class="w-3 h-3 rounded-full bg-rose-500"></div>
                    <div class="w-3 h-3 rounded-full bg-amber-500"></div>
                    <div class="w-3 h-3 rounded-full bg-emerald-500"></div>
                    <span class="ml-2 text-xs font-mono text-slate-400">spendwise.dashboard.io</span>
                  </div>
                  <span class="text-xs font-bold text-indigo-600 dark:text-indigo-400 bg-indigo-50 dark:bg-indigo-950/60 px-3 py-1 rounded-full">Autonomous AI Tools Active</span>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6 pt-6">
                  <div class="p-5 rounded-2xl bg-gradient-to-br from-indigo-600 to-violet-700 text-white shadow-lg">
                    <div class="text-xs uppercase font-medium tracking-wider text-indigo-200 mb-1">Available Balance</div>
                    <div class="text-3xl font-extrabold mb-3">₹24,580</div>
                    <div class="text-xs text-indigo-100 flex items-center justify-between pt-3 border-t border-white/20">
                      <span>In: ₹35,000</span>
                      <span>Out: ₹10,420</span>
                    </div>
                  </div>
                  <div class="p-5 rounded-2xl bg-slate-50 dark:bg-slate-800/60 border border-slate-200 dark:border-slate-800">
                    <div class="text-xs uppercase font-semibold text-slate-400 mb-1">Monthly Budget</div>
                    <div class="text-2xl font-bold text-slate-800 dark:text-slate-100 mb-2">65% Used</div>
                    <div class="w-full bg-slate-200 dark:bg-slate-700 h-2.5 rounded-full overflow-hidden">
                      <div class="bg-indigo-600 h-full rounded-full" style="width: 65%"></div>
                    </div>
                  </div>
                  <div class="p-5 rounded-2xl bg-slate-50 dark:bg-slate-800/60 border border-slate-200 dark:border-slate-800 flex flex-col justify-center">
                    <div class="flex items-center gap-2 text-indigo-600 dark:text-indigo-400 font-bold text-sm mb-1">
                      <i data-lucide="bot" class="w-4 h-4"></i> Gemini 3.5 Flash-Lite
                    </div>
                    <p class="text-xs text-slate-500 dark:text-slate-400 italic">"Added ₹450 for Starbucks and updated your weekly food analytics."</p>
                  </div>
                </div>
              </div>
            </div>
          </section>

          <!-- Feature Cards Section -->
          <section id="features" class="max-w-7xl mx-auto px-6 py-20 border-t border-slate-200 dark:border-slate-800">
            <div class="text-center max-w-2xl mx-auto mb-16">
              <h2 class="text-3xl font-extrabold mb-4">Complete Fintech Command Center</h2>
              <p class="text-slate-600 dark:text-slate-400">Everything you need to master your personal economy with zero friction.</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-4 gap-6">
              <div class="p-6 rounded-2xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800 hover:border-indigo-500/50 transition">
                <div class="w-12 h-12 rounded-xl bg-indigo-50 dark:bg-indigo-950/60 text-indigo-600 dark:text-indigo-400 flex items-center justify-center mb-5">
                  <i data-lucide="trending-down" class="w-6 h-6"></i>
                </div>
                <h3 class="text-lg font-bold mb-2">Track Expenses</h3>
                <p class="text-sm text-slate-500 dark:text-slate-400">Categorize transactions automatically with auto-captured time and editable notes.</p>
              </div>

              <div class="p-6 rounded-2xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800 hover:border-indigo-500/50 transition">
                <div class="w-12 h-12 rounded-xl bg-violet-50 dark:bg-violet-950/60 text-violet-600 dark:text-violet-400 flex items-center justify-center mb-5">
                  <i data-lucide="target" class="w-6 h-6"></i>
                </div>
                <h3 class="text-lg font-bold mb-2">Manage Budget</h3>
                <p class="text-sm text-slate-500 dark:text-slate-400">Dynamic 5-stage smart budget guardrails that caution before you overspend.</p>
              </div>

              <div class="p-6 rounded-2xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800 hover:border-indigo-500/50 transition">
                <div class="w-12 h-12 rounded-xl bg-emerald-50 dark:bg-emerald-950/60 text-emerald-600 dark:text-emerald-400 flex items-center justify-center mb-5">
                  <i data-lucide="pie-chart" class="w-6 h-6"></i>
                </div>
                <h3 class="text-lg font-bold mb-2">Analyze Spending</h3>
                <p class="text-sm text-slate-500 dark:text-slate-400">Interactive cashflow and category donut charts powered by responsive Chart.js.</p>
              </div>

              <div class="p-6 rounded-2xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800 hover:border-indigo-500/50 transition">
                <div class="w-12 h-12 rounded-xl bg-pink-50 dark:bg-pink-950/60 text-pink-600 dark:text-pink-400 flex items-center justify-center mb-5">
                  <i data-lucide="sparkles" class="w-6 h-6"></i>
                </div>
                <h3 class="text-lg font-bold mb-2">Gemini 3.5 Copilot</h3>
                <p class="text-sm text-slate-500 dark:text-slate-400">Autonomous tool calls to record, update, navigate, and audit with natural voice or text.</p>
              </div>
            </div>
          </section>

          <!-- Footer -->
          <footer class="border-t border-slate-200 dark:border-slate-800 py-12 bg-white dark:bg-[#0b0f19] text-center text-sm text-slate-500">
            <div class="max-w-7xl mx-auto px-6 flex flex-col md:flex-row items-center justify-between gap-4">
              <div class="flex items-center gap-2">
                <div class="w-6 h-6 rounded-lg bg-indigo-600 flex items-center justify-center text-white">
                  <i data-lucide="wallet" class="w-3.5 h-3.5"></i>
                </div>
                <span class="font-bold text-slate-800 dark:text-slate-200">SpendWise</span>
                <span>— Modern Personal Finance</span>
              </div>
              <p>© 2026 SpendWise Technologies Inc. Built with Google AI Studio & Gemini 3.5 Flash-Lite.</p>
            </div>
          </footer>
        </div>
      `;
    }

    function renderAuthPage(type = 'login') {
      const isLogin = type === 'login';
      return `
        <div class="flex-1 flex items-center justify-center p-6 overflow-y-auto">
          <div class="w-full max-w-md bg-white dark:bg-[#131b2e] rounded-3xl p-8 border border-slate-200 dark:border-slate-800 shadow-2xl">
            <div class="text-center mb-8">
              <div class="w-12 h-12 rounded-2xl bg-indigo-600 text-white flex items-center justify-center mx-auto mb-4 shadow-lg shadow-indigo-600/30">
                <i data-lucide="wallet" class="w-6 h-6"></i>
              </div>
              <h2 class="text-2xl font-extrabold">${isLogin ? 'Welcome back' : 'Create your account'}</h2>
              <p class="text-sm text-slate-500 dark:text-slate-400 mt-1">
                ${isLogin ? 'Enter your credentials to access your financial dashboard' : 'Join SpendWise to master your income and expenses'}
              </p>
            </div>

            <form id="auth-form" onsubmit="handleAuthSubmit(event, '${type}')" class="space-y-4">
              ${!isLogin ? `
                <div>
                  <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Full Name</label>
                  <input type="text" id="auth-name" required value="Alex Morgan" class="w-full px-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500">
                </div>
              ` : ''}

              <div>
                <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Email / Username</label>
                <input type="email" id="auth-email" required value="alex@spendwise.io" class="w-full px-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500">
              </div>

              <div>
                <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Password</label>
                <div class="relative">
                  <input type="password" id="auth-password" required value="password123" minlength="6" class="w-full px-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500">
                  <button type="button" onclick="togglePasswordVisibility('auth-password', this)" class="absolute right-3.5 top-3.5 text-slate-400 hover:text-slate-600">
                    <i data-lucide="eye" class="w-4 h-4"></i>
                  </button>
                </div>
              </div>

              ${!isLogin ? `
                <div>
                  <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Confirm Password</label>
                  <input type="password" id="auth-confirm" required value="password123" minlength="6" class="w-full px-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500">
                </div>
              ` : `
                <div class="flex items-center justify-between text-xs">
                  <label class="flex items-center gap-2 cursor-pointer text-slate-600 dark:text-slate-400">
                    <input type="checkbox" checked class="rounded border-slate-300 text-indigo-600 focus:ring-indigo-500"> Remember me
                  </label>
                  <a href="#" onclick="showToast('Password reset link sent to demo email', 'info')" class="text-indigo-600 dark:text-indigo-400 font-semibold hover:underline">Forgot password?</a>
                </div>
              `}

              <div id="auth-error" class="hidden text-xs text-rose-500 font-medium"></div>

              <button type="submit" class="w-full py-3.5 rounded-xl font-bold bg-indigo-600 hover:bg-indigo-700 text-white shadow-lg shadow-indigo-600/25 transition">
                ${isLogin ? 'Sign In to Dashboard' : 'Create SpendWise Account'}
              </button>
            </form>

            <div class="mt-6 text-center text-xs text-slate-500">
              ${isLogin ? `
                Don't have an account? <a href="#" onclick="navigateTo('signup')" class="text-indigo-600 dark:text-indigo-400 font-bold hover:underline">Sign up</a>
              ` : `
                Already registered? <a href="#" onclick="navigateTo('login')" class="text-indigo-600 dark:text-indigo-400 font-bold hover:underline">Log in</a>
              `}
            </div>
          </div>
        </div>
      `;
    }

    function renderSidebar() {
      const navItems = [
        { id: 'dashboard', label: 'Dashboard', icon: 'layout-dashboard' },
        { id: 'expenses', label: 'Expenses', icon: 'arrow-down-right', action: () => openModal('expense') },
        { id: 'income', label: 'Income', icon: 'arrow-up-right', action: () => openModal('income') },
        { id: 'analytics', label: 'Analytics', icon: 'bar-chart-3' },
        { id: 'budget', label: 'Budget', icon: 'target' },
        { id: 'transactions', label: 'Transactions', icon: 'receipt' },
        { id: 'settings', label: 'Settings', icon: 'settings' }
      ];

      return `
        <aside class="hidden lg:flex flex-col w-64 border-r border-slate-200 dark:border-slate-800 bg-white dark:bg-[#131b2e] p-5 justify-between select-none">
          <div>
            <!-- Brand -->
            <div class="flex items-center gap-3 px-3 py-2 mb-8 cursor-pointer" onclick="navigateTo('dashboard')">
              <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-indigo-600 to-violet-500 flex items-center justify-center text-white shadow-lg shadow-indigo-500/25">
                <i data-lucide="wallet" class="w-5 h-5"></i>
              </div>
              <div>
                <span class="text-lg font-bold tracking-tight bg-gradient-to-r from-indigo-600 to-violet-600 bg-clip-text text-transparent dark:from-indigo-400 dark:to-violet-400">SpendWise</span>
                <span class="block text-[10px] uppercase font-bold tracking-widest text-slate-400">Fintech Suite</span>
              </div>
            </div>

            <!-- Navigation Links -->
            <nav class="space-y-1.5">
              ${navItems.map(item => {
                const active = state.currentPage === item.id;
                return `
                  <button onclick="${item.action ? `(${item.action.toString()})()` : `navigateTo('${item.id}')`}" 
                    class="w-full flex items-center gap-3.5 px-4 py-3 rounded-xl text-sm font-semibold transition ${
                      active 
                        ? 'bg-indigo-50 dark:bg-indigo-950/60 text-indigo-600 dark:text-indigo-400 border border-indigo-200/50 dark:border-indigo-800/50' 
                        : 'text-slate-600 dark:text-slate-400 hover:bg-slate-100 dark:hover:bg-slate-800/60'
                    }">
                    <i data-lucide="${item.icon}" class="w-4 h-4"></i>
                    <span>${item.label}</span>
                  </button>
                `;
              }).join('')}
            </nav>
          </div>

          <!-- Bottom Profile / AI Studio Key status -->
          <div class="pt-6 border-t border-slate-100 dark:border-slate-800 space-y-3">
            <div onclick="openModal('aiKey')" class="cursor-pointer p-3 rounded-xl bg-indigo-50 dark:bg-indigo-950/40 border border-indigo-200/60 dark:border-indigo-900/60 flex items-center gap-3">
              <div class="w-8 h-8 rounded-lg bg-indigo-600 text-white flex items-center justify-center">
                <i data-lucide="sparkles" class="w-4 h-4"></i>
              </div>
              <div class="flex-1 overflow-hidden">
                <div class="text-xs font-bold text-indigo-700 dark:text-indigo-300">Gemini 3.5 API</div>
                <div class="text-[11px] text-slate-500 truncate">${state.aiApiKey ? '● Connected' : '○ Click to configure'}</div>
              </div>
            </div>

            <div class="flex items-center justify-between px-2">
              <div class="flex items-center gap-3">
                <div class="w-9 h-9 rounded-full bg-slate-200 dark:bg-slate-700 flex items-center justify-center font-bold text-xs">
                  ${state.user.name.split(' ').map(n=>n[0]).join('')}
                </div>
                <div class="text-left">
                  <div class="text-xs font-bold truncate max-w-[100px]">${state.user.name}</div>
                  <div class="text-[10px] text-slate-400">Pro Plan</div>
                </div>
              </div>
              <button onclick="handleLogout()" title="Logout" class="p-2 text-slate-400 hover:text-rose-500 rounded-lg transition">
                <i data-lucide="log-out" class="w-4 h-4"></i>
              </button>
            </div>
          </div>
        </aside>
      `;
    }

    function renderMobileNavbar() {
      return `
        <div class="lg:hidden fixed bottom-0 left-0 right-0 z-40 bg-white/95 dark:bg-[#131b2e]/95 backdrop-blur-md border-t border-slate-200 dark:border-slate-800 px-4 py-2 flex items-center justify-around">
          <button onclick="navigateTo('dashboard')" class="flex flex-col items-center p-2 text-xs font-medium ${state.currentPage === 'dashboard' ? 'text-indigo-600 dark:text-indigo-400' : 'text-slate-500'}">
            <i data-lucide="home" class="w-5 h-5"></i>
            <span class="text-[10px] mt-1">Home</span>
          </button>
          <button onclick="navigateTo('analytics')" class="flex flex-col items-center p-2 text-xs font-medium ${state.currentPage === 'analytics' ? 'text-indigo-600 dark:text-indigo-400' : 'text-slate-500'}">
            <i data-lucide="pie-chart" class="w-5 h-5"></i>
            <span class="text-[10px] mt-1">Analytics</span>
          </button>
          <button onclick="openModal('expense')" class="flex items-center justify-center w-12 h-12 -mt-6 rounded-full bg-indigo-600 text-white shadow-xl shadow-indigo-600/40">
            <i data-lucide="plus" class="w-6 h-6"></i>
          </button>
          <button onclick="navigateTo('transactions')" class="flex flex-col items-center p-2 text-xs font-medium ${state.currentPage === 'transactions' ? 'text-indigo-600 dark:text-indigo-400' : 'text-slate-500'}">
            <i data-lucide="receipt" class="w-5 h-5"></i>
            <span class="text-[10px] mt-1">Transactions</span>
          </button>
          <button onclick="navigateTo('settings')" class="flex flex-col items-center p-2 text-xs font-medium ${state.currentPage === 'settings' ? 'text-indigo-600 dark:text-indigo-400' : 'text-slate-500'}">
            <i data-lucide="user" class="w-5 h-5"></i>
            <span class="text-[10px] mt-1">Profile</span>
          </button>
        </div>
      `;
    }

    function renderDashboardHeader() {
      const dateStr = new Date().toLocaleDateString('en-GB', {
        weekday: 'long',
        day: 'numeric',
        month: 'short',
        year: 'numeric'
      });

      return `
        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 mb-8">
          <div>
            <h1 class="text-2xl sm:text-3xl font-extrabold tracking-tight">Good Morning, ${state.user.name.split(' ')[0]} 👋</h1>
            <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400 mt-1 flex items-center gap-1.5">
              <i data-lucide="calendar" class="w-3.5 h-3.5"></i> ${dateStr}
            </p>
          </div>

          <div class="flex items-center gap-2.5">
            <button onclick="toggleThemeGlobal()" class="p-2.5 rounded-xl border border-slate-200 dark:border-slate-800 text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 transition">
              <i data-lucide="${state.user.darkMode ? 'sun' : 'moon'}" class="w-4 h-4"></i>
            </button>
            <button onclick="toggleAIChat()" class="px-4 py-2.5 rounded-xl text-xs font-bold bg-indigo-50 dark:bg-indigo-950/60 text-indigo-600 dark:text-indigo-400 border border-indigo-200 dark:border-indigo-800 flex items-center gap-2 hover:bg-indigo-100 transition">
              <i data-lucide="sparkles" class="w-4 h-4"></i> SpendWise AI
            </button>
          </div>
        </div>
      `;
    }

    function renderDashboardView() {
      const fin = getFinancials();

      return `
        <div class="space-y-8">
          <!-- Main Balance Card & Quick Stats Grid -->
          <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <!-- Balance Card -->
            <div class="md:col-span-2 p-8 rounded-3xl bg-gradient-to-tr from-indigo-700 via-indigo-600 to-violet-600 text-white shadow-xl shadow-indigo-600/20 relative overflow-hidden">
              <div class="absolute -right-8 -bottom-8 w-44 h-44 rounded-full bg-white/10 blur-2xl pointer-events-none"></div>
              
              <div class="flex items-center justify-between mb-4">
                <span class="text-xs uppercase font-extrabold tracking-wider text-indigo-200">AVAILABLE BALANCE</span>
                <span class="px-3 py-1 rounded-full bg-white/15 text-xs backdrop-blur-sm font-semibold">Active Vault</span>
              </div>

              <div class="text-4xl sm:text-5xl font-black tracking-tight mb-8">${formatCurrency(fin.balance)}</div>

              <div class="grid grid-cols-2 gap-4 pt-6 border-t border-white/20">
                <div>
                  <div class="text-xs text-indigo-200 flex items-center gap-1.5 mb-1">
                    <i data-lucide="arrow-up-circle" class="w-3.5 h-3.5 text-emerald-300"></i> Total Income
                  </div>
                  <div class="text-xl font-bold">${formatCurrency(fin.income)}</div>
                </div>
                <div>
                  <div class="text-xs text-indigo-200 flex items-center gap-1.5 mb-1">
                    <i data-lucide="arrow-down-circle" class="w-3.5 h-3.5 text-rose-300"></i> Total Expenses
                  </div>
                  <div class="text-xl font-bold">${formatCurrency(fin.expenses)}</div>
                </div>
              </div>
            </div>

            <!-- Monthly Budget Card -->
            <div class="p-6 rounded-3xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800 flex flex-col justify-between shadow-sm">
              <div>
                <div class="flex items-center justify-between mb-2">
                  <span class="text-xs uppercase font-extrabold tracking-wider text-slate-400">MONTHLY BUDGET</span>
                  <button onclick="openModal('budget')" class="text-xs text-indigo-600 dark:text-indigo-400 font-bold hover:underline">Edit</button>
                </div>
                <div class="text-2xl font-black mb-1">${formatCurrency(fin.budget)}</div>
                <div class="text-xs text-slate-500 mb-6">
                  Spent: <span class="font-bold text-slate-700 dark:text-slate-300">${formatCurrency(fin.expenses)}</span> | 
                  Remaining: <span class="font-bold ${fin.remainingBudget < 0 ? 'text-rose-500' : 'text-emerald-500'}">${formatCurrency(fin.remainingBudget)}</span>
                </div>

                <div class="space-y-2 mb-4">
                  <div class="flex justify-between text-xs font-bold">
                    <span>Budget Used</span>
                    <span class="${Number(fin.budgetUsedPercent) > 100 ? 'text-rose-500 font-extrabold' : ''}">${fin.budgetUsedPercent}%</span>
                  </div>
                  <div class="w-full bg-slate-100 dark:bg-slate-800 h-3 rounded-full overflow-hidden">
                    <div class="h-full rounded-full transition-all duration-500 ${
                      Number(fin.budgetUsedPercent) > 90 ? 'bg-rose-500' : Number(fin.budgetUsedPercent) >= 75 ? 'bg-amber-500' : 'bg-indigo-600'
                    }" style="width: ${Math.min(Number(fin.budgetUsedPercent), 100)}%"></div>
                  </div>
                </div>
              </div>

              <!-- Informational Suggestion -->
              <div class="p-3.5 rounded-2xl text-xs flex items-start gap-2.5 ${
                fin.suggestionLevel === 'danger' ? 'bg-rose-50 dark:bg-rose-950/40 text-rose-700 dark:text-rose-300 border border-rose-200/50 dark:border-rose-900/50' :
                fin.suggestionLevel === 'warning' ? 'bg-amber-50 dark:bg-amber-950/40 text-amber-700 dark:text-amber-300 border border-amber-200/50 dark:border-amber-900/50' :
                'bg-indigo-50 dark:bg-indigo-950/40 text-indigo-700 dark:text-indigo-300 border border-indigo-200/50 dark:border-indigo-900/50'
              }">
                <i data-lucide="lightbulb" class="w-4 h-4 shrink-0 mt-0.5"></i>
                <p class="leading-relaxed">${fin.suggestion}</p>
              </div>
            </div>
          </div>

          <!-- Quick Action Buttons -->
          <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
            <button onclick="openModal('expense')" class="p-4 rounded-2xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800 hover:border-rose-500/50 transition flex items-center gap-4 group text-left shadow-sm">
              <div class="w-12 h-12 rounded-xl bg-rose-50 dark:bg-rose-950/50 text-rose-600 flex items-center justify-center group-hover:scale-105 transition">
                <i data-lucide="minus-circle" class="w-6 h-6"></i>
              </div>
              <div>
                <div class="font-bold text-sm">Add Expense</div>
                <div class="text-xs text-slate-400">Record a new purchase</div>
              </div>
            </button>

            <button onclick="openModal('income')" class="p-4 rounded-2xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800 hover:border-emerald-500/50 transition flex items-center gap-4 group text-left shadow-sm">
              <div class="w-12 h-12 rounded-xl bg-emerald-50 dark:bg-emerald-950/50 text-emerald-600 flex items-center justify-center group-hover:scale-105 transition">
                <i data-lucide="plus-circle" class="w-6 h-6"></i>
              </div>
              <div>
                <div class="font-bold text-sm">Add Income</div>
                <div class="text-xs text-slate-400">Deposit or salary credit</div>
              </div>
            </button>

            <button onclick="openModal('budget')" class="p-4 rounded-2xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800 hover:border-indigo-500/50 transition flex items-center gap-4 group text-left shadow-sm">
              <div class="w-12 h-12 rounded-xl bg-indigo-50 dark:bg-indigo-950/50 text-indigo-600 flex items-center justify-center group-hover:scale-105 transition">
                <i data-lucide="sliders" class="w-6 h-6"></i>
              </div>
              <div>
                <div class="font-bold text-sm">Set Budget</div>
                <div class="text-xs text-slate-400">Configure monthly targets</div>
              </div>
            </button>
          </div>

          <!-- Recent Transactions Card -->
          <div class="p-6 rounded-3xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800 shadow-sm">
            <div class="flex items-center justify-between mb-6">
              <h3 class="text-lg font-bold">Recent Transactions</h3>
              <button onclick="navigateTo('transactions')" class="text-xs font-bold text-indigo-600 dark:text-indigo-400 hover:underline flex items-center gap-1">
                View All Transactions <i data-lucide="chevron-right" class="w-3.5 h-3.5"></i>
              </button>
            </div>

            ${renderTransactionList(state.transactions.slice(0, 5))}
          </div>
        </div>
      `;
    }

    function renderTransactionList(items) {
      if (items.length === 0) {
        return `
          <div class="py-12 text-center">
            <div class="w-12 h-12 rounded-full bg-slate-100 dark:bg-slate-800 text-slate-400 flex items-center justify-center mx-auto mb-3">
              <i data-lucide="receipt" class="w-6 h-6"></i>
            </div>
            <h4 class="text-base font-bold text-slate-700 dark:text-slate-300">Your money story starts here.</h4>
            <p class="text-xs text-slate-400 mt-1 max-w-sm mx-auto mb-4">Add your first income or expense to start tracking with live intelligence.</p>
            <button onclick="openModal('expense')" class="px-5 py-2.5 rounded-xl bg-indigo-600 text-white text-xs font-bold shadow-md shadow-indigo-600/20">
              + Add Transaction
            </button>
          </div>
        `;
      }

      const categoryIcons = {
        Food: 'utensils',
        Travel: 'train',
        Shopping: 'shopping-bag',
        Education: 'book-open',
        Bills: 'zap',
        Entertainment: 'film',
        Health: 'activity',
        Salary: 'briefcase',
        Other: 'dollar-sign'
      };

      return `
        <div class="divide-y divide-slate-100 dark:divide-slate-800">
          ${items.map(tx => {
            const isExp = tx.type === 'expense';
            const icon = categoryIcons[tx.category] || 'dollar-sign';

            return `
              <div class="py-4 flex items-center justify-between gap-4 hover:bg-slate-50/50 dark:hover:bg-slate-800/30 px-3 rounded-xl transition">
                <div class="flex items-center gap-3.5 min-w-0">
                  <div class="w-11 h-11 rounded-2xl flex items-center justify-center shrink-0 ${
                    isExp ? 'bg-rose-50 dark:bg-rose-950/40 text-rose-500' : 'bg-emerald-50 dark:bg-emerald-950/40 text-emerald-500'
                  }">
                    <i data-lucide="${icon}" class="w-5 h-5"></i>
                  </div>
                  <div class="min-w-0">
                    <div class="text-sm font-bold truncate text-slate-800 dark:text-slate-200">${tx.title}</div>
                    <div class="text-xs text-slate-400 flex items-center gap-2 mt-0.5">
                      <span>${tx.date} •${tx.time}</span>
                      <span>•</span>
                      <span class="px-2 py-0.5 rounded-md bg-slate-100 dark:bg-slate-800 text-[10px] font-medium">${tx.paymentMethod}</span>
                    </div>
                  </div>
                </div>

                <div class="flex items-center gap-4 shrink-0">
                  <div class="text-right">
                    <div class="text-sm sm:text-base font-extrabold ${isExp ? 'text-rose-500' : 'text-emerald-500'}">
                      ${isExp ? '-' : '+'}${formatCurrency(tx.amount)}
                    </div>
                    <div class="text-[10px] text-slate-400 uppercase font-semibold">${tx.category}</div>
                  </div>

                  <!-- Actions Dropdown / Menu -->
                  <div class="relative group">
                    <button class="p-2 text-slate-400 hover:text-slate-600 dark:hover:text-slate-200 rounded-lg">
                      <i data-lucide="more-vertical" class="w-4 h-4"></i>
                    </button>
                    <div class="absolute right-0 top-full mt-1 hidden group-hover:block w-32 bg-white dark:bg-[#1a233b] border border-slate-200 dark:border-slate-700 rounded-xl shadow-xl z-20 py-1">
                      <button onclick="editTransactionModal('${tx.id}')" class="w-full text-left px-3 py-2 text-xs font-semibold hover:bg-slate-100 dark:hover:bg-slate-700 flex items-center gap-2">
                        <i data-lucide="edit-3" class="w-3.5 h-3.5"></i> Edit
                      </button>
                      <button onclick="confirmDeleteTransaction('${tx.id}')" class="w-full text-left px-3 py-2 text-xs font-semibold text-rose-500 hover:bg-rose-50 dark:hover:bg-rose-950/40 flex items-center gap-2">
                        <i data-lucide="trash-2" class="w-3.5 h-3.5"></i> Delete
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            `;
          }).join('')}
        </div>
      `;
    }

    function renderTransactionsPage() {
      // Apply filters and sorting
      let list = [...state.transactions];

      if (state.filterType !== 'all') {
        list = list.filter(t => t.type === state.filterType);
      }
      if (state.filterCategory !== 'all') {
        list = list.filter(t => t.category.toLowerCase() === state.filterCategory.toLowerCase());
      }
      if (state.searchQuery.trim()) {
        const q = state.searchQuery.toLowerCase();
        list = list.filter(t => t.title.toLowerCase().includes(q) || t.note?.toLowerCase().includes(q));
      }

      if (state.sortField === 'date-desc') {
        list.sort((a,b) => new Date(b.date + ' ' + b.time) - new Date(a.date + ' ' + a.time));
      } else if (state.sortField === 'date-asc') {
        list.sort((a,b) => new Date(a.date + ' ' + a.time) - new Date(b.date + ' ' + b.time));
      } else if (state.sortField === 'amount-desc') {
        list.sort((a,b) => b.amount - a.amount);
      } else if (state.sortField === 'amount-asc') {
        list.sort((a,b) => a.amount - b.amount);
      }

      return `
        <div class="space-y-6">
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div>
              <h2 class="text-2xl font-extrabold">Transaction History</h2>
              <p class="text-xs text-slate-400">Search, filter, edit, or export your financial records.</p>
            </div>
            <div class="flex items-center gap-2">
              <button onclick="exportCSV()" class="px-4 py-2 rounded-xl border border-slate-200 dark:border-slate-800 text-xs font-bold hover:bg-slate-100 dark:hover:bg-slate-800 transition flex items-center gap-1.5">
                <i data-lucide="download" class="w-3.5 h-3.5"></i> Export CSV
              </button>
              <button onclick="openModal('expense')" class="px-4 py-2 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white text-xs font-bold transition flex items-center gap-1.5 shadow-md shadow-indigo-600/20">
                <i data-lucide="plus" class="w-3.5 h-3.5"></i> New Entry
              </button>
            </div>
          </div>

          <!-- Search & Filter Controls -->
          <div class="p-4 rounded-2xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 gap-3">
            <div class="relative">
              <i data-lucide="search" class="w-4 h-4 text-slate-400 absolute left-3 top-3"></i>
              <input type="text" placeholder="Search transactions..." value="${state.searchQuery}" oninput="state.searchQuery = this.value; renderApp();" class="w-full pl-9 pr-4 py-2 rounded-xl bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-xs focus:outline-none focus:ring-2 focus:ring-indigo-500">
            </div>

            <select onchange="state.filterType = this.value; renderApp();" class="px-3 py-2 rounded-xl bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-xs font-medium focus:outline-none focus:ring-2 focus:ring-indigo-500">
              <option value="all" ${state.filterType === 'all' ? 'selected' : ''}>All Types (In & Out)</option>
              <option value="income" ${state.filterType === 'income' ? 'selected' : ''}>Income Only</option>
              <option value="expense" ${state.filterType === 'expense' ? 'selected' : ''}>Expenses Only</option>
            </select>

            <select onchange="state.filterCategory = this.value; renderApp();" class="px-3 py-2 rounded-xl bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-xs font-medium focus:outline-none focus:ring-2 focus:ring-indigo-500">
              <option value="all" ${state.filterCategory === 'all' ? 'selected' : ''}>All Categories</option>
              <option value="food">Food</option>
              <option value="travel">Travel</option>
              <option value="shopping">Shopping</option>
              <option value="education">Education</option>
              <option value="bills">Bills</option>
              <option value="entertainment">Entertainment</option>
              <option value="health">Health</option>
              <option value="salary">Salary</option>
              <option value="other">Other</option>
            </select>

            <select onchange="state.sortField = this.value; renderApp();" class="px-3 py-2 rounded-xl bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-xs font-medium focus:outline-none focus:ring-2 focus:ring-indigo-500">
              <option value="date-desc" ${state.sortField === 'date-desc' ? 'selected' : ''}>Newest First</option>
              <option value="date-asc" ${state.sortField === 'date-asc' ? 'selected' : ''}>Oldest First</option>
              <option value="amount-desc" ${state.sortField === 'amount-desc' ? 'selected' : ''}>Highest Amount</option>
              <option value="amount-asc" ${state.sortField === 'amount-asc' ? 'selected' : ''}>Lowest Amount</option>
            </select>
          </div>

          <!-- Transaction List -->
          <div class="p-6 rounded-3xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800 shadow-sm">
            ${renderTransactionList(list)}
          </div>
        </div>
      `;
    }

    function renderAnalyticsPage() {
      const fin = getFinancials();

      // Aggregate category totals
      const categoryTotals = {};
      state.transactions
        .filter(t => t.type === 'expense')
        .forEach(t => {
          categoryTotals[t.category] = (categoryTotals[t.category] || 0) + Number(t.amount);
        });

      const categoriesSorted = Object.entries(categoryTotals).sort((a,b) => b[1] - a[1]);

      return `
        <div class="space-y-6">
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div>
              <h2 class="text-2xl font-extrabold">Financial Analytics</h2>
              <p class="text-xs text-slate-400">Deep insights into cashflow distribution and budget efficiency.</p>
            </div>
            <div class="inline-flex rounded-xl bg-slate-100 dark:bg-slate-800 p-1 text-xs font-semibold">
              <button class="px-3 py-1.5 rounded-lg bg-white dark:bg-slate-700 shadow-sm">This Month</button>
              <button class="px-3 py-1.5 rounded-lg text-slate-500 hover:text-slate-800 dark:hover:text-slate-200">Weekly</button>
              <button class="px-3 py-1.5 rounded-lg text-slate-500 hover:text-slate-800 dark:hover:text-slate-200">Annual</button>
            </div>
          </div>

          <!-- Charts Grid -->
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <!-- Inflow vs Outflow Chart -->
            <div class="p-6 rounded-3xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800">
              <h3 class="text-base font-bold mb-1">Income vs Expense</h3>
              <p class="text-xs text-slate-400 mb-6">Net financial flow comparison</p>
              <div class="h-64 relative flex items-center justify-center">
                <canvas id="chart-flow"></canvas>
              </div>
            </div>

            <!-- Category Expense Distribution -->
            <div class="p-6 rounded-3xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800">
              <h3 class="text-base font-bold mb-1">Category Breakdown</h3>
              <p class="text-xs text-slate-400 mb-6">Where your money went this cycle</p>
              <div class="h-64 relative flex items-center justify-center">
                <canvas id="chart-categories"></canvas>
              </div>
            </div>
          </div>

          <!-- Category Expense Cards Grid -->
          <div class="p-6 rounded-3xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800">
            <h3 class="text-base font-bold mb-4">Ranked Expense Categories</h3>
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-4">
              ${categoriesSorted.length ? categoriesSorted.map(([cat, amt]) => `
                <div class="p-4 rounded-2xl bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-800">
                  <div class="text-xs font-semibold text-slate-400 uppercase tracking-wider mb-1">${cat}</div>
                  <div class="text-lg font-black">${formatCurrency(amt)}</div>
                  <div class="text-[11px] text-indigo-600 dark:text-indigo-400 mt-1">
                    ${fin.expenses ? ((amt / fin.expenses) * 100).toFixed(0) : 0}% of total
                  </div>
                </div>
              `).join('') : '<div class="text-xs text-slate-400 col-span-4 py-4 text-center">No expense categories registered yet.</div>'}
            </div>
          </div>
        </div>
      `;
    }

    function renderBudgetPage() {
      const fin = getFinancials();

      return `
        <div class="max-w-4xl mx-auto space-y-6">
          <div>
            <h2 class="text-2xl font-extrabold">Monthly Expense Budget</h2>
            <p class="text-xs text-slate-400">Establish proactive guardrails to ensure sustainable wealth building.</p>
          </div>

          <div class="p-8 rounded-3xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800 shadow-sm space-y-6">
            <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 pb-6 border-b border-slate-100 dark:border-slate-800">
              <div>
                <span class="text-xs font-extrabold tracking-wider text-slate-400 uppercase">Current Limit</span>
                <div class="text-4xl font-black mt-1">${formatCurrency(fin.budget)}</div>
              </div>
              <button onclick="openModal('budget')" class="px-5 py-2.5 rounded-xl bg-indigo-600 text-white text-xs font-bold hover:bg-indigo-700 transition">
                Modify Budget Limit
              </button>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
              <div class="p-4 rounded-2xl bg-slate-50 dark:bg-slate-900">
                <div class="text-xs text-slate-400 uppercase font-bold">Spent So Far</div>
                <div class="text-2xl font-extrabold mt-1 text-slate-800 dark:text-slate-100">${formatCurrency(fin.expenses)}</div>
              </div>
              <div class="p-4 rounded-2xl bg-slate-50 dark:bg-slate-900">
                <div class="text-xs text-slate-400 uppercase font-bold">Remaining</div>
                <div class="text-2xl font-extrabold mt-1 ${fin.remainingBudget < 0 ? 'text-rose-500' : 'text-emerald-500'}">
                  ${formatCurrency(fin.remainingBudget)}
                </div>
              </div>
              <div class="p-4 rounded-2xl bg-slate-50 dark:bg-slate-900">
                <div class="text-xs text-slate-400 uppercase font-bold">Budget Consumed</div>
                <div class="text-2xl font-extrabold mt-1 ${Number(fin.budgetUsedPercent) > 90 ? 'text-rose-500' : 'text-indigo-600 dark:text-indigo-400'}">
                  ${fin.budgetUsedPercent}%
                </div>
              </div>
            </div>

            <!-- Progress Bar -->
            <div class="space-y-2 pt-2">
              <div class="w-full bg-slate-100 dark:bg-slate-800 h-4 rounded-full overflow-hidden p-0.5">
                <div class="h-full rounded-full transition-all duration-700 ${
                  Number(fin.budgetUsedPercent) > 90 ? 'bg-rose-500' : Number(fin.budgetUsedPercent) >= 75 ? 'bg-amber-500' : 'bg-indigo-600'
                }" style="width: ${Math.min(Number(fin.budgetUsedPercent), 100)}%"></div>
              </div>
              <div class="flex justify-between text-[11px] text-slate-400 font-medium">
                <span>0% Safe</span>
                <span>50% Caution</span>
                <span>75% Warning</span>
                <span>100% Exceeded</span>
              </div>
            </div>

            <!-- Informational Suggestion Banner -->
            <div class="p-5 rounded-2xl ${
              fin.suggestionLevel === 'danger' ? 'bg-rose-50 dark:bg-rose-950/40 text-rose-700 dark:text-rose-300 border border-rose-200 dark:border-rose-900' :
              fin.suggestionLevel === 'warning' ? 'bg-amber-50 dark:bg-amber-950/40 text-amber-700 dark:text-amber-300 border border-amber-200 dark:border-amber-900' :
              'bg-indigo-50 dark:bg-indigo-950/40 text-indigo-700 dark:text-indigo-300 border border-indigo-200 dark:border-indigo-900'
            } flex items-center gap-3">
              <i data-lucide="info" class="w-5 h-5 shrink-0"></i>
              <div class="text-xs font-semibold leading-relaxed">${fin.suggestion}</div>
            </div>
          </div>
        </div>
      `;
    }

    function renderSettingsPage() {
      return `
        <div class="max-w-3xl mx-auto space-y-6">
          <div>
            <h2 class="text-2xl font-extrabold">Preferences & Profile</h2>
            <p class="text-xs text-slate-400">Configure your account, AI keys, and display parameters.</p>
          </div>

          <div class="p-6 rounded-3xl bg-white dark:bg-[#131b2e] border border-slate-200 dark:border-slate-800 space-y-6">
            <!-- Profile Info -->
            <div class="flex items-center gap-4 pb-6 border-b border-slate-100 dark:border-slate-800">
              <div class="w-16 h-16 rounded-2xl bg-indigo-600 text-white flex items-center justify-center font-bold text-xl">
                ${state.user.name.split(' ').map(n=>n[0]).join('')}
              </div>
              <div>
                <h3 class="text-base font-bold">${state.user.name}</h3>
                <p class="text-xs text-slate-400">${state.user.email}</p>
                <span class="inline-block mt-1 px-2.5 py-0.5 rounded-full bg-indigo-50 dark:bg-indigo-950 text-[10px] font-bold text-indigo-600 dark:text-indigo-400">LocalStorage Encrypted Tier</span>
              </div>
            </div>

            <!-- AI Studio API Key Setting -->
            <div class="space-y-2 pb-6 border-b border-slate-100 dark:border-slate-800">
              <div class="flex items-center justify-between">
                <div>
                  <div class="text-xs font-bold uppercase tracking-wider text-slate-500">Google AI Studio API Key</div>
                  <div class="text-xs text-slate-400">Powers Gemini 3.5 Flash-Lite Copilot and autonomous app tools</div>
                </div>
                <a href="https://aistudio.google.com/app/apikey" target="_blank" class="text-xs font-bold text-indigo-600 dark:text-indigo-400 hover:underline">Get Free Key ↗</a>
              </div>
              <div class="flex gap-2">
                <input type="password" id="settings-api-key" placeholder="AIzaSy..." value="${state.aiApiKey}" class="flex-1 px-4 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-xs font-mono">
                <button onclick="saveApiKeyFromSettings()" class="px-5 py-2.5 rounded-xl bg-indigo-600 text-white font-bold text-xs hover:bg-indigo-700 transition">Save Key</button>
              </div>
            </div>

            <!-- Currency & Budget Form -->
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 pb-6 border-b border-slate-100 dark:border-slate-800">
              <div>
                <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Currency Symbol</label>
                <select id="settings-currency" onchange="state.user.currency = this.value; persistState(); renderApp();" class="w-full px-4 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-xs font-medium">
                  <option value="₹" ${state.user.currency === '₹' ? 'selected' : ''}>₹ (INR - Indian Rupee)</option>
                  <option value="$" ${state.user.currency === '$' ? 'selected' : ''}>$ (USD - US Dollar)</option>
                  <option value="€" ${state.user.currency === '€' ? 'selected' : ''}>€ (EUR - Euro)</option>
                  <option value="£" ${state.user.currency === '£' ? 'selected' : ''}>£ (GBP - British Pound)</option>
                  <option value="AED " ${state.user.currency === 'AED ' ? 'selected' : ''}>AED (UAE Dirham)</option>
                </select>
              </div>

              <div>
                <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Monthly Budget Target</label>
                <input type="number" id="settings-budget" value="${state.user.monthlyBudget}" onchange="state.user.monthlyBudget = Number(this.value); persistState(); renderApp();" class="w-full px-4 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-xs">
              </div>
            </div>

            <!-- Appearance Toggle -->
            <div class="flex items-center justify-between pb-6 border-b border-slate-100 dark:border-slate-800">
              <div>
                <div class="text-sm font-bold">Dark Appearance</div>
                <div class="text-xs text-slate-400">Switch between deep dark and crisp light fintech themes</div>
              </div>
              <button onclick="toggleThemeGlobal()" class="p-2.5 rounded-xl border border-slate-200 dark:border-slate-700">
                <i data-lucide="${state.user.darkMode ? 'sun' : 'moon'}" class="w-5 h-5 text-indigo-500"></i>
              </button>
            </div>

            <!-- Logout -->
            <div class="pt-2 flex justify-end">
              <button onclick="handleLogout()" class="px-5 py-2.5 rounded-xl border border-rose-200 dark:border-rose-900 text-rose-500 text-xs font-bold hover:bg-rose-50 dark:hover:bg-rose-950/40 transition">
                Sign Out of SpendWise
              </button>
            </div>
          </div>
        </div>
      `;
    }

    // ==========================================
    // MODALS: ADD EXPENSE, INCOME, BUDGET & API
    // ==========================================
    function renderModals() {
      if (!state.activeModal) return '';

      const now = new Date();
      const defaultDate = now.toISOString().split('T')[0];
      const defaultTime = now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });

      if (state.activeModal === 'expense') {
        return `
          <div class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4">
            <div class="w-full max-w-lg bg-white dark:bg-[#131b2e] rounded-3xl p-6 sm:p-8 border border-slate-200 dark:border-slate-800 shadow-2xl animate-in fade-in zoom-in-95 duration-200">
              <div class="flex items-center justify-between mb-6">
                <div class="flex items-center gap-3">
                  <div class="w-10 h-10 rounded-xl bg-rose-50 dark:bg-rose-950/60 text-rose-500 flex items-center justify-center">
                    <i data-lucide="arrow-down-right" class="w-5 h-5"></i>
                  </div>
                  <div>
                    <h3 class="text-lg font-extrabold">Add New Expense</h3>
                    <p class="text-xs text-slate-400">Captured automatically with current date & time</p>
                  </div>
                </div>
                <button onclick="closeModal()" class="p-2 text-slate-400 hover:text-slate-600 rounded-lg">
                  <i data-lucide="x" class="w-5 h-5"></i>
                </button>
              </div>

              <form onsubmit="handleCreateExpense(event)" class="space-y-4">
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                  <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Amount (${state.user.currency}) *</label>
                    <input type="number" step="0.01" min="1" id="exp-amount" required placeholder="0.00" class="w-full px-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm font-bold focus:ring-2 focus:ring-rose-500 focus:outline-none">
                  </div>
                  <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Expense Name *</label>
                    <input type="text" id="exp-title" required placeholder="e.g. Lunch with team" class="w-full px-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm focus:ring-2 focus:ring-rose-500 focus:outline-none">
                  </div>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                  <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Category</label>
                    <select id="exp-category" class="w-full px-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm focus:ring-2 focus:ring-rose-500 focus:outline-none">
                      <option value="Food">Food 🍔</option>
                      <option value="Travel">Travel 🚇</option>
                      <option value="Shopping">Shopping 🛍️</option>
                      <option value="Education">Education 🎓</option>
                      <option value="Bills">Bills ⚡</option>
                      <option value="Entertainment">Entertainment 🎬</option>
                      <option value="Health">Health 💊</option>
                      <option value="Other">Other 📦</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Payment Method</label>
                    <select id="exp-method" class="w-full px-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm focus:ring-2 focus:ring-rose-500 focus:outline-none">
                      <option value="UPI">UPI / GPay</option>
                      <option value="Credit Card">Credit Card</option>
                      <option value="Debit Card">Debit Card</option>
                      <option value="Cash">Cash</option>
                      <option value="Other">Other</option>
                    </select>
                  </div>
                </div>

                <!-- Automatic Date / Time with Edit Switch -->
                <div class="p-3.5 rounded-2xl bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-800 space-y-2">
                  <div class="flex items-center justify-between">
                    <span class="text-xs font-semibold text-slate-500 flex items-center gap-1.5">
                      <i data-lucide="clock" class="w-3.5 h-3.5"></i> Timestamp captured
                    </span>
                    <button type="button" onclick="document.getElementById('exp-custom-dt').classList.toggle('hidden')" class="text-xs text-indigo-600 dark:text-indigo-400 font-bold hover:underline">
                      Edit Date & Time
                    </button>
                  </div>
                  <div id="exp-custom-dt" class="hidden grid grid-cols-2 gap-2 pt-2">
                    <input type="date" id="exp-date" value="${defaultDate}" class="px-3 py-2 rounded-lg border border-slate-200 dark:border-slate-700 bg-white dark:bg-slate-800 text-xs">
                    <input type="text" id="exp-time" value="${defaultTime}" class="px-3 py-2 rounded-lg border border-slate-200 dark:border-slate-700 bg-white dark:bg-slate-800 text-xs">
                  </div>
                </div>

                <div>
                  <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Note (Optional)</label>
                  <input type="text" id="exp-note" placeholder="Add remarks or tags" class="w-full px-4 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-xs focus:ring-2 focus:ring-rose-500 focus:outline-none">
                </div>

                <div class="flex justify-end gap-3 pt-4">
                  <button type="button" onclick="closeModal()" class="px-5 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 text-xs font-bold">Cancel</button>
                  <button type="submit" class="px-6 py-2.5 rounded-xl bg-rose-600 hover:bg-rose-700 text-white text-xs font-bold shadow-lg shadow-rose-600/25">Save Expense</button>
                </div>
              </form>
            </div>
          </div>
        `;
      }

      if (state.activeModal === 'income') {
        return `
          <div class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4">
            <div class="w-full max-w-lg bg-white dark:bg-[#131b2e] rounded-3xl p-6 sm:p-8 border border-slate-200 dark:border-slate-800 shadow-2xl animate-in fade-in zoom-in-95 duration-200">
              <div class="flex items-center justify-between mb-6">
                <div class="flex items-center gap-3">
                  <div class="w-10 h-10 rounded-xl bg-emerald-50 dark:bg-emerald-950/60 text-emerald-500 flex items-center justify-center">
                    <i data-lucide="arrow-up-right" class="w-5 h-5"></i>
                  </div>
                  <div>
                    <h3 class="text-lg font-extrabold">Add Income</h3>
                    <p class="text-xs text-slate-400">Register new funds into your cashflow</p>
                  </div>
                </div>
                <button onclick="closeModal()" class="p-2 text-slate-400 hover:text-slate-600 rounded-lg">
                  <i data-lucide="x" class="w-5 h-5"></i>
                </button>
              </div>

              <form onsubmit="handleCreateIncome(event)" class="space-y-4">
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                  <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Amount (${state.user.currency}) *</label>
                    <input type="number" step="0.01" min="1" id="inc-amount" required placeholder="0.00" class="w-full px-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm font-bold focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                  </div>
                  <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Income Title *</label>
                    <input type="text" id="inc-title" required placeholder="e.g. Consulting Fee" class="w-full px-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                  </div>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                  <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Category</label>
                    <select id="inc-category" class="w-full px-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                      <option value="Salary">Salary 💼</option>
                      <option value="Investments">Investments 📈</option>
                      <option value="Pocket Money">Pocket Money 💰</option>
                      <option value="Bonus">Bonus 🎉</option>
                      <option value="Other">Other 📦</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Payment Method</label>
                    <select id="inc-method" class="w-full px-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                      <option value="UPI">UPI / GPay</option>
                      <option value="Bank Transfer">Bank Transfer</option>
                      <option value="Cash">Cash</option>
                      <option value="Cheque">Cheque</option>
                      <option value="Other">Other</option>
                    </select>
                  </div>
                </div>

                <!-- Timestamp -->
                <div class="p-3.5 rounded-2xl bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-800 space-y-2">
                  <div class="flex items-center justify-between">
                    <span class="text-xs font-semibold text-slate-500 flex items-center gap-1.5">
                      <i data-lucide="clock" class="w-3.5 h-3.5"></i> Timestamp captured
                    </span>
                    <button type="button" onclick="document.getElementById('inc-custom-dt').classList.toggle('hidden')" class="text-xs text-indigo-600 dark:text-indigo-400 font-bold hover:underline">
                      Edit Date & Time
                    </button>
                  </div>
                  <div id="inc-custom-dt" class="hidden grid grid-cols-2 gap-2 pt-2">
                    <input type="date" id="inc-date" value="${defaultDate}" class="px-3 py-2 rounded-lg border border-slate-200 dark:border-slate-700 bg-white dark:bg-slate-800 text-xs">
                    <input type="text" id="inc-time" value="${defaultTime}" class="px-3 py-2 rounded-lg border border-slate-200 dark:border-slate-700 bg-white dark:bg-slate-800 text-xs">
                  </div>
                </div>

                <div class="flex justify-end gap-3 pt-4">
                  <button type="button" onclick="closeModal()" class="px-5 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 text-xs font-bold">Cancel</button>
                  <button type="submit" class="px-6 py-2.5 rounded-xl bg-emerald-600 hover:bg-emerald-700 text-white text-xs font-bold shadow-lg shadow-emerald-600/25">Save Income</button>
                </div>
              </form>
            </div>
          </div>
        `;
      }

      if (state.activeModal === 'budget') {
        return `
          <div class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4">
            <div class="w-full max-w-md bg-white dark:bg-[#131b2e] rounded-3xl p-6 sm:p-8 border border-slate-200 dark:border-slate-800 shadow-2xl animate-in fade-in zoom-in-95 duration-200">
              <div class="flex items-center justify-between mb-6">
                <div class="flex items-center gap-3">
                  <div class="w-10 h-10 rounded-xl bg-indigo-50 dark:bg-indigo-950/60 text-indigo-600 flex items-center justify-center">
                    <i data-lucide="target" class="w-5 h-5"></i>
                  </div>
                  <h3 class="text-lg font-extrabold">Set Monthly Budget</h3>
                </div>
                <button onclick="closeModal()" class="p-2 text-slate-400 hover:text-slate-600 rounded-lg">
                  <i data-lucide="x" class="w-5 h-5"></i>
                </button>
              </div>

              <form onsubmit="handleSetBudget(event)" class="space-y-4">
                <div>
                  <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Monthly Spending Limit (${state.user.currency})</label>
                  <input type="number" min="1" id="budget-input" value="${state.user.monthlyBudget}" required class="w-full px-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-base font-extrabold focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                  <p class="text-xs text-slate-400 mt-2">SpendWise will calculate consumption percentages and caution you when approaching 75% or 90%.</p>
                </div>

                <div class="flex justify-end gap-3 pt-4">
                  <button type="button" onclick="closeModal()" class="px-5 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 text-xs font-bold">Cancel</button>
                  <button type="submit" class="px-6 py-2.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white text-xs font-bold shadow-lg shadow-indigo-600/25">Update Budget</button>
                </div>
              </form>
            </div>
          </div>
        `;
      }

      if (state.activeModal === 'aiKey') {
        return `
          <div class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4">
            <div class="w-full max-w-md bg-white dark:bg-[#131b2e] rounded-3xl p-6 sm:p-8 border border-slate-200 dark:border-slate-800 shadow-2xl animate-in fade-in zoom-in-95 duration-200">
              <div class="flex items-center justify-between mb-4">
                <div class="flex items-center gap-3">
                  <div class="w-10 h-10 rounded-xl bg-indigo-600 text-white flex items-center justify-center">
                    <i data-lucide="sparkles" class="w-5 h-5"></i>
                  </div>
                  <div>
                    <h3 class="text-lg font-extrabold">Gemini 3.5 Flash-Lite</h3>
                    <p class="text-xs text-slate-400">Google AI Studio API Configuration</p>
                  </div>
                </div>
                <button onclick="closeModal()" class="p-2 text-slate-400 hover:text-slate-600 rounded-lg">
                  <i data-lucide="x" class="w-5 h-5"></i>
                </button>
              </div>

              <div class="text-xs text-slate-500 dark:text-slate-400 space-y-2 mb-4">
                <p>SpendWise connects directly to Google AI Studio to run <strong class="text-indigo-600 dark:text-indigo-400">Gemini 3.5 Flash-Lite</strong> with tool execution.</p>
                <p>Your API key is stored strictly on your device inside LocalStorage and is never relayed to third parties.</p>
              </div>

              <div class="space-y-4">
                <div>
                  <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">API Key</label>
                  <input type="password" id="modal-api-key" placeholder="AIzaSy..." value="${state.aiApiKey}" class="w-full px-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-xs font-mono focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                </div>

                <div class="flex items-center justify-between text-xs">
                  <a href="https://aistudio.google.com/app/apikey" target="_blank" class="text-indigo-600 dark:text-indigo-400 font-bold hover:underline flex items-center gap-1">
                    Get key from Google AI Studio <i data-lucide="external-link" class="w-3 h-3"></i>
                  </a>
                  <button type="button" onclick="state.aiApiKey = ''; persistState(); renderApp(); showToast('API Key cleared. Simulation Mode restored.', 'info')" class="text-rose-500 hover:underline">
                    Clear Key
                  </button>
                </div>

                <div class="flex justify-end gap-3 pt-2">
                  <button type="button" onclick="closeModal()" class="px-5 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 text-xs font-bold">Close</button>
                  <button type="button" onclick="saveApiKeyFromModal()" class="px-6 py-2.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white text-xs font-bold shadow-lg shadow-indigo-600/25">Save & Connect</button>
                </div>
              </div>
            </div>
          </div>
        `;
      }

      if (state.activeModal === 'editTx' && state.editingTx) {
        const tx = state.editingTx;
        return `
          <div class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4">
            <div class="w-full max-w-lg bg-white dark:bg-[#131b2e] rounded-3xl p-6 sm:p-8 border border-slate-200 dark:border-slate-800 shadow-2xl animate-in fade-in zoom-in-95 duration-200">
              <div class="flex items-center justify-between mb-6">
                <h3 class="text-lg font-extrabold">Edit Transaction</h3>
                <button onclick="closeModal()" class="p-2 text-slate-400 hover:text-slate-600 rounded-lg">
                  <i data-lucide="x" class="w-5 h-5"></i>
                </button>
              </div>

              <form onsubmit="handleUpdateTransaction(event)" class="space-y-4">
                <div class="grid grid-cols-2 gap-4">
                  <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Amount</label>
                    <input type="number" step="0.01" min="1" id="edit-amount" value="${tx.amount}" required class="w-full px-4 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm font-bold">
                  </div>
                  <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Title</label>
                    <input type="text" id="edit-title" value="${tx.title}" required class="w-full px-4 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm">
                  </div>
                </div>

                <div class="grid grid-cols-2 gap-4">
                  <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Category</label>
                    <input type="text" id="edit-category" value="${tx.category}" required class="w-full px-4 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm">
                  </div>
                  <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Payment Method</label>
                    <input type="text" id="edit-method" value="${tx.paymentMethod}" required class="w-full px-4 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-sm">
                  </div>
                </div>

                <div class="grid grid-cols-2 gap-4">
                  <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Date</label>
                    <input type="date" id="edit-date" value="${tx.date}" class="w-full px-4 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-xs">
                  </div>
                  <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Time</label>
                    <input type="text" id="edit-time" value="${tx.time}" class="w-full px-4 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-xs">
                  </div>
                </div>

                <div>
                  <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Note</label>
                  <input type="text" id="edit-note" value="${tx.note || ''}" class="w-full px-4 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900 text-xs">
                </div>

                <div class="flex justify-end gap-3 pt-4">
                  <button type="button" onclick="closeModal()" class="px-5 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 text-xs font-bold">Cancel</button>
                  <button type="submit" class="px-6 py-2.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white text-xs font-bold shadow-lg shadow-indigo-600/25">Save Changes</button>
                </div>
              </form>
            </div>
          </div>
        `;
      }

      return '';
    }

    // ==========================================
    // FLOATING GEMINI 3.5 AI ASSISTANT CHAT DRAWER
    // ==========================================
    function renderAIChatDrawer() {
      if (!state.isLoggedIn) return '';

      return `
        <!-- Floating Toggle Trigger Button -->
        <button onclick="toggleAIChat()" class="fixed right-6 bottom-20 lg:bottom-8 z-40 px-4 py-3 rounded-full bg-gradient-to-r from-indigo-600 via-indigo-700 to-violet-700 text-white shadow-2xl shadow-indigo-600/50 flex items-center gap-2.5 hover:scale-105 transition transform pulse-glow">
          <i data-lucide="sparkles" class="w-5 h-5 text-amber-300"></i>
          <span class="text-xs font-bold tracking-wide">Gemini 3.5 Copilot</span>
          ${state.aiApiKey ? '<span class="w-2 h-2 rounded-full bg-emerald-400"></span>' : '<span class="w-2 h-2 rounded-full bg-amber-400"></span>'}
        </button>

        <!-- Slide-out AI Panel -->
        <div id="ai-chat-panel" class="fixed right-4 bottom-24 lg:bottom-12 z-50 w-[94vw] sm:w-[420px] max-h-[82vh] h-[600px] bg-white dark:bg-[#131b2e] rounded-3xl border border-slate-200 dark:border-slate-800 shadow-2xl flex flex-col overflow-hidden transition-all duration-300 ${
          state.aiChatOpen ? 'opacity-100 scale-100 pointer-events-auto' : 'opacity-0 scale-95 pointer-events-none'
        }">
          <!-- Header -->
          <div class="p-4 bg-gradient-to-r from-indigo-600 to-violet-600 text-white flex items-center justify-between shrink-0">
            <div class="flex items-center gap-2.5">
              <div class="w-9 h-9 rounded-xl bg-white/15 backdrop-blur-md flex items-center justify-center text-white">
                <i data-lucide="bot" class="w-5 h-5"></i>
              </div>
              <div>
                <div class="text-xs font-black flex items-center gap-1.5">
                  SpendWise AI Copilot
                  <span class="text-[9px] px-1.5 py-0.5 rounded bg-white/20 font-mono">Gemini 3.5 Flash-Lite</span>
                </div>
                <div class="text-[10px] text-indigo-100 flex items-center gap-1">
                  ${state.aiApiKey ? '<span class="text-emerald-300">● Live AI Studio API Key</span>' : '<span class="text-amber-300">○ Simulation Mode (Key not set)</span>'}
                </div>
              </div>
            </div>

            <div class="flex items-center gap-1">
              <button onclick="openModal('aiKey')" title="Configure API Key" class="p-1.5 rounded-lg hover:bg-white/15 text-white">
                <i data-lucide="key" class="w-4 h-4"></i>
              </button>
              <button onclick="clearAIChat()" title="Clear Chat" class="p-1.5 rounded-lg hover:bg-white/15 text-white">
                <i data-lucide="rotate-ccw" class="w-4 h-4"></i>
              </button>
              <button onclick="toggleAIChat()" class="p-1.5 rounded-lg hover:bg-white/15 text-white">
                <i data-lucide="x" class="w-4 h-4"></i>
              </button>
            </div>
          </div>

          <!-- Quick Action Prompts -->
          <div class="px-4 py-2 bg-slate-50 dark:bg-slate-900 border-b border-slate-100 dark:border-slate-800 flex items-center gap-2 overflow-x-auto custom-scrollbar whitespace-nowrap text-[11px]">
            <button onclick="sendQuickPrompt('Add ₹450 expense for Uber to office via UPI')" class="px-2.5 py-1 rounded-full bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 hover:border-indigo-500 shrink-0">
              🚕 Add ₹450 Uber
            </button>
            <button onclick="sendQuickPrompt('What is my current financial status and budget health?')" class="px-2.5 py-1 rounded-full bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 hover:border-indigo-500 shrink-0">
              📊 Budget Health
            </button>
            <button onclick="sendQuickPrompt('Set my monthly budget to ₹30,000')" class="px-2.5 py-1 rounded-full bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 hover:border-indigo-500 shrink-0">
              🎯 Budget ₹30k
            </button>
            <button onclick="sendQuickPrompt('Switch to dark mode')" class="px-2.5 py-1 rounded-full bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 hover:border-indigo-500 shrink-0">
              🌙 Dark Theme
            </button>
          </div>

          <!-- Messages Container -->
          <div id="ai-messages-scroll" class="flex-1 p-4 overflow-y-auto custom-scrollbar space-y-3 text-xs">
            ${state.aiMessages.map(msg => {
              const isUser = msg.role === 'user';
              if (msg.toolExec) {
                return `
                  <div class="p-2.5 rounded-xl bg-indigo-50 dark:bg-indigo-950/60 border border-indigo-200/60 dark:border-indigo-800/60 font-mono text-[11px] text-indigo-700 dark:text-indigo-300 flex items-center gap-2">
                    <span class="w-2 h-2 rounded-full bg-indigo-500 animate-ping"></span>
                    <span>${msg.text}</span>
                  </div>
                `;
              }
              return `
                <div class="flex flex-col ${isUser ? 'items-end' : 'items-start'}">
                  <div class="max-w-[85%] rounded-2xl px-4 py-2.5 ${
                    isUser 
                      ? 'bg-indigo-600 text-white rounded-br-sm' 
                      : msg.isError 
                        ? 'bg-rose-50 dark:bg-rose-950/50 text-rose-600 dark:text-rose-300 border border-rose-200 rounded-bl-sm' 
                        : 'bg-slate-100 dark:bg-slate-800/80 text-slate-800 dark:text-slate-200 border border-slate-200/60 dark:border-slate-700/60 rounded-bl-sm'
                  }">
                    <p class="leading-relaxed whitespace-pre-wrap">${msg.text}</p>
                  </div>
                  <span class="text-[9px] text-slate-400 mt-1 px-1">${msg.timestamp}</span>
                </div>
              `;
            }).join('')}

            ${state.aiThinking ? `
              <div class="flex items-center gap-2 text-slate-400 text-xs italic">
                <i data-lucide="loader-2" class="w-4 h-4 animate-spin text-indigo-500"></i>
                Gemini 3.5 is reasoning and executing tools...
              </div>
            ` : ''}
          </div>

          <!-- Input Bar -->
          <form onsubmit="handleAIChatSubmit(event)" class="p-3 bg-white dark:bg-[#131b2e] border-t border-slate-100 dark:border-slate-800 flex items-center gap-2">
            <input type="text" id="ai-chat-input" placeholder="Ask AI: 'Add ₹600 for Dinner' or 'Show analytics'..." class="flex-1 px-4 py-2.5 rounded-xl bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
            <button type="submit" class="p-2.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white transition disabled:opacity-50">
              <i data-lucide="send" class="w-4 h-4"></i>
            </button>
          </form>
        </div>
      `;
    }

    // ==========================================
    // MAIN APP RENDER DISPATCHER
    // ==========================================
    function renderApp() {
      const appEl = document.getElementById('app');

      if (!state.isLoggedIn) {
        if (state.currentPage === 'signup') {
          appEl.innerHTML = renderAuthPage('signup');
        } else if (state.currentPage === 'login') {
          appEl.innerHTML = renderAuthPage('login');
        } else {
          appEl.innerHTML = renderLandingPage();
        }
      } else {
        // Logged In Shell
        let mainContent = '';
        switch (state.currentPage) {
          case 'dashboard':
            mainContent = renderDashboardView();
            break;
          case 'transactions':
            mainContent = renderTransactionsPage();
            break;
          case 'analytics':
            mainContent = renderAnalyticsPage();
            break;
          case 'budget':
            mainContent = renderBudgetPage();
            break;
          case 'settings':
            mainContent = renderSettingsPage();
            break;
          default:
            mainContent = renderDashboardView();
        }

        appEl.innerHTML = `
          <div class="flex-1 flex overflow-hidden">
            ${renderSidebar()}
            <main class="flex-1 overflow-y-auto custom-scrollbar p-5 sm:p-8 pb-28 lg:pb-8">
              ${renderDashboardHeader()}
              ${mainContent}
            </main>
          </div>
          ${renderMobileNavbar()}
          ${renderModals()}
          ${renderAIChatDrawer()}
        `;

        // Render analytics charts if on Analytics page
        if (state.currentPage === 'analytics') {
          setTimeout(initAnalyticsCharts, 50);
        }
      }

      lucide.createIcons();

      // Scroll AI chat to bottom if open
      const scrollEl = document.getElementById('ai-messages-scroll');
      if (scrollEl) {
        scrollEl.scrollTop = scrollEl.scrollHeight;
      }
    }

    // ==========================================
    // CHART.JS INTEGRATION
    // ==========================================
    let flowChartInstance = null;
    let catChartInstance = null;

    function initAnalyticsCharts() {
      const fin = getFinancials();
      const isDark = state.user.darkMode;

      const flowCanvas = document.getElementById('chart-flow');
      if (flowCanvas) {
        if (flowChartInstance) flowChartInstance.destroy();
        flowChartInstance = new Chart(flowCanvas, {
          type: 'bar',
          data: {
            labels: ['Total Inflow (Income)', 'Total Outflow (Expense)', 'Remaining Vault'],
            datasets: [{
              data: [fin.income, fin.expenses, Math.max(0, fin.balance)],
              backgroundColor: ['#10b981', '#f43f5e', '#6366f1'],
              borderRadius: 8
            }]
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
              legend: { display: false }
            },
            scales: {
              y: {
                grid: { color: isDark ? '#1e293b' : '#f1f5f9' },
                ticks: { color: isDark ? '#94a3b8' : '#64748b' }
              },
              x: {
                grid: { display: false },
                ticks: { color: isDark ? '#94a3b8' : '#64748b' }
              }
            }
          }
        });
      }

      const catCanvas = document.getElementById('chart-categories');
      if (catCanvas) {
        if (catChartInstance) catChartInstance.destroy();

        const catMap = {};
        state.transactions
          .filter(t => t.type === 'expense')
          .forEach(t => { catMap[t.category] = (catMap[t.category] || 0) + Number(t.amount); });

        const labels = Object.keys(catMap);
        const dataValues = Object.values(catMap);

        catChartInstance = new Chart(catCanvas, {
          type: 'doughnut',
          data: {
            labels: labels.length ? labels : ['No Expenses'],
            datasets: [{
              data: dataValues.length ? dataValues : [1],
              backgroundColor: [
                '#6366f1', '#f43f5e', '#ec4899', '#8b5cf6', 
                '#10b981', '#f59e0b', '#06b6d4', '#64748b'
              ],
              borderWidth: 0
            }]
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
              legend: {
                position: 'right',
                labels: { color: isDark ? '#94a3b8' : '#64748b', boxWidth: 12 }
              }
            }
          }
        });
      }
    }

    // ==========================================
    // ACTION HANDLERS & EVENT LISTENERS
    // ==========================================
    function navigateTo(page) {
      state.currentPage = page;
      renderApp();
    }

    function toggleThemeGlobal() {
      state.user.darkMode = !state.user.darkMode;
      applyTheme();
      persistState();
      renderApp();
    }

    function openModal(modalName) {
      state.activeModal = modalName;
      renderApp();
    }

    function closeModal() {
      state.activeModal = null;
      state.editingTx = null;
      renderApp();
    }

    function toggleAIChat() {
      state.aiChatOpen = !state.aiChatOpen;
      renderApp();
    }

    function clearAIChat() {
      state.aiMessages = [
        {
          role: 'model',
          text: "Chat cleared! How can I help you manage your funds today?",
          timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
        }
      ];
      renderApp();
    }

    function sendQuickPrompt(promptText) {
      sendPromptToGemini(promptText);
    }

    function handleAIChatSubmit(e) {
      e.preventDefault();
      const input = document.getElementById('ai-chat-input');
      const val = input.value.trim();
      if (!val) return;
      input.value = '';
      sendPromptToGemini(val);
    }

    function handleAuthSubmit(e, type) {
      e.preventDefault();
      if (type === 'signup') {
        const name = document.getElementById('auth-name').value.trim();
        const email = document.getElementById('auth-email').value.trim();
        const pwd = document.getElementById('auth-password').value;
        const confirm = document.getElementById('auth-confirm').value;

        if (pwd !== confirm) {
          document.getElementById('auth-error').textContent = "Passwords do not match.";
          document.getElementById('auth-error').classList.remove('hidden');
          return;
        }

        state.user.name = name;
        state.user.email = email;
        state.user.password = pwd;
        state.isLoggedIn = true;
        state.currentPage = 'dashboard';
        persistState();
        showToast("Account created successfully! Welcome to SpendWise.", "success");
        renderApp();
      } else {
        state.isLoggedIn = true;
        state.currentPage = 'dashboard';
        persistState();
        showToast("Logged in successfully.", "success");
        renderApp();
      }
    }

    function handleLogout() {
      state.isLoggedIn = false;
      state.currentPage = 'landing';
      persistState();
      showToast("Signed out safely.", "info");
      renderApp();
    }

    function togglePasswordVisibility(inputId, btn) {
      const el = document.getElementById(inputId);
      if (el.type === 'password') {
        el.type = 'text';
      } else {
        el.type = 'password';
      }
    }

    function handleCreateExpense(e) {
      e.preventDefault();
      const amount = parseFloat(document.getElementById('exp-amount').value);
      const title = document.getElementById('exp-title').value.trim();
      const category = document.getElementById('exp-category').value;
      const paymentMethod = document.getElementById('exp-method').value;
      const date = document.getElementById('exp-date').value;
      const time = document.getElementById('exp-time').value;
      const note = document.getElementById('exp-note').value.trim();

      const newTx = {
        id: 'tx-' + Date.now(),
        title,
        amount,
        type: 'expense',
        category,
        paymentMethod,
        date,
        time,
        note
      };

      state.transactions.unshift(newTx);
      persistState();
      closeModal();
      showToast(`Expense added: ${formatCurrency(amount)}`, 'success');
      renderApp();
    }

    function handleCreateIncome(e) {
      e.preventDefault();
      const amount = parseFloat(document.getElementById('inc-amount').value);
      const title = document.getElementById('inc-title').value.trim();
      const category = document.getElementById('inc-category').value;
      const paymentMethod = document.getElementById('inc-method').value;
      const date = document.getElementById('inc-date').value;
      const time = document.getElementById('inc-time').value;

      const newTx = {
        id: 'tx-' + Date.now(),
        title,
        amount,
        type: 'income',
        category,
        paymentMethod,
        date,
        time
      };

      state.transactions.unshift(newTx);
      persistState();
      closeModal();
      showToast(`Income credited: ${formatCurrency(amount)}`, 'success');
      renderApp();
    }

    function handleSetBudget(e) {
      e.preventDefault();
      const val = parseFloat(document.getElementById('budget-input').value);
      state.user.monthlyBudget = val;
      persistState();
      closeModal();
      showToast(`Monthly budget set to ${formatCurrency(val)}`, 'success');
      renderApp();
    }

    function editTransactionModal(id) {
      const tx = state.transactions.find(t => t.id === id);
      if (tx) {
        state.editingTx = { ...tx };
        state.activeModal = 'editTx';
        renderApp();
      }
    }

    function handleUpdateTransaction(e) {
      e.preventDefault();
      const idx = state.transactions.findIndex(t => t.id === state.editingTx.id);
      if (idx !== -1) {
        state.transactions[idx] = {
          ...state.editingTx,
          amount: parseFloat(document.getElementById('edit-amount').value),
          title: document.getElementById('edit-title').value.trim(),
          category: document.getElementById('edit-category').value.trim(),
          paymentMethod: document.getElementById('edit-method').value.trim(),
          date: document.getElementById('edit-date').value,
          time: document.getElementById('edit-time').value,
          note: document.getElementById('edit-note').value.trim()
        };
        persistState();
        closeModal();
        showToast("Transaction updated successfully", "success");
        renderApp();
      }
    }

    function confirmDeleteTransaction(id) {
      const tx = state.transactions.find(t => t.id === id);
      if (confirm(`Are you sure you want to delete "${tx ? tx.title : 'this transaction'}"?`)) {
        state.transactions = state.transactions.filter(t => t.id !== id);
        persistState();
        showToast("Transaction deleted", "info");
        renderApp();
      }
    }

    function saveApiKeyFromModal() {
      const input = document.getElementById('modal-api-key');
      state.aiApiKey = input.value.trim();
      persistState();
      closeModal();
      showToast("Gemini 3.5 API key saved!", "success");
      renderApp();
    }

    function saveApiKeyFromSettings() {
      const input = document.getElementById('settings-api-key');
      state.aiApiKey = input.value.trim();
      persistState();
      showToast("Gemini 3.5 API key saved!", "success");
      renderApp();
    }

    function exportCSV() {
      let csv = "ID,Title,Type,Category,Amount,Payment Method,Date,Time,Note\n";
      state.transactions.forEach(t => {
        csv += `"${t.id}","${t.title}","${t.type}","${t.category}",${t.amount},"${t.paymentMethod}","${t.date}","${t.time}","${t.note || ''}"\n`;
      });

      const blob = new Blob([csv], { type: 'text/csv' });
      const url = window.URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.setAttribute('href', url);
      a.setAttribute('download', `SpendWise_Export_${new Date().toISOString().split('T')[0]}.csv`);
      a.click();
      showToast("CSV exported successfully", "success");
    }

    // Initial Render
    window.addEventListener('DOMContentLoaded', () => {
      renderApp();
    });
  </script>
</body>
</html>
