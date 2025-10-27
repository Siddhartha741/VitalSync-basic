# VitalSync- web page





<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VitalSync Health App</title>
    <!-- Load Tailwind CSS --><script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap');
        body { font-family: 'Inter', sans-serif; }
        
        /* --- NEW PROFESSIONAL COLOR PALETTE (Coral/Salmon) --- */
        :root {
            --color-primary: #FF8A65; /* Coral */
            --color-primary-dark: #E67C5E;
            --color-primary-light: #FFECE9;
            --color-primary-lightest: #FFF8F6;
            
            /* Dark Mode Colors - Adjusted */
            --color-bg-dark: #121212; /* Near black for main background */
            --color-sidebar-dark: #1B1B1B; /* Darker sidebar color */
            --color-card-dark: #2C2C2C; /* Darker grey for cards */
            --color-text-dark: #E0E0E0; /* Off-white for general text */
            --color-subtext-dark: #A0A0A0; /* Lighter grey for subtext */
            --color-border-dark: #333333; /* Darker border color */
            --color-input-dark: #2C2C2C; /* Darker input background */
        }

        /* Utility Styles from React Component Definitions */
        .input-field {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #d1d5db; /* gray-300 */
            border-radius: 0.5rem; /* rounded-lg */
            transition: all 150ms ease-in-out;
            background-color: white; /* Default light mode BG */
            color: #1f2937; /* Default text color */
        }
        .input-field:focus {
            outline: none;
            box-shadow: 0 0 0 2px rgba(255, 138, 101, 0.5); /* Primary ring */
            border-color: var(--color-primary);
        }
        
        /* Dark mode specific input styles */
        .dark .input-field {
            background-color: var(--color-input-dark);
            border-color: var(--color-border-dark);
            color: var(--color-text-dark);
        }

        .btn-primary {
            background-color: var(--color-primary);
            color: white;
            transition: background-color 150ms ease-in-out, box-shadow 150ms ease-in-out;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* shadow-md */
        }
        .btn-primary:hover {
            background-color: var(--color-primary-dark);
        }
        .dashboard-card {
            padding: 1.5rem;
            border-radius: 0.75rem; /* rounded-xl */
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05); /* shadow-lg */
            border: 1px solid #f3f4f6; /* border-gray-100 */
            background-color: white; /* Default */
            color: #1f2937; /* Default text */
            transition: background-color 300ms ease-in-out, color 300ms ease-in-out, border-color 300ms ease-in-out;
        }
        
        /* Dark mode specific card styles */
        .dark .dashboard-card {
            background-color: var(--color-card-dark);
            border-color: var(--color-border-dark);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.3), 0 4px 6px -2px rgba(0, 0, 0, 0.1); 
            color: var(--color-text-dark);
        }

        .upload-box {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 3rem;
            border: 2px dashed #d1d5db; /* gray-300 */
            border-radius: 0.75rem; /* rounded-xl */
            text-align: center;
            cursor: pointer;
            transition: border-color 150ms ease-in-out;
        }
        .upload-box:hover {
            border-color: var(--color-primary);
        }
        .dark .upload-box {
            border-color: var(--color-border-dark);
        }
        .dark .upload-box:hover {
             border-color: var(--color-primary);
        }
        
        /* Chat bubble styles */
        .chat-container {
            height: calc(100vh - 200px); /* Adjust based on header/footer size */
        }
        .chat-bubble {
            max-width: 80%; /* Adjusted for better mobile view */
            padding: 0.75rem;
            border-radius: 0.75rem; /* rounded-xl */
            box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05); /* shadow-sm */
            font-size: 1rem;
        }
        .agent {
            background-color: #e5e7eb; /* gray-200 */
            color: #1f2937; /* gray-800 */
            border-top-left-radius: 0.25rem; /* rounded-tl-none */
            margin-right: auto;
            transition: background-color 300ms ease-in-out, color 300ms ease-in-out;
        }
        .dark .agent {
            background-color: #333333; /* Darker grey */
            color: var(--color-text-dark);
        }
        .user {
            background-color: var(--color-primary);
            color: white;
            border-top-right-radius: 0.25rem; /* rounded-br-none */
            margin-left: auto;
        }
        /* Typing indicator animation */
        .typing-dot {
            display: inline-block;
            width: 8px;
            height: 8px;
            background-color: #1f2937;
            border-radius: 50%;
            margin: 0 2px;
            animation: bounce 1.4s infinite ease-in-out both;
        }
        .dark .typing-dot {
            background-color: var(--color-text-dark);
        }
        @keyframes bounce {
            0%, 80%, 100% { transform: scale(0); }
            40% { transform: scale(1.0); }
        }

        /* --- GLOBAL DARK MODE STYLES --- */
        .dark body {
            background-color: var(--color-bg-dark); /* Apply dark background to body */
        }
        .dark #main-content { /* Specific for the main content area */
            background-color: var(--color-bg-dark);
            color: var(--color-text-dark);
        }
        
        /* Text colors for dark mode */
        .dark .text-gray-900 { color: var(--color-text-dark); }
        .dark .text-gray-800 { color: var(--color-text-dark); }
        .dark .text-gray-700 { color: var(--color-text-dark); }
        .dark .text-gray-600 { color: var(--color-subtext-dark); }
        .dark .text-gray-500 { color: var(--color-subtext-dark); }
        
        /* Backgrounds for dark mode */
        .dark .bg-gray-50 { background-color: var(--color-bg-dark); }
        .dark .bg-white { background-color: var(--color-card-dark); }
        .dark .bg-gray-100 { background-color: #333333; } /* Darker hover/button background */
        .dark .hover\:bg-gray-200:hover { background-color: #444444; } /* Even darker on hover */

        /* Borders for dark mode */
        .dark .border-gray-100, .dark .border-gray-200, .dark .border-gray-300 {
            border-color: var(--color-border-dark);
        }
        
        /* Shadows for dark mode - make them subtle or remove */
        .dark .shadow-md, .dark .shadow-lg, .dark .shadow-xl, .dark .shadow-2xl {
            box-shadow: none; /* Remove harsh shadows, rely on background difference */
        }

        /* Specific element overrides to keep light mode appearance */
        .dark #sidebar {
            background-color: var(--color-sidebar-dark); /* Changed sidebar to dark gray/black */
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .dark #sidebar .text-gray-600 { 
            color: var(--color-subtext-dark); /* Sidebar nav text is light gray */
        }
        .dark #sidebar .hover\:bg-gray-100:hover {
            background-color: #333333; /* Dark gray hover for sidebar */
        }

    </style>
