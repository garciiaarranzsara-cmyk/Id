# Id
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>I+D HUB - Plataforma de Innovación</title>
    <!-- Tailwind CSS para el diseño -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- React y Babel para ejecutar la lógica en un solo archivo -->
    <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <!-- Lucide Icons para los iconos -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700;900&display=swap');
        body { 
            font-family: 'Inter', sans-serif; 
            background-color: #0f172a; 
            color: #e2e8f0; 
            margin: 0; 
        }
        .glass { 
            background: rgba(255, 255, 255, 0.03); 
            backdrop-filter: blur(10px); 
            border: 1px solid rgba(255, 255, 255, 0.05); 
        }
        .sidebar-active { 
            background-color: #4f46e5; 
            color: white; 
            box-shadow: 0 10px 15px -3px rgba(79, 70, 229, 0.3); 
        }
        /* Animaciones */
        .fade-in { animation: fadeIn 0.5s ease-out; }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        const { useState, useEffect } = React;

        // Componente de Icono para Lucide
        const Icon = ({ name, size = 20, className = "" }) => {
            useEffect(() => {
                if (window.lucide) {
                    window.lucide.createIcons();
                }
            }, [name]);
            return <i data-lucide={name} style={{ width: size, height: size }} className={className}></i>;
        };

        const App = () => {
            const [isAuthenticated, setIsAuthenticated] = useState(false);
            const [activeTab, setActiveTab] = useState('dashboard');
            const [coins, setCoins] = useState(1250);
            const [user, setUser] = useState({ name: "Alex I+D", role: "Investigador Senior", dept: "Biotecnología" });

            // Credenciales Demo actualizadas
            const [email, setEmail] = useState('Alex@idcorp.com');
            const [password, setPassword] = useState('idcorp2024');

            const handleLogin = (e) => {
                e.preventDefault();
                // Permitir acceso con las credenciales establecidas
                if (email.toLowerCase() === 'alex@idcorp.com' && password === 'idcorp2024') {
                    setIsAuthenticated(true);
                } else {
                    // En un entorno real se mostraría un error en la UI, aquí permitimos el login para la demo
                    setIsAuthenticated(true);
                }
            };

            if (!isAuthenticated) {
                return (
                    <div className="min-h-screen flex items-center justify-center p-4 bg-[#020617]">
                        <div className="max-w-md w-full bg-slate-900 border border-slate-800 rounded-[2.5rem] p-8 shadow-2xl fade-in text-center">
                            <div className="bg-indigo-600/20 w-16 h-16 rounded-2xl flex items-center justify-center mx-auto mb-4 border border-indigo-500/30">
                                <Icon name="lock" size={32} className="text-indigo-400" />
                            </div>
                            <h1 className="text-2xl font-black text-white italic uppercase tracking-tighter mb-2">Acceso I+D Corp</h1>
                            <p className="text-slate-400 text-sm mb-8">Credenciales de Alex actualizadas</p>
                            
                            <form onSubmit={handleLogin} className="space-y-4 text-left">
                                <div>
                                    <label className="text-xs font-bold text-slate-500 uppercase ml-2 block mb-1">Email Corporativo</label>
                                    <input 
                                        type="email" 
                                        value={email} 
                                        onChange={e => setEmail(e.target.value)} 
                                        className="w-full bg-slate-800 border border-slate-700 rounded-2xl px-4 py-3 text-white outline-none focus:ring-2 focus:ring-indigo-500" 
                                    />
                                </div>
                                <div>
                                    <label className="text-xs font-bold text-slate-500 uppercase ml-2 block mb-1">Contraseña</label>
                                    <input 
                                        type="password" 
                                        value={password} 
                                        onChange={e => setPassword(e.target.value)} 
                                        className="w-full bg-slate-800 border border-slate-700 rounded-2xl px-4 py-3 text-white outline-none focus:ring-2 focus:ring-indigo-500" 
                                    />
                                </div>
                                <button type="submit" className="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-black py-4 rounded-2xl shadow-lg transition-all flex items-center justify-center gap-2 uppercase tracking-widest text-sm mt-6">
                                    Entrar al Ecosistema <Icon name="chevron-right" size={18} />
                                </button>
                            </form>
                        </div>
                    </div>
                );
            }

            return (
                <div className="min-h-screen flex flex-col md:flex-row">
                    {/* Sidebar */}
                    <aside className="w-full md:w-64 bg-slate-900 border-r border-slate-800 p-4 flex flex-col">
                        <div className="mb-10 p-2">
                            <h2 className="text-indigo-400 font-black italic text-2xl tracking-tighter">I+D HUB</h2>
                        </div>
                        <nav className="flex-grow space-y-2">
                            {[
                                { id: 'dashboard', label: 'Dashboard', icon: 'map' },
                                { id: 'contrato', label: 'Contrato 3D', icon: 'trending-up' },
                                { id: 'misiones', label: 'Misiones Pro', icon: 'zap' },
                                { id: 'micropolix', label: 'Micropolix', icon: 'building-2' },
                                { id: 'bonos', label: 'Bonificaciones', icon: 'gift' }
                            ].map(item => (
                                <button 
                                    key={item.id}
                                    onClick={() => setActiveTab(item.id)}
                                    className={`w-full flex items-center gap-3 px-4 py-4 rounded-2xl font-bold text-sm transition-all ${activeTab === item.id ? 'sidebar-active' : 'text-slate-400 hover:bg-slate-800'}`}
                                >
                                    <Icon name={item.icon} size={20} />
                                    {item.label}
                                </button>
                            ))}
                        </nav>
                        <div className="mt-auto p-2 pt-6 border-t border-slate-800">
                            <div className="bg-amber-500/10 border border-amber-500/20 rounded-2xl p-4 flex items-center gap-3 mb-4 text-amber-500">
                                <Icon name="coins" size={20} />
                                <span className="font-black text-xl">{coins}</span>
                                <span className="text-[10px] uppercase font-black opacity-60">Credits</span>
                            </div>
                            <button onClick={() => setIsAuthenticated(false)} className="w-full flex items-center gap-3 px-4 py-3 text-rose-500 font-bold hover:bg-rose-500/10 rounded-xl transition-all">
                                <Icon name="log-out" size={20} />
                                <span className="text-xs uppercase tracking-widest">Cerrar Sesión</span>
                            </button>
                        </div>
                    </aside>

                    {/* Content Area */}
                    <main className="flex-grow p-6 md:p-12 overflow-y-auto bg-[#020617]">
                        <header className="mb-10 flex justify-between items-end">
                            <div className="fade-in">
                                <h1 className="text-4xl font-black text-white italic uppercase tracking-tighter leading-none mb-2">
                                    {activeTab === 'dashboard' && 'Ecosistema de Impacto'}
                                    {activeTab === 'contrato' && 'Dimensión 1: Contrato 3D'}
                                    {activeTab === 'misiones' && 'Dimensión 2: Misiones Pro'}
                                    {activeTab === 'micropolix' && 'Dimensión 3: Micropolix'}
                                    {activeTab === 'bonos' && 'Bonus Marketplace'}
                                </h1>
                                <p className="text-slate-500 font-bold uppercase text-xs tracking-widest">{user.name} • {user.dept}</p>
                            </div>
                        </header>

                        <div className="fade-in">
                            {activeTab === 'dashboard' && <DashboardView setTab={setActiveTab} coins={coins} />}
                            {activeTab === 'contrato' && <Contrato3DView updateCoins={setCoins} />}
                            {activeTab === 'misiones' && <MisionesProView updateCoins={setCoins} />}
                            {activeTab === 'micropolix' && <MicropolixView />}
                            {activeTab === 'bonos' && <BonosView currentCoins={coins} updateCoins={setCoins} />}
                        </div>
                    </main>
                </div>
            );
        };

        const DashboardView = ({ setTab, coins }) => (
            <div className="grid lg:grid-cols-3 gap-8">
                <div className="lg:col-span-2 space-y-8">
                    <div className="bg-gradient-to-br from-indigo-600 to-indigo-800 rounded-[3rem] p-10 shadow-2xl relative overflow-hidden text-white">
                        <div className="relative z-10 space-y-4">
                            <h2 className="text-4xl font-black italic uppercase leading-none">Tu impacto cultural<br/>está creciendo</h2>
                            <p className="text-indigo-100/80 max-w-md text-sm">Has completado el 84% de tus hitos trimestrales. Desbloquea misiones Pro para conseguir Bio-Credits.</p>
                            <button onClick={() => setTab('misiones')} className="bg-white text-indigo-600 px-8 py-3 rounded-xl font-black text-xs uppercase tracking-widest hover:scale-105 transition-all">Ir a Misiones</button>
                        </div>
                        <Icon name="zap" size={200} className="absolute right-[-40px] bottom-[-40px] opacity-10 rotate-12" />
                    </div>
                    <div className="grid grid-cols-2 gap-6">
                        <div className="bg-slate-900 border border-slate-800 rounded-[2rem] p-8">
                            <div className="flex justify-between items-center mb-2">
                                <p className="text-slate-500 font-bold uppercase text-[10px] tracking-widest">Evolución</p>
                                <Icon name="trophy" size={16} className="text-amber-500" />
                            </div>
                            <p className="text-4xl font-black text-white leading-none">84%</p>
                        </div>
                        <div className="bg-slate-900 border border-slate-800 rounded-[2rem] p-8">
                            <div className="flex justify-between items-center mb-2">
                                <p className="text-slate-500 font-bold uppercase text-[10px] tracking-widest">Bio-Credits</p>
                                <Icon name="coins" size={16} className="text-amber-500" />
                            </div>
                            <p className="text-4xl font-black text-white leading-none">{coins}</p>
                        </div>
                    </div>
                </div>
                <div className="bg-slate-900/50 border border-slate-800 rounded-[3rem] p-8">
                    <h3 className="text-lg font-black text-white italic uppercase mb-6 flex items-center gap-2">
                        <Icon name="mail" size={18} className="text-indigo-400" /> Notificaciones
                    </h3>
                    <div className="space-y-4">
                        <div className="p-4 bg-white/5 rounded-2xl border border-white/5">
                            <p className="text-xs font-bold mb-1 uppercase text-indigo-300">Nueva Misión Flash</p>
                            <p className="text-xs text-slate-400 leading-relaxed">Conecta con alguien de Logística y descubre su hobby secreto.</p>
                        </div>
                        <div className="p-4 border border-white/5 rounded-2xl opacity-50">
                            <p className="text-xs font-bold mb-1 uppercase">Bonificación Canjeada</p>
                            <p className="text-xs text-slate-500">Has recibido 50€ en tu Ticket Restaurante.</p>
                        </div>
                    </div>
                </div>
            </div>
        );

        const Contrato3DView = ({ updateCoins }) => {
            const [done, setDone] = useState([false, false, false]);
            const complete = (i) => {
                if(!done[i]) {
                    const next = [...done]; next[i] = true; setDone(next);
                    updateCoins(c => c + 200);
                }
            };
            return (
                <div className="space-y-8">
                    <div className="grid md:grid-cols-3 gap-6">
                        <DimensionCard 
                            icon="user" title="Visión Propia" color="indigo"
                            desc="Define cómo te ves hoy en tu puesto, tus motivaciones y propósito personal."
                            done={done[0]} onAction={() => complete(0)} 
                        />
                        <DimensionCard 
                            icon="users" title="Visión Equipo" color="purple"
                            desc="El impacto que generas en los demás. Cómo te percibe tu equipo de I+D."
                            done={done[1]} onAction={() => complete(1)} 
                        />
                        <DimensionCard 
                            icon="trending-up" title="Desarrollo" color="amber"
                            desc="Tu plan de crecimiento a 90 días. Desbloquea nuevas habilidades técnicas."
                            done={done[2]} onAction={() => complete(2)} 
                        />
                    </div>
                    <div className="bg-slate-900 border border-slate-800 rounded-[2.5rem] p-8 text-sm leading-relaxed text-slate-400">
                        <h4 className="font-black text-white uppercase italic mb-2">¿Por qué hablamos de 3 Dimensiones?</h4>
                        En nuestra empresa de I+D, no eres una pieza estática. El Contrato 3D asegura que tu visión personal, la percepción de tu equipo y tu plan de carrera estén alineados. Cada dimensión completada te otorga 200 Bio-Credits para canjear por beneficios reales.
                    </div>
                </div>
            );
        };

        const DimensionCard = ({ icon, title, desc, done, onAction, color }) => (
            <div className={`p-8 rounded-[2.5rem] border transition-all ${done ? 'bg-emerald-500/5 border-emerald-500/20' : 'bg-slate-900 border-slate-800'}`}>
                <Icon name={icon} size={40} className={`text-${color}-400 mb-6`} />
                <h3 className="text-xl font-black text-white uppercase italic mb-2">{title}</h3>
                <p className="text-slate-400 text-xs leading-relaxed mb-6">{desc}</p>
                <button 
                    onClick={onAction} 
                    disabled={done}
                    className={`w-full py-3 rounded-xl font-black text-[10px] uppercase tracking-widest transition-all ${done ? 'bg-emerald-500 text-white' : 'bg-indigo-600 hover:bg-indigo-500 text-white'}`}
                >
                    {done ? 'Completado +200' : 'Completar Dimensión'}
                </button>
            </div>
        );

        const MisionesProView = ({ updateCoins }) => {
            const [m, setM] = useState(null);
            const [load, setLoad] = useState(false);
            const roll = () => {
                setLoad(true);
                setTimeout(() => {
                    const names = ["Lucía (IT)", "Marc (Legal)", "Sara (Marketing)", "Hugo (Procesos)"];
                    const tasks = ["color favorito", "hobby secreto", "canción para trabajar", "mayor logro del año"];
                    setM({ n: names[Math.floor(Math.random()*4)], t: tasks[Math.floor(Math.random()*4)] });
                    setLoad(false);
                }, 1000);
            };
            return (
                <div className="max-w-2xl mx-auto bg-slate-900 border border-slate-800 rounded-[3rem] p-10 text-center">
                    <div className="bg-indigo-600/20 w-20 h-20 rounded-3xl flex items-center justify-center mx-auto mb-6">
                        <Icon name="zap" size={40} className="text-indigo-400" />
                    </div>
                    <h2 className="text-3xl font-black text-white italic uppercase mb-2">Misiones Flash</h2>
                    <p className="text-slate-400 text-sm mb-10">Conecta con compañeros fuera de tu área mediante misiones asignadas aleatoriamente por correo electrónico.</p>
                    
                    {m ? (
                        <div className="bg-indigo-500/10 border border-indigo-500/20 rounded-[2rem] p-8 mb-6 animate-in zoom-in">
                            <p className="text-xs font-black text-indigo-400 uppercase tracking-widest mb-4 italic">Misión Asignada</p>
                            <p className="text-xl text-white font-bold mb-6 leading-relaxed">
                                Tu compañero es <span className="text-indigo-300">{m.n}</span>. <br/>
                                Descubre su <span className="text-indigo-300 italic">"{m.t}"</span>.
                            </p>
                            <button onClick={() => { updateCoins(c => c+100); setM(null); }} className="bg-emerald-500 text-white px-8 py-3 rounded-xl font-black text-xs uppercase">Completar +100</button>
                        </div>
                    ) : (
                        <button onClick={roll} disabled={load} className="bg-indigo-600 hover:bg-indigo-500 text-white px-10 py-5 rounded-3xl font-black text-lg uppercase shadow-xl transition-all">
                            {load ? "Generando..." : "Solicitar Nueva Misión"}
                        </button>
                    )}
                </div>
            );
        };

        const MicropolixView = () => {
            const [sent, setSent] = useState(false);
            return (
                <div className="max-w-3xl mx-auto bg-slate-900 border border-slate-800 rounded-[3rem] p-10">
                    <div className="flex items-center gap-4 mb-8">
                        <Icon name="building-2" size={32} className="text-amber-500" />
                        <h2 className="text-2xl font-black text-white italic uppercase tracking-tighter">Micropolix: Inmersión Técnica</h2>
                    </div>
                    {sent ? (
                        <div className="text-center py-10 fade-in">
                            <Icon name="check-circle-2" size={64} className="text-emerald-500 mx-auto mb-4" />
                            <h3 className="text-2xl font-black text-white italic uppercase mb-2">Solicitud Enviada</h3>
                            <p className="text-slate-400 text-sm">Te avisaremos cuando tu compañero acepte la visita semestral.</p>
                            <button onClick={() => setSent(false)} className="mt-6 text-indigo-400 text-xs font-bold uppercase underline">Nueva Solicitud</button>
                        </div>
                    ) : (
                        <form onSubmit={(e) => { e.preventDefault(); setSent(true); }} className="space-y-6 text-left">
                            <div className="grid md:grid-cols-2 gap-6">
                                <div>
                                    <label className="text-[10px] font-black text-slate-500 uppercase ml-2 mb-2 block">Área a conocer</label>
                                    <select className="w-full bg-slate-800 border border-slate-700 rounded-2xl px-4 py-3 text-white text-sm outline-none">
                                        <option>Ingeniería de Datos</option>
                                        <option>Procesos Químicos</option>
                                        <option>Desarrollo de Software</option>
                                        <option>Diseño Industrial</option>
                                    </select>
                                </div>
                                <div>
                                    <label className="text-[10px] font-black text-slate-500 uppercase ml-2 mb-2 block">Compañero Referente</label>
                                    <input type="text" placeholder="Nombre completo" className="w-full bg-slate-800 border border-slate-700 rounded-2xl px-4 py-3 text-white text-sm outline-none" required />
                                </div>
                            </div>
                            <div>
                                <label className="text-[10px] font-black text-slate-500 uppercase ml-2 mb-2 block">Motivo de la visita</label>
                                <textarea className="w-full bg-slate-800 border border-slate-700 rounded-2xl px-4 py-3 text-white text-sm outline-none" rows="3" placeholder="¿Qué acciones específicas quieres observar?"></textarea>
                            </div>
                            <p className="text-[10px] text-slate-500 italic">Esta actividad es semestral y no otorga Bio-Credits directos, se enfoca en la transferencia de conocimiento.</p>
                            <button type="submit" className="w-full bg-amber-500 text-slate-900 font-black py-4 rounded-2xl uppercase text-sm tracking-widest shadow-lg shadow-amber-500/10 transition-all hover:bg-amber-400">Enviar Formulario de Inmersión</button>
                        </form>
                    )}
                </div>
            );
        };

        const BonosView = ({ currentCoins, updateCoins }) => {
            const list = [
                { id:1, n: "50€ Ticket Restaurante", c: 1000, i: "utensils" },
                { id:2, n: "Tarde de Viernes Libre", c: 2000, i: "clock" },
                { id:3, n: "Formación Técnica Pro", c: 1500, i: "graduation-cap" },
                { id:4, n: "Día Cumpleaños Libre Extra", c: 3000, i: "cake" },
                { id:5, n: "Material I+D Premium", c: 1200, i: "zap" },
                { id:6, n: "Suscripción Científica", c: 800, i: "search" }
            ];
            const buy = (cost) => { if(currentCoins >= cost) updateCoins(c => c - cost); };
            return (
                <div className="grid md:grid-cols-3 gap-6">
                    {list.map(b => (
                        <div key={b.id} className="bg-slate-900 border border-slate-800 rounded-[2.5rem] p-8 text-center transition-all hover:border-indigo-500/30">
                            <div className="bg-indigo-500/10 w-16 h-16 rounded-3xl flex items-center justify-center mx-auto mb-6 text-indigo-400">
                                <Icon name={b.i} size={28} />
                            </div>
                            <h4 className="text-white font-black uppercase italic text-sm mb-4 leading-tight">{b.n}</h4>
                            <p className="text-amber-500 font-black text-xs mb-6 flex items-center justify-center gap-2">
                                <Icon name="coins" size={12} /> {b.c} Bio-Credits
                            </p>
                            <button 
                                onClick={() => buy(b.c)} 
                                disabled={currentCoins < b.c}
                                className={`w-full py-3 rounded-xl font-black text-[10px] uppercase tracking-widest transition-all ${currentCoins >= b.c ? 'bg-indigo-600 hover:bg-indigo-500 text-white shadow-lg' : 'bg-slate-800 text-slate-600 cursor-not-allowed'}`}
                            >
                                {currentCoins >= b.c ? 'Canjear Bono' : 'Faltan Créditos'}
                            </button>
                        </div>
                    ))}
                </div>
            );
        };

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>
</html>
