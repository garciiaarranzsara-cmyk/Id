# Id
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>I+D HUB - Plataforma de Innovación</title>
    <!-- Tailwind CSS para el diseño -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons para los iconos (Carga ligera) -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700;900&display=swap');
        
        :root {
            --bg-dark: #020617;
            --card-bg: #0f172a;
            --accent: #4f46e5;
        }

        body { 
            font-family: 'Inter', sans-serif; 
            background-color: var(--bg-dark); 
            color: #e2e8f0; 
            margin: 0; 
            overflow-x: hidden;
        }

        .sidebar-active { 
            background-color: var(--accent); 
            color: white; 
            box-shadow: 0 10px 15px -3px rgba(79, 70, 229, 0.3); 
        }

        .fade-in { animation: fadeIn 0.4s ease-out forwards; }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .glass { 
            background: rgba(255, 255, 255, 0.03); 
            backdrop-filter: blur(10px); 
            border: 1px solid rgba(255, 255, 255, 0.05); 
        }

        input:focus { ring: 2px solid var(--accent); outline: none; }
    </style>
</head>
<body>

    <!-- Contenedor de Autenticación -->
    <div id="login-screen" class="min-h-screen flex items-center justify-center p-4">
        <div class="max-w-md w-full bg-slate-900 border border-slate-800 rounded-[2.5rem] p-8 shadow-2xl text-center">
            <div class="bg-indigo-600/20 w-16 h-16 rounded-2xl flex items-center justify-center mx-auto mb-4 border border-indigo-500/30">
                <i data-lucide="lock" class="text-indigo-400 w-8 h-8"></i>
            </div>
            <h1 class="text-2xl font-black text-white italic uppercase tracking-tighter mb-2">Acceso I+D Corp</h1>
            <p class="text-slate-400 text-sm mb-8">Credenciales preestablecidas para Alex</p>
            
            <form id="login-form" class="space-y-4 text-left">
                <div>
                    <label class="text-xs font-bold text-slate-500 uppercase ml-2 block mb-1">Email Corporativo</label>
                    <input type="email" id="email" value="Alex@idcorp.com" class="w-full bg-slate-800 border border-slate-700 rounded-2xl px-4 py-3 text-white">
                </div>
                <div>
                    <label class="text-xs font-bold text-slate-500 uppercase ml-2 block mb-1">Contraseña</label>
                    <input type="password" id="password" value="idcorp2024" class="w-full bg-slate-800 border border-slate-700 rounded-2xl px-4 py-3 text-white">
                </div>
                <p id="login-error" class="text-rose-500 text-xs font-bold hidden">Credenciales incorrectas.</p>
                <button type="submit" class="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-black py-4 rounded-2xl shadow-lg flex items-center justify-center gap-2 uppercase tracking-widest text-sm mt-6">
                    Entrar al Ecosistema <i data-lucide="chevron-right" class="w-5 h-5"></i>
                </button>
            </form>
        </div>
    </div>

    <!-- Contenedor Principal de la App -->
    <div id="app-screen" class="min-h-screen hidden flex flex-col md:flex-row">
        <!-- Sidebar -->
        <aside class="w-full md:w-64 bg-slate-900 border-r border-slate-800 p-4 flex flex-col shrink-0">
            <div class="mb-10 p-2 text-center md:text-left">
                <h2 class="text-indigo-400 font-black italic text-2xl tracking-tighter uppercase leading-none">I+D HUB</h2>
            </div>
            <nav id="nav-links" class="flex-grow space-y-2">
                <button onclick="navigate('dashboard')" id="nav-dashboard" class="sidebar-btn w-full flex items-center gap-3 px-4 py-4 rounded-2xl font-bold text-sm transition-all sidebar-active">
                    <i data-lucide="map" class="w-5 h-5"></i> Dashboard
                </button>
                <button onclick="navigate('contrato')" id="nav-contrato" class="sidebar-btn w-full flex items-center gap-3 px-4 py-4 rounded-2xl font-bold text-sm transition-all text-slate-400 hover:bg-slate-800">
                    <i data-lucide="trending-up" class="w-5 h-5"></i> Contrato 3D
                </button>
                <button onclick="navigate('misiones')" id="nav-misiones" class="sidebar-btn w-full flex items-center gap-3 px-4 py-4 rounded-2xl font-bold text-sm transition-all text-slate-400 hover:bg-slate-800">
                    <i data-lucide="zap" class="w-5 h-5"></i> Misiones Pro
                </button>
                <button onclick="navigate('micropolix')" id="nav-micropolix" class="sidebar-btn w-full flex items-center gap-3 px-4 py-4 rounded-2xl font-bold text-sm transition-all text-slate-400 hover:bg-slate-800">
                    <i data-lucide="building-2" class="w-5 h-5"></i> Micropolix
                </button>
                <button onclick="navigate('bonos')" id="nav-bonos" class="sidebar-btn w-full flex items-center gap-3 px-4 py-4 rounded-2xl font-bold text-sm transition-all text-slate-400 hover:bg-slate-800">
                    <i data-lucide="gift" class="w-5 h-5"></i> Bonificaciones
                </button>
            </nav>
            
            <div class="mt-auto p-2 pt-6 border-t border-slate-800">
                <div class="bg-amber-500/10 border border-amber-500/20 rounded-2xl p-4 flex items-center gap-3 mb-4 text-amber-500">
                    <i data-lucide="coins" class="w-5 h-5"></i>
                    <span id="bio-credits-display" class="font-black text-xl">1250</span>
                    <span class="text-[10px] uppercase font-black opacity-60">Credits</span>
                </div>
                <button onclick="logout()" class="w-full flex items-center gap-3 px-4 py-3 text-rose-500 font-bold hover:bg-rose-500/10 rounded-xl transition-all">
                    <i data-lucide="log-out" class="w-5 h-5"></i>
                    <span class="text-xs uppercase tracking-widest">Cerrar Sesión</span>
                </button>
            </div>
        </aside>

        <!-- Área de Contenido -->
        <main class="flex-grow p-6 md:p-12 overflow-y-auto" id="main-content">
            <!-- El contenido se inyecta vía JS -->
        </main>
    </div>

    <script>
        // --- ESTADO GLOBAL ---
        let state = {
            isAuthenticated: false,
            activeTab: 'dashboard',
            coins: 1250,
            user: { name: "Alex I+D", dept: "Biotecnología" },
            doneDimensions: [false, false, false],
            currentMission: null
        };

        // --- LÓGICA DE NAVEGACIÓN Y RENDERIZADO ---
        function navigate(tab) {
            state.activeTab = tab;
            updateSidebar();
            renderContent();
        }

        function updateSidebar() {
            document.querySelectorAll('.sidebar-btn').forEach(btn => {
                btn.classList.remove('sidebar-active');
                btn.classList.add('text-slate-400');
            });
            const activeBtn = document.getElementById('nav-' + state.activeTab);
            if(activeBtn) {
                activeBtn.classList.add('sidebar-active');
                activeBtn.classList.remove('text-slate-400');
            }
        }

        function renderContent() {
            const container = document.getElementById('main-content');
            container.innerHTML = ''; // Limpiar
            
            let html = `
                <header class="mb-10 fade-in">
                    <h1 class="text-3xl md:text-4xl font-black text-white italic uppercase tracking-tighter leading-none mb-2">
                        ${getTitle(state.activeTab)}
                    </h1>
                    <p class="text-slate-500 font-bold uppercase text-[10px] md:text-xs tracking-widest">
                        ${state.user.name} • ${state.user.dept}
                    </p>
                </header>
                <div class="fade-in">
                    ${getViewHTML(state.activeTab)}
                </div>
            `;
            container.innerHTML = html;
            lucide.createIcons(); // Re-inicializar iconos
        }

        function getTitle(tab) {
            const titles = {
                dashboard: 'Ecosistema de Impacto',
                contrato: 'Dimensión 1: Contrato 3D',
                misiones: 'Dimensión 2: Misiones Pro',
                micropolix: 'Dimensión 3: Micropolix',
                bonos: 'Bonus Marketplace'
            };
            return titles[tab] || '';
        }

        function getViewHTML(tab) {
            switch(tab) {
                case 'dashboard':
                    return `
                        <div class="grid lg:grid-cols-3 gap-8">
                            <div class="lg:col-span-2 space-y-8">
                                <div class="bg-gradient-to-br from-indigo-600 to-indigo-800 rounded-[3rem] p-8 md:p-10 shadow-2xl relative overflow-hidden text-white">
                                    <div class="relative z-10 space-y-4">
                                        <h2 class="text-3xl md:text-4xl font-black italic uppercase leading-tight">Tu impacto cultural<br/>está creciendo</h2>
                                        <p class="text-indigo-100/80 max-w-md text-sm leading-relaxed">Has completado el 84% de tus hitos trimestrales. Desbloquea misiones Pro para conseguir Bio-Credits.</p>
                                        <button onclick="navigate('misiones')" class="bg-white text-indigo-600 px-8 py-3 rounded-xl font-black text-xs uppercase tracking-widest hover:scale-105 transition-all">Ir a Misiones</button>
                                    </div>
                                    <i data-lucide="zap" class="absolute right-[-40px] bottom-[-40px] opacity-10 rotate-12 w-48 h-48"></i>
                                </div>
                                <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                                    <div class="bg-slate-900 border border-slate-800 rounded-[2rem] p-8 text-center sm:text-left">
                                        <p class="text-slate-500 font-bold uppercase text-[10px] tracking-widest mb-2">Evolución</p>
                                        <p class="text-4xl font-black text-white leading-none">84%</p>
                                    </div>
                                    <div class="bg-slate-900 border border-slate-800 rounded-[2rem] p-8 text-center sm:text-left">
                                        <p class="text-slate-500 font-bold uppercase text-[10px] tracking-widest mb-2">Bio-Credits</p>
                                        <p class="text-4xl font-black text-white leading-none">${state.coins}</p>
                                    </div>
                                </div>
                            </div>
                            <div class="bg-slate-900/50 border border-slate-800 rounded-[3rem] p-8">
                                <h3 class="text-lg font-black text-white italic uppercase mb-6 flex items-center gap-2">
                                    <i data-lucide="mail" class="text-indigo-400 w-5 h-5"></i> Notificaciones
                                </h3>
                                <div class="space-y-4">
                                    <div class="p-4 bg-white/5 rounded-2xl border border-white/5">
                                        <p class="text-xs font-bold mb-1 uppercase text-indigo-300">Nueva Misión Flash</p>
                                        <p class="text-xs text-slate-400 leading-relaxed">Conecta con alguien de Logística y descubre su hobby secreto.</p>
                                    </div>
                                    <div class="p-4 border border-white/5 rounded-2xl opacity-50">
                                        <p class="text-xs font-bold mb-1 uppercase text-slate-400">Bonificación Canjeada</p>
                                        <p class="text-xs text-slate-500 leading-relaxed">Has recibido 50€ en tu Ticket Restaurante.</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    `;
                case 'contrato':
                    return `
                        <div class="space-y-8">
                            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 text-left">
                                ${renderDimCard(0, 'user', 'Visión Propia', 'indigo', '¿Cómo te ves hoy? Tu propósito y motivación personal.')}
                                ${renderDimCard(1, 'users', 'Visión Equipo', 'purple', '¿Cómo te ven? El impacto que generas en el ecosistema I+D.')}
                                ${renderDimCard(2, 'trending-up', 'Desarrollo', 'amber', '¿Cómo crecerás? Tu plan de carrera a 90 días.')}
                            </div>
                            <div class="bg-slate-900 border border-slate-800 rounded-[2.5rem] p-8 text-sm text-slate-400 leading-relaxed">
                                <h4 class="font-black text-white uppercase italic mb-2">¿Por qué el 3D es el nuevo estándar?</h4>
                                En I+D HUB, el talento tiene profundidad. El contrato 3D une lo que tú quieres, lo que tu equipo necesita y hacia dónde vamos. Ganarás 200 Bio-Credits por cada dimensión completada.
                            </div>
                        </div>
                    `;
                case 'misiones':
                    return `
                        <div class="max-w-2xl mx-auto bg-slate-900 border border-slate-800 rounded-[3rem] p-10 text-center">
                            <div class="bg-indigo-600/20 w-20 h-20 rounded-3xl flex items-center justify-center mx-auto mb-6">
                                <i data-lucide="zap" class="text-indigo-400 w-10 h-10"></i>
                            </div>
                            <h2 class="text-3xl font-black text-white italic uppercase mb-2">Misiones Flash</h2>
                            <p class="text-slate-400 text-sm mb-10">Conecta con compañeros de otros departamentos mediante misiones rápidas enviadas por correo.</p>
                            ${state.currentMission ? `
                                <div class="bg-indigo-500/10 border border-indigo-500/20 rounded-[2rem] p-8 mb-6">
                                    <p class="text-xs font-black text-indigo-400 uppercase tracking-widest mb-4 italic">Misión Asignada</p>
                                    <p class="text-xl text-white font-bold mb-6">Compañero: <span class="text-indigo-300">${state.currentMission.n}</span><br>Objetivo: <span class="text-indigo-300 italic">Descubrir su "${state.currentMission.t}"</span></p>
                                    <button onclick="completeMission()" class="bg-emerald-500 text-white px-8 py-3 rounded-xl font-black text-xs uppercase shadow-lg">Misión Cumplida +100</button>
                                </div>
                            ` : `
                                <button onclick="generateMission()" class="bg-indigo-600 hover:bg-indigo-500 text-white px-10 py-5 rounded-3xl font-black text-lg uppercase shadow-xl">Solicitar Nueva Misión</button>
                            `}
                        </div>
                    `;
                case 'micropolix':
                    return `
                        <div class="max-w-3xl mx-auto bg-slate-900 border border-slate-800 rounded-[3rem] p-10">
                            <div class="flex items-center gap-4 mb-8">
                                <i data-lucide="building-2" class="text-amber-500 w-8 h-8"></i>
                                <h2 class="text-2xl font-black text-white italic uppercase tracking-tighter text-left">Micropolix: Inmersión Técnica</h2>
                            </div>
                            <form id="micro-form" onsubmit="handleMicro(event)" class="space-y-6 text-left">
                                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                                    <div>
                                        <label class="text-[10px] font-black text-slate-500 uppercase ml-2 block mb-2">Área a conocer</label>
                                        <select class="w-full bg-slate-800 border border-slate-700 rounded-2xl px-4 py-3 text-white text-sm">
                                            <option>Ingeniería de Datos</option>
                                            <option>Procesos Químicos</option>
                                            <option>Desarrollo Software</option>
                                        </select>
                                    </div>
                                    <div>
                                        <label class="text-[10px] font-black text-slate-500 uppercase ml-2 block mb-2">Compañero Referente</label>
                                        <input type="text" placeholder="Nombre completo" class="w-full bg-slate-800 border border-slate-700 rounded-2xl px-4 py-3 text-white text-sm" required>
                                    </div>
                                </div>
                                <p class="text-[10px] text-slate-500 italic">Inmersión semestral para transferencia de conocimiento. No otorga Bio-Credits directos.</p>
                                <button type="submit" class="w-full bg-amber-500 text-slate-900 font-black py-4 rounded-2xl uppercase text-sm tracking-widest shadow-lg hover:bg-amber-400">Enviar Formulario de Inmersión</button>
                            </form>
                            <div id="micro-success" class="hidden text-center py-6">
                                <i data-lucide="check-circle-2" class="text-emerald-500 w-16 h-16 mx-auto mb-4"></i>
                                <p class="font-bold">Solicitud enviada con éxito.</p>
                            </div>
                        </div>
                    `;
                case 'bonos':
                    return `
                        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 text-center">
                            ${renderBono('50€ Ticket Restaurante', 1000, 'utensils')}
                            ${renderBono('Tarde Viernes Libre', 2000, 'clock')}
                            ${renderBono('Día Cumpleaños Extra', 3000, 'cake')}
                            ${renderBono('Formación Pro I+D', 1500, 'graduation-cap')}
                            ${renderBono('Material Premium', 1200, 'zap')}
                            ${renderBono('Suscripción Científica', 800, 'search')}
                        </div>
                    `;
                default: return '';
            }
        }

        // --- FUNCIONES DE SOPORTE ---
        function renderDimCard(idx, icon, title, color, desc) {
            const isDone = state.doneDimensions[idx];
            return `
                <div class="p-8 rounded-[2.5rem] border ${isDone ? 'bg-emerald-500/5 border-emerald-500/20' : 'bg-slate-900 border-slate-800'}">
                    <i data-lucide="${icon}" class="text-${color}-400 mb-6 w-10 h-10"></i>
                    <h3 class="text-xl font-black text-white uppercase italic mb-2">${title}</h3>
                    <p class="text-slate-400 text-xs leading-relaxed mb-6">${desc}</p>
                    <button onclick="completeDimension(${idx})" ${isDone ? 'disabled' : ''} 
                        class="w-full py-3 rounded-xl font-black text-[10px] uppercase tracking-widest ${isDone ? 'bg-emerald-500 text-white' : 'bg-indigo-600 text-white'}">
                        ${isDone ? 'Completado +200' : 'Completar'}
                    </button>
                </div>
            `;
        }

        function renderBono(name, cost, icon) {
            const canBuy = state.coins >= cost;
            return `
                <div class="bg-slate-900 border border-slate-800 rounded-[2.5rem] p-8 flex flex-col h-full items-center">
                    <div class="bg-indigo-500/10 w-14 h-14 rounded-2xl flex items-center justify-center mb-6 text-indigo-400">
                        <i data-lucide="${icon}" class="w-6 h-6"></i>
                    </div>
                    <h4 class="text-white font-black uppercase italic text-sm mb-4 leading-tight flex-grow">${name}</h4>
                    <p class="text-amber-500 font-black text-xs mb-6 flex items-center gap-2">
                        <i data-lucide="coins" class="w-3 h-3"></i> ${cost} Bio-Credits
                    </p>
                    <button onclick="buyBono(${cost})" ${!canBuy ? 'disabled' : ''} 
                        class="w-full py-3 rounded-xl font-black text-[10px] uppercase ${canBuy ? 'bg-indigo-600 text-white shadow-lg' : 'bg-slate-800 text-slate-600'}">
                        ${canBuy ? 'Canjear' : 'Faltan Créditos'}
                    </button>
                </div>
            `;
        }

        // --- ACCIONES DE USUARIO ---
        function completeDimension(idx) {
            state.doneDimensions[idx] = true;
            addCoins(200);
            renderContent();
        }

        function generateMission() {
            const names = ["Lucía (IT)", "Marc (Legal)", "Sara (Logística)"];
            const tasks = ["color favorito", "hobby secreto", "canción favorita"];
            state.currentMission = {
                n: names[Math.floor(Math.random() * names.length)],
                t: tasks[Math.floor(Math.random() * tasks.length)]
            };
            renderContent();
        }

        function completeMission() {
            state.currentMission = null;
            addCoins(100);
            renderContent();
        }

        function handleMicro(e) {
            e.preventDefault();
            document.getElementById('micro-form').classList.add('hidden');
            document.getElementById('micro-success').classList.remove('hidden');
            lucide.createIcons();
        }

        function buyBono(cost) {
            if(state.coins >= cost) {
                state.coins -= cost;
                updateCreditsUI();
                renderContent();
            }
        }

        function addCoins(amount) {
            state.coins += amount;
            updateCreditsUI();
        }

        function updateCreditsUI() {
            document.getElementById('bio-credits-display').innerText = state.coins;
        }

        function logout() {
            state.isAuthenticated = false;
            document.getElementById('app-screen').classList.add('hidden');
            document.getElementById('login-screen').classList.remove('hidden');
        }

        // --- LOGIN ---
        document.getElementById('login-form').onsubmit = (e) => {
            e.preventDefault();
            const mail = document.getElementById('email').value.toLowerCase();
            const pass = document.getElementById('password').value;

            if(mail === 'alex@idcorp.com' && pass === 'idcorp2024') {
                state.isAuthenticated = true;
                document.getElementById('login-screen').classList.add('hidden');
                document.getElementById('app-screen').classList.remove('hidden');
                renderContent();
            } else {
                document.getElementById('login-error').classList.remove('hidden');
            }
        };

        // Inicializar iconos al cargar
        window.onload = () => lucide.createIcons();
    </script>
</body>
</html>