</head>
<body class="bg-gray-50 transition-colors duration-300">
    <div id="app" class="flex flex-col min-h-screen font-sans">
        <!-- Content will be injected by JavaScript --></div>

    <script>
        // --- 1. GLOBAL STATE & UTILITIES ---

        // Global State - Replaces React Context and all useState calls
        let appState = {
            currentPage: 'login',
            chatHistory: [
                { id: 1, sender: 'agent', text: "Hi! Let's start our 60-second check-in. How was your sleep quality last night (1-5)?" }
            ],
            // Dashboard & Reports Data (simulating data fetching)
            dashboard: {
                userName: "Loading...",
                insights: [],
                isDarkMode: false // UPDATED: State reflects light/dark mode
            },
            reports: [],
            // Chat & Upload UI States
            chat: {
                isAgentTyping: false
            },
            upload: {
                state: 'initial', // 'initial', 'progress', 'success'
                fileName: '',
                progress: 0,
                summary: '',
                isSummarizing: false
            }
        };

        // State update function - Replaces useState setters
        function setState(newState, subStateKey = null) {
            if (subStateKey && appState[subStateKey]) {
                appState[subStateKey] = { ...appState[subStateKey], ...newState };
            } else {
                appState = { ...appState, ...newState };
            }
            renderApp();
        }

        // Navigation function - Replaces navigateTo
        function navigateTo(page) {
            // Clear page-specific ephemeral states on navigation
            if (page === 'dashboard') {
                initializeAppState(); // Re-initialize data fetching
            }
            if (page === 'upload-report') {
                 // Reset upload state
                 setState({ 
                    state: 'initial', fileName: '', progress: 0, summary: '', isSummarizing: false
                }, 'upload');
            }
            
            setState({ currentPage: page });
        }

        // --- 2. ASYNCHRONOUS DATA & MOCK API ---

        // Gemini Mock API Call
        async function callGeminiApi(prompt) {
            console.log("Calling Gemini API with prompt:", prompt);
            await new Promise(resolve => setTimeout(resolve, 1500));

            if (prompt.includes("Summarize the following report")) {
                return "This blood panel shows slightly elevated glucose levels, suggesting a need to monitor sugar intake. All other values, including cholesterol and white blood cell count, are within the normal range. Regular exercise and a balanced diet are recommended.";
            }

            if (prompt.includes("energy level")) {
                return "Thanks for sharing that. It's helpful to know. Sometimes a dip in energy can be linked to sleep or diet. Did you have any particularly heavy meals yesterday?";
            }

            return "That's good to know. Thank you for logging that. Is there anything else you'd like to add about your day?";
        }

        // Simulate initial data fetching on app start or dashboard load
        function initializeAppState() {
            // Dashboard Data Simulation
            setTimeout(() => {
                setState({ 
                    userName: "Alex",
                    insights: [
                        { id: 1, type: "Possible Pattern Detected", text: "I've noticed that on days you report poor sleep, your stress levels the next afternoon tend to be higher. Does that sound right to you?" },
                        { id: 2, type: "Forecast", text: "Since you mentioned a high-stress meeting today, remember that prioritizing a short walk this evening has helped lower your stress in the past." }
                    ]
                }, 'dashboard');
            }, 1000);

            // Reports Data Simulation
            setTimeout(() => {
                setState({
                    reports: []
                });
            }, 1000);
        }


        // --- 3. ICONS (SVG Functions) ---
        // Using an external URL for reliability
        function VitalSyncLogo() {
            return <img src="vitalsync logo white.png" alt="VitalSync Logo" class="mx-auto h-10" onerror="this.src='https://placehold.co/150x40/FF8A65/ffffff?text=VitalSync';" />;
        }
        function DashboardIcon() {
            return <svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"></path></svg>;
        }
        function ChatIcon() {
            return <svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z"></path></svg>;
        }
        function ReportsIcon() {
            return <svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V7a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path></svg>;
        }
        function LogoutIcon() {
            return <svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"></path></svg>;
        }
        function UploadIcon() {
            return <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12"></path></svg>;
        }
        function UploadBoxIcon() {
            return <svg class="mx-auto h-12 w-12 text-gray-400" stroke="currentColor" fill="none" viewBox="0 0 48 48"><path d="M28 8H12a4 4 0 00-4 4v20m32-12v8m0 0v8a4 4 0 01-4 4H12a4 4 0 01-4-4v-4m32-4l-3.172-3.172a4 4 0 00-5.656 0L28 28M8 32l9.172-9.172a4 4 0 015.656 0L28 28m0 0l4 4m4-24h8m-4-4v8" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path></svg>;
        }
        function SuccessIcon() {
            return <svg class="h-8 w-8 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>;
        }
        function SparkleIcon() {
            return <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 2a1 1 0 011 1v2.268l1.91 1.273a1 1 0 01.364 1.364l-1.273 1.91V13a1 1 0 11-2 0v-3.179l-1.273-1.91a1 1 0 01.364-1.364L9 5.268V3a1 1 0 011-1zM5 5.5A1.5 1.5 0 016.5 4h.09a1 1 0 00.707-.293l1.414-1.414a1 1 0 00-1.414-1.414L5.88 2.293A1 1 0 005.172 3H3.5A1.5 1.5 0 002 4.5v1.672a1 1 0 00.293.707l1.414 1.414a1 1 0 001.414-1.414L3.707 6.41A1 1 0 003 5.5V5.5zm10 0A1.5 1.5 0 0013.5 4h-.09a1 1 0 01-.707-.293l-1.414-1.414a1 1 0 111.414-1.414L14.12 2.293A1 1 0 0114.828 3h1.672A1.5 1.5 0 0118 4.5v1.672a1 1 0 01-.293.707l-1.414 1.414a1 1 0 11-1.414-1.414L16.293 6.41A1 1 0 0117 5.5V5.5zM5.172 17a1 1 0 01.707.293l1.414 1.414a1 1 0 01-1.414 1.414L4.464 18.707A1 1 0 013.757 18H2a1.5 1.5 0 01-1.5-1.5v-1.586a1 1 0 01.293-.707l1.414-1.414a1 1 0 011.414 1.414L2.293 15.293A1 1 0 003 16h1.172zm11.192-.293l-1.414-1.414a1 1 0 10-1.414 1.414l1.414 1.414A1 1 0 0015.657 18H17a1.5 1.5 0 001.5-1.5v-1.586a1 1 0 00-.293-.707l-1.414-1.414a1 1 0 10-1.414 1.414l1.414 1.414a1 1 0 01.293.707v.086z" clip-rule="evenodd" /></svg>;
        }


        // --- 4. PAGE RENDERERS (Replaces React Components) ---

        function Sidebar() {
            const { currentPage } = appState;
            // Sidebar link styling remains light-mode consistent
            const linkClass = (page) => flex items-center px-4 py-3 font-semibold rounded-lg mt-2 transition-colors ${currentPage === page || (page === 'reports' && currentPage === 'upload-report') ? 'bg-[#FFECE9] text-[#E67C5E]' : 'text-gray-600 hover:bg-gray-100'};

            return `
                <aside id="sidebar" class="w-64 bg-white shadow-md flex-shrink-0 p-4 hidden md:flex flex-col transition-colors duration-300">
                    <div class="text-center mb-10 pt-2">
                        ${VitalSyncLogo()}
                    </div>
                    <nav class="flex-grow">
                        <a href="#" id="nav-dashboard" class="${linkClass('dashboard')}">
                            ${DashboardIcon()} Dashboard
                        </a>
                        <a href="#" id="nav-chat" class="${linkClass('chat')}">
                            ${ChatIcon()} Daily Check-in
                        </a>
                        <a href="#" id="nav-reports" class="${linkClass('reports')}">
                            ${ReportsIcon()} My Reports
                        </a>
                    </nav>
                    <div class="mt-auto">
                        <a href="#" id="nav-logout" class="flex items-center px-4 py-3 text-gray-600 hover:bg-gray-100 rounded-lg transition-colors">
                            ${LogoutIcon()} Logout
                        </a>
                    </div>
                </aside>
            `;
        }
        
        function LoginPage() {
            return `
                <div class="flex-grow flex items-center justify-center p-4 bg-gray-50 transition-colors duration-300 dark:bg-gray-800">
                    <div class="bg-white rounded-xl shadow-lg p-8 max-w-md w-full transition-colors duration-300 dark:bg-gray-700">
                        <div class="text-center mb-8">
                            ${VitalSyncLogo()}
                            <h1 class="text-3xl font-bold text-gray-900 mt-4 dark:text-gray-100">Welcome Back</h1>
                            <p class="text-gray-500 dark:text-gray-400">Sign in to continue your health journey.</p>
                        </div>
                        <form id="login-form">
                            <div class="mb-4">
                                <label for="email" class="block text-sm font-medium text-gray-700 mb-2 dark:text-gray-300">Email</label>
                                <input type="email" id="email" class="input-field" placeholder="you@example.com" required/>
                            </div>
                            <div class="mb-6">
                                <label for="password" class="block text-sm font-medium text-gray-700 mb-2 dark:text-gray-300">Password</label>
                                <input type="password" id="password" class="input-field" placeholder="••••••••" required/>
                            </div>
                            <button type="button" id="login-btn" class="w-full btn-primary font-semibold py-3 rounded-lg text-lg">Sign In</button>
                        </form>
                        <p class="text-center text-sm text-gray-500 mt-8 dark:text-gray-400">
                            Don't have an account? <a href="#" id="link-signup" class="font-semibold text-[#FF8A65] hover:underline">Sign Up</a>
                        </p>
                    </div>
                </div>
            `;
        }

        function SignupPage() {
            return `
                <div class="flex-grow flex items-center justify-center p-4 bg-gray-50 transition-colors duration-300 dark:bg-gray-800">
                    <div class="bg-white rounded-xl shadow-lg p-8 max-w-md w-full transition-colors duration-300 dark:bg-gray-700">
                        <div class="text-center mb-8">
                            ${VitalSyncLogo()}
                            <h1 class="text-3xl font-bold text-gray-900 mt-4 dark:text-gray-100">Create Your Account</h1>
                            <p class="text-gray-500 dark:text-gray-400">Start understanding your health story today.</p>
                        </div>
                        <form>
                            <div class="mb-4">
                                <label for="signup-name" class="block text-sm font-medium text-gray-700 mb-2 dark:text-gray-300">Full Name</label>
                                <input type="text" id="signup-name" class="input-field" placeholder="Your Name" required/>
                            </div>
                            <div class="mb-4">
                                <label for="signup-email" class="block text-sm font-medium text-gray-700 mb-2 dark:text-gray-300">Email</label>
                                <input type="email" id="signup-email" class="input-field" placeholder="you@example.com" required/>
                            </div>
                            <div class="mb-6">
                                <label for="signup-password" class="block text-sm font-medium text-gray-700 mb-2 dark:text-gray-300">Password</label>
                                <input type="password" id="signup-password" class="input-field" placeholder="••••••••" required/>
                            </div>
                            <button type="button" id="signup-btn" class="w-full btn-primary font-semibold py-3 rounded-lg text-lg">Create Account</button>
                        </form>
                        <p class="text-center text-sm text-gray-500 mt-8 dark:text-gray-400">
                            Already have an account? <a href="#" id="link-login" class="font-semibold text-[#FF8A65] hover:underline">Sign In</a>
                        </p>
                    </div>
                </div>
            `;
        }

        function OTPPage() {
            return `
                <div class="flex-grow flex items-center justify-center p-4 bg-gray-50 transition-colors duration-300 dark:bg-gray-800">
                    <div class="bg-white rounded-xl shadow-lg p-8 max-w-md w-full text-center transition-colors duration-300 dark:bg-gray-700">
                        ${VitalSyncLogo()}
                        <h1 class="text-3xl font-bold text-gray-900 mt-4 dark:text-gray-100">Check Your Email</h1>
                        <p class="text-gray-500 mb-6 dark:text-gray-400">We've sent a 6-digit security code to your email.</p>
                        <div class="flex justify-center gap-2 mb-6" id="otp-inputs">
                            ${[...Array(6)].map((_, i) => `
                                <input 
                                    key="${i}" 
                                    type="text" 
                                    maxlength="1" 
                                    id="otp-${i}"
                                    class="w-14 h-14 text-center text-2xl font-semibold border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-[#FF8A65] transition-all dark:bg-gray-600 dark:border-gray-500 dark:text-gray-100" 
                                    inputmode="numeric"
                                    onkeyup="moveFocus(this, 'otp-${i+1}')"
                                />
                            `).join('')}
                        </div>
                        <button type="button" id="verify-otp-btn" class="w-full btn-primary font-semibold py-3 rounded-lg text-lg">Verify Account</button>
                        <p class="text-center text-sm text-gray-500 mt-6 dark:text-gray-400">
                            Didn't receive a code? <a href="#" class="font-semibold text-[#FF8A65] hover:underline">Resend</a>
                        </p>
                    </div>
                </div>
            `;
        }

        function DashboardPage() {
            const { userName, insights, isDarkMode } = appState.dashboard;

            const insightsHtml = insights.length > 0 ? insights.map(insight => `
                <div key="${insight.id}" class="p-4 bg-gray-50 rounded-lg border border-gray-200 dark:bg-gray-800 dark:border-gray-600">
                    <p class="font-semibold text-gray-800 dark:text-gray-100">${insight.type}</p>
                    <p class="text-sm text-gray-600 dark:text-gray-400">"${insight.text}"</p>
                </div>
            `).join('') : '<p class="text-gray-500 animate-pulse dark:text-gray-400">Loading insights...</p>';

            return `
                <div>
                    <!-- HEADER ROW with TITLE and TOGGLE SWITCH --><div class="flex justify-between items-center mb-2">
                        <h1 class="text-4xl font-bold text-gray-900 dark:text-gray-100">Good Morning, ${userName}</h1>
                        
                        <!-- TOGGLE SWITCH (Light/Dark Mode) --><div class="flex items-center space-x-2">
                            <svg class="w-5 h-5 ${isDarkMode ? 'text-gray-400' : 'text-[#FF8A65]'} transition-colors duration-300" fill="currentColor" viewBox="0 0 20 20"><path d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.808 5.666a1 1 0 01-.158.26l-1.414 1.414a1 1 0 01-1.414 0l-1.414-1.414a1 1 0 010-1.414l1.414-1.414a1 1 0 011.414 0l1.414 1.414a1 1 0 01.158.26zM2 10a1 1 0 011-1h1a1 1 0 110 2H3a1 1 0 01-1-1zm15.707 3.707a1 1 0 010 1.414l-1.414 1.414a1 1 0 01-1.414 0l-1.414-1.414a1 1 0 010-1.414l1.414-1.414a1 1 0 011.414 0l1.414 1.414z"></path></svg>
                            <label class="relative inline-flex items-center cursor-pointer">
                                <input type="checkbox" id="dark-mode-checkbox" class="sr-only peer" ${isDarkMode ? 'checked' : ''}>
                                <div class="w-11 h-6 bg-gray-300 peer-focus:outline-none peer-focus:ring-2 peer-focus:ring-[#FF8A65] rounded-full peer peer-checked:after:translate-x-full rtl:peer-checked:after:-translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:start-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-[#FF8A65]"></div>
                            </label>
                            <svg class="w-5 h-5 ${isDarkMode ? 'text-[#FF8A65]' : 'text-gray-400'} transition-colors duration-300" fill="currentColor" viewBox="0 0 20 20"><path d="M17.293 13.903a8 8 0 11-9.982-12.784 1 1 0 011.536.852c.079.522.682 1.458 1.446 2.502.83 1.137 1.954 2.222 3.327 3.16.89.606 1.83 1.056 2.802 1.346a1 1 0 01-.005 1.956c-.972.29-1.912.74-2.802 1.346-1.373.938-2.497 2.023-3.327 3.16-.764 1.044-1.367 1.98-1.446 2.502a1 1 0 01-1.536.852 8 8 0 019.982-12.784z"></path></svg>
                        </div>
                    </div>
                    <!-- The main dashboard text elements are now using default dark gray colors (text-gray-900/800) which contrast well in light mode. -->
                    <p class="text-lg text-gray-500 dark:text-gray-400 mb-8">Here's your action plan for today.</p>

                    <!-- HERO SECTION - Brief Summary of Website --><div class="dashboard-card p-8 mb-10 shadow-2xl border-l-4 border-l-[#FF8A65]">
                        <h2 class="text-3xl font-bold text-gray-900 mb-3 flex items-center dark:text-gray-100">
                            <svg class="w-7 h-7 mr-3 text-[#FF8A65]" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg>
                            Your AI Health Command Center
                        </h2>
                        <p class="text-gray-600 text-lg dark:text-gray-400">
                            VitalSync is your personalized AI health partner. We securely analyze your daily check-ins and clinical reports to discover hidden patterns, provide tailored forecasts, and offer actionable advice to improve your well-being.
                        </p>
                        <p class="mt-4 text-sm font-medium text-gray-500 dark:text-gray-500">
                            Start a Daily Check-in or upload your latest report to unlock your full health story.
                        </p>
                    </div>

                    <!-- DASHBOARD CONTENT - Structured into 3 columns --><h2 class="text-3xl font-bold text-gray-800 mb-6 dark:text-gray-100">Today's Focus</h2>

                    <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                        
                        <!-- 1. REPORTS / UPLOAD --><div class="dashboard-card bg-[#FF8A65] text-white">
                            <h2 class="text-2xl font-semibold mb-3">Reports & Upload</h2>
                            <p class="text-white opacity-90 mb-4">Link your latest blood work or scans. Get a Gemini-powered summary and connect data points to your life events.</p>
                            <button id="dash-upload-btn" class="bg-white text-[#FF8A65] font-semibold px-6 py-2 rounded-lg flex items-center hover:bg-[#FFF8F6] transition-colors">
                                ${UploadIcon()} Upload Report
                            </button>
                        </div>
                        
                        <!-- 2. DAILY CHECK-IN --><div class="dashboard-card border border-gray-200">
                            <h2 class="text-2xl font-semibold text-gray-800 mb-4 dark:text-gray-100">Daily Check-in</h2>
                            <p class="text-gray-600 mb-4 dark:text-gray-400">Your AI journalist is ready to chat. A quick 60-second conversation can uncover valuable insights.</p>
                            <button id="dash-chat-btn" class="w-full text-center bg-gray-100 text-gray-800 font-semibold py-3 rounded-lg hover:bg-gray-200 transition-colors dark:bg-gray-600 dark:text-gray-100 dark:hover:bg-gray-500">Start Conversation</button>
                        </div>

                        <!-- 3. RECENT INSIGHTS --><div class="dashboard-card border border-gray-200 lg:col-span-1">
                            <h2 class="text-2xl font-semibold text-gray-800 mb-4 dark:text-gray-100">Recent Insights</h2>
                            <div class="space-y-4">
                                ${insightsHtml}
                            </div>
                        </div>
                    </div>
                </div>
            `;
        }

        function ChatPage() {
            const { chatHistory } = appState;
            const { isAgentTyping } = appState.chat;

            const messagesHtml = chatHistory.map((message) => `
                <div key="${message.id}" class="flex ${message.sender === 'user' ? 'justify-end' : 'justify-start'}">
                    <div class="chat-bubble ${message.sender}">
                        ${message.text}
                    </div>
                </div>
            `).join('');

            const typingIndicatorHtml = isAgentTyping ? `
                <div class="flex justify-start">
                    <div class="chat-bubble agent">
                        <div class="flex items-center">
                            <span class="typing-dot"></span>
                            <span class="typing-dot"></span>
                            <span class="typing-dot"></span>
                        </div>
                    </div>
                </div>
            ` : '';

            return `
                <div class="h-full flex flex-col max-w-4xl mx-auto">
                    <h1 class="text-4xl font-bold text-gray-900 mb-6 dark:text-gray-100">Daily Check-in</h1>
                    <!-- Scrollable Chat Area --><div id="chat-messages" class="flex-grow bg-white rounded-lg shadow-inner p-6 flex flex-col space-y-6 overflow-y-auto chat-container dark:bg-gray-700">
                        ${messagesHtml}
                        ${typingIndicatorHtml}
                        <div id="chat-end-ref"></div>
                    </div>
                    <!-- Input Area --><div class="mt-6 flex">
                        <input 
                            type="text" 
                            id="user-input"
                            class="input-field flex-grow text-lg" 
                            placeholder="Type your message..." 
                            value=""
                        />
                        <button id="send-btn" class="btn-primary font-semibold px-6 py-3 rounded-lg ml-3 text-lg">Send</button>
                    </div>
                </div>
            `;
        }

        function ReportsPage() {
            const { reports } = appState;

            if (reports.length === 0) {
                // RENDER EMPTY STATE: Show large upload prompt
                return `
                    <div>
                        <h1 class="text-4xl font-bold text-gray-900 mb-8 dark:text-gray-100">My Reports</h1>
                        <div class="bg-white p-12 rounded-xl shadow-lg text-center max-w-2xl mx-auto dark:bg-gray-700">
                            ${UploadBoxIcon()}
                            <h3 class="mt-4 text-2xl font-semibold text-gray-800 dark:text-gray-100">No Reports Found</h3>
                            <p class="text-gray-600 mt-2 mb-8 dark:text-gray-400">Upload your first clinical report (PDF or Image) to start getting personalized health insights linked to your daily check-ins.</p>
                            <button id="reports-upload-btn" class="btn-primary font-semibold px-8 py-3 rounded-lg flex items-center justify-center mx-auto text-lg">
                                ${UploadIcon()} Upload New Report
                            </button>
                        </div>
                    </div>
                `;
            }

            // RENDER TABLE STATE: Show table and smaller upload button
            const reportsBodyHtml = reports.map((report) => `
                <tr class="dark:bg-gray-700 dark:hover:bg-gray-600 transition-colors duration-200">
                    <td class="p-4 font-medium text-gray-800 dark:text-gray-100">${report.name}</td>
                    <td class="p-4 text-gray-600 dark:text-gray-400">${report.date}</td>
                    <td class="p-4">
                        <span class="px-2.5 py-1 text-xs font-semibold rounded-full ${ report.status === 'Current' ? 'text-green-800 bg-green-100' : 'text-gray-800 bg-gray-100 dark:text-gray-300 dark:bg-gray-800' }">
                            ${report.status}
                        </span>
                    </td>
                    <td class="p-4">
                        <button class="text-sm font-medium text-[#FF8A65] hover:text-[#E67C5E]">Toggle Status</button>
                    </td>
                </tr>
            `).join('');

            return `
                <div>
                    <div class="flex justify-between items-center mb-8">
                        <h1 class="text-4xl font-bold text-gray-900 dark:text-gray-100">My Reports</h1>
                        <button id="reports-upload-btn" class="btn-primary font-semibold px-5 py-2 rounded-lg flex items-center text-base">
                            ${UploadIcon()} Upload New Report
                        </button>
                    </div>
                    <div class="bg-white rounded-lg shadow overflow-hidden dark:bg-gray-700">
                        <table class="w-full text-left">
                            <thead class="bg-gray-50 border-b border-gray-200 dark:bg-gray-800 dark:border-gray-600">
                                <tr>
                                    <th class="p-4 font-semibold text-sm text-gray-600 uppercase tracking-wider dark:text-gray-400">Report Name</th>
                                    <th class="p-4 font-semibold text-sm text-gray-600 uppercase tracking-wider dark:text-gray-400">Date</th>
                                    <th class="p-4 font-semibold text-sm text-gray-600 uppercase tracking-wider dark:text-gray-400">Status</th>
                                    <th class="p-4 font-semibold text-sm text-gray-600 uppercase tracking-wider dark:text-gray-400">Actions</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-gray-200 dark:divide-gray-600">
                                ${reportsBodyHtml}
                            </tbody>
                        </table>
                    </div>
                </div>
            `;
        }

        function UploadReportPage() {
            const { state, fileName, progress, summary, isSummarizing } = appState.upload;

            let contentHtml = '';

            if (state === 'initial') {
                contentHtml = `
                    <div id="upload-box" class="upload-box">
                        <input type="file" id="file-input" class="hidden" accept=".pdf,.jpg,.jpeg,.png" />
                        ${UploadBoxIcon()}
                        <p class="mt-2 text-sm text-gray-600 dark:text-gray-400"><span class="font-semibold text-[#FF8A65]">Click to upload</span> or drag and drop</p>
                        <p class="text-xs text-gray-500 mt-1 dark:text-gray-500">PDF, PNG, JPG up to 10MB</p>
                    </div>
                `;
            } else if (state === 'progress') {
                contentHtml = `
                    <div>
                        <p class="text-center font-semibold text-gray-700 mb-4 dark:text-gray-100">${fileName}</p>
                        <div class="w-full bg-gray-200 rounded-full h-2.5 dark:bg-gray-600">
                            <div class="h-2.5 rounded-full" style="width: ${progress}%; background-color: var(--color-primary);"></div>
                        </div>
                        <p class="text-center text-sm text-gray-500 mt-2 dark:text-gray-400">Uploading... ${progress}%</p>
                    </div>
                `;
            } else if (state === 'success') {
                const summaryHtml = summary ? `
                    <div class="mt-6 text-left p-4 bg-gray-50 border border-gray-200 rounded-lg dark:bg-gray-800 dark:border-gray-600">
                        <h4 class="font-bold text-lg text-gray-800 mb-2 dark:text-gray-100">AI Summary</h4>
                        <p class="text-gray-700 dark:text-gray-300">${summary}</p>
                    </div>
                ` : '';

                contentHtml = `
                    <div class="text-center">
                        <div class="mx-auto bg-green-100 rounded-full h-16 w-16 flex items-center justify-center">
                            ${SuccessIcon()}
                        </div>
                        <h3 class="mt-4 text-2xl font-semibold text-gray-800 dark:text-gray-100">Upload Successful!</h3>
                        <p class="text-gray-600 mt-2 dark:text-gray-400">Your report has been securely uploaded. Let our AI summarize it for you.</p>
                        
                        <div class="mt-6">
                            <button id="summarize-btn" ${isSummarizing ? 'disabled' : ''} class="w-full btn-primary font-semibold py-3 rounded-lg text-lg flex items-center justify-center disabled:opacity-60">
                                ${SparkleIcon()}
                                ${isSummarizing ? 'Summarizing...' : '✨ Summarize with AI'}
                            </button>
                        </div>

                        ${isSummarizing ? '<div class="mt-4 text-gray-500 animate-pulse dark:text-gray-400">Generating summary...</div>' : ''}
                        
                        ${summaryHtml}

                        <button id="back-to-reports-btn" class="mt-6 w-full text-center bg-gray-100 text-gray-800 font-semibold py-3 rounded-lg hover:bg-gray-200 transition-colors dark:bg-gray-600 dark:text-gray-100 dark:hover:bg-gray-500">Back to My Reports</button>
                    </div>
                `;
            }

            return `
                <div>
                    <h1 class="text-4xl font-bold text-gray-900 mb-8 dark:text-gray-100">Upload New Report</h1>
                    <div class="bg-white p-8 rounded-xl shadow-lg max-w-2xl mx-auto dark:bg-gray-700">
                        ${contentHtml}
                    </div>
                </div>
            `;
        }

        // --- 5. EVENT HANDLERS & LIFECYCLE HOOKS ---
        
        // --- CHAT LOGIC ---
        async function handleSendMessage() {
            const inputElement = document.getElementById('user-input');
            const userInput = inputElement.value.trim();
            if (!userInput || appState.chat.isAgentTyping) return;

            const newUserMessage = { id: Date.now(), sender: 'user', text: userInput };
            
            // 1. Update history and set typing indicator
            setState({ chatHistory: [...appState.chatHistory, newUserMessage] });
            setState({ isAgentTyping: true }, 'chat');
            inputElement.value = ''; // Clear input immediately
            
            const prompt = The user said: "${userInput}". Based on the conversation history, provide an empathetic response.;
            
            try {
                const agentResponseText = await callGeminiApi(prompt);
                
                const newAgentMessage = { id: Date.now() + 1, sender: 'agent', text: agentResponseText };
                
                // 2. Update history with agent response
                setState({ chatHistory: [...appState.chatHistory, newUserMessage, newAgentMessage] });
            } catch (error) {
                console.error("Gemini API call failed:", error);
                const errorMessage = { id: Date.now() + 1, sender: 'agent', text: "Sorry, I ran into an error. Please try again." };
                setState({ chatHistory: [...appState.chatHistory, newUserMessage, errorMessage] });
            } finally {
                // 3. Hide typing indicator
                setState({ isAgentTyping: false }, 'chat');
            }
        }
        
        function handleChatScroll() {
            const chatEndRef = document.getElementById('chat-end-ref');
            chatEndRef?.scrollIntoView({ behavior: 'smooth', block: 'end' });
        }

        // --- DASHBOARD LOGIC ---
        function handleToggleMode() { // Renamed for clarity
            const checkbox = document.getElementById('dark-mode-checkbox');
            if (checkbox) {
                const isChecked = checkbox.checked;
                // Toggle the state in the dashboard sub-object
                setState({ isDarkMode: isChecked }, 'dashboard');
                
                // Apply dark mode class to the body
                document.body.classList.toggle('dark', isChecked);
            }
        }


        // --- UPLOAD LOGIC ---

        function startUploadSimulation(file) {
            setState({ fileName: file.name, state: 'progress', progress: 0 }, 'upload');
            
            let currentProgress = 0;
            const interval = setInterval(() => {
                currentProgress += 10;
                setState({ progress: currentProgress }, 'upload');

                if (currentProgress >= 100) {
                    clearInterval(interval);
                    
                    // Add the new report to the reports array upon successful upload
                    const newReportId = Date.now().toString();
                    const newReport = {
                        id: newReportId,
                        name: file.name,
                        date: new Date().toLocaleDateString('en-US', { year: 'numeric', month: 'long', day: 'numeric' }),
                        status: 'Current'
                    };
                    setState({ reports: [...appState.reports, newReport] });

                    setTimeout(() => setState({ state: 'success' }, 'upload'), 500);
                }
            }, 150);
        }

        async function handleSummarize() {
            setState({ isSummarizing: true, summary: '' }, 'upload');
            
            const prompt = "Summarize the following report content in simple terms: [Mock Report Data]";
            const result = await callGeminiApi(prompt);
            
            setState({ summary: result, isSummarizing: false }, 'upload');
        }

        function handleDrop(e) {
            e.preventDefault();
            const files = e.dataTransfer.files;
            if (files && files[0]) {
                startUploadSimulation(files[0]);
            }
        }

        function handleFileChange(e) {
            const files = e.target.files;
            if (files && files[0]) {
                startUploadSimulation(files[0]);
            }
        }
        
        // --- AUTH LOGIC (Simple Navigation) ---
        function moveFocus(currentElement, nextId) {
            if (currentElement.value.length === currentElement.maxLength) {
                const nextElement = document.getElementById(nextId);
                if (nextElement) {
                    nextElement.focus();
                } else {
                    document.getElementById('verify-otp-btn')?.focus();
                }
            }
        }


        // --- 6. MAIN RENDERER ---

        function renderApp() {
            const appContainer = document.getElementById('app');
            const { currentPage } = appState;
            let contentHtml;
            const isAuthPage = ['login', 'signup', 'otp'].includes(currentPage);
            
            // Apply dark mode class on initial render if state says so
            if (appState.dashboard.isDarkMode) {
                document.body.classList.add('dark');
            } else {
                document.body.classList.remove('dark');
            }
            
            // Clear existing event listeners to prevent duplicates
            document.getElementById('app').innerHTML = ''; // Clear container first

            // Determine main layout
            if (isAuthPage) {
                switch (currentPage) {
                    case 'login': contentHtml = LoginPage(); break;
                    case 'signup': contentHtml = SignupPage(); break;
                    case 'otp': contentHtml = OTPPage(); break;
                }
                appContainer.innerHTML = contentHtml;
            } else {
                let mainContent = '';
                switch (currentPage) {
                    case 'dashboard': mainContent = DashboardPage(); break;
                    case 'chat': mainContent = ChatPage(); break;
                    case 'reports': mainContent = ReportsPage(); break;
                    case 'upload-report': mainContent = UploadReportPage(); break;
                    default: mainContent = DashboardPage(); break;
                }
                appContainer.innerHTML = `
                    <div class="flex h-screen">
                        ${Sidebar()}
                        <main id="main-content" class="flex-1 p-6 md:p-10 overflow-y-auto">
                            ${mainContent}
                        </main>
                    </div>
                `;
            }

            // --- Attach Event Listeners (React Component Did Mount equivalent) ---

            // General Navigation Listeners (Always active if rendered)
            const elements = [
                { id: 'nav-dashboard', page: 'dashboard' },
                { id: 'nav-chat', page: 'chat' },
                { id: 'nav-reports', page: 'reports' },
                { id: 'nav-logout', page: 'login' },
                { id: 'link-signup', page: 'signup' },
                { id: 'link-login', page: 'login' },
                { id: 'dash-upload-btn', page: 'upload-report' },
                { id: 'dash-chat-btn', page: 'chat' },
                { id: 'reports-upload-btn', page: 'upload-report' }, // Now targets both empty and table views
                { id: 'back-to-reports-btn', page: 'reports' },
                // Auth buttons
                { id: 'login-btn', page: 'dashboard' },
                { id: 'signup-btn', page: 'otp' },
                { id: 'verify-otp-btn', page: 'dashboard' }
            ];

            elements.forEach(item => {
                const el = document.getElementById(item.id);
                if (el) {
                    el.onclick = (e) => {
                        e.preventDefault();
                        navigateTo(item.page);
                    };
                }
            });

            // Page-specific listeners
            if (currentPage === 'dashboard') {
                const toggleElement = document.getElementById('dark-mode-checkbox');
                if (toggleElement) {
                    toggleElement.onchange = handleToggleMode;
                }
            }

            if (currentPage === 'chat') {
                setTimeout(handleChatScroll, 0); // Scroll after render

                const sendBtn = document.getElementById('send-btn');
                const userInput = document.getElementById('user-input');

                if (sendBtn) {
                    sendBtn.onclick = handleSendMessage;
                }
                if (userInput) {
                    userInput.onkeypress = (e) => {
                        if (e.key === 'Enter') {
                            handleSendMessage();
                        }
                    };
                }
            }
            
            if (currentPage === 'upload-report') {
                const uploadBox = document.getElementById('upload-box');
                const fileInput = document.getElementById('file-input');
                const summarizeBtn = document.getElementById('summarize-btn');

                if (uploadBox) {
                    uploadBox.addEventListener('dragover', (e) => e.preventDefault());
                    uploadBox.addEventListener('drop', handleDrop);
                    uploadBox.addEventListener('click', () => fileInput.click());
                }
                if (fileInput) {
                    fileInput.onchange = handleFileChange;
                }
                if (summarizeBtn) {
                    summarizeBtn.onclick = handleSummarize;
                }
            }
        }

        // --- 7. INITIALIZATION ---

        window.onload = function() {
            // Start the app and trigger initial data fetching simulation
            initializeAppState(); 
            renderApp();
        };

    </script>
</body>
</html>
