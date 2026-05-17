<html>

<head>
    <style>
      @charset "UTF-8";

@import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800;900&display=swap');

body {
    font-family: 'Plus Jakarta Sans', sans-serif;
    background-color: #050811;
    color: #e2e8f0;
    overflow-x: hidden;
}

#particles-js {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
    pointer-events: none;
}

.glass {
    background: rgba(15, 23, 42, 0.45);
    backdrop-filter: blur(24px);
    -webkit-backdrop-filter: blur(24px);
    border: 1px solid rgba(139, 92, 246, 0.15);
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
    transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}

.glass:hover {
    border-color: rgba(139, 92, 246, 0.4);
    box-shadow: 0 12px 40px rgba(139, 92, 246, 0.15);
}

.scroll-reveal {
    opacity: 0;
    transform: translateY(40px);
    transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}
.scroll-reveal.active {
    opacity: 1;
    transform: translateY(0);
}

/* Slider Customizado */
.neon-slider {
    -webkit-appearance: none;
    appearance: none;
    background: transparent;
    cursor: pointer;
}

.neon-slider::-webkit-slider-runnable-track {
    width: 100%;
    height: 8px;
    background: #1e293b;
    border-radius: 10px;
    border: 1px solid #334155;
}

.neon-slider::-webkit-slider-thumb {
    -webkit-appearance: none;
    height: 24px;
    width: 24px;
    border-radius: 50%;
    background: #8b5cf6;
    margin-top: -9px;
    box-shadow: 0 0 15px #8b5cf6, 0 0 30px #a78bfa;
    transition: transform 0.2s ease;
}

.neon-slider::-webkit-slider-thumb:hover {
    transform: scale(1.2);
}

/* Paginação da Tabela */
.page-link {
    cursor: pointer;
    padding: 6px 14px;
    border-radius: 8px;
    font-size: 12px;
    font-weight: 800;
    transition: all 0.3s ease;
    border: 1px solid transparent;
}
.page-link.active {
    background: #8b5cf6;
    color: white;
    box-shadow: 0 0 10px rgba(139, 92, 246, 0.4);
}
.page-link:hover:not(.active) {
    background: rgba(139, 92, 246, 0.15);
    border-color: rgba(139, 92, 246, 0.3);
    color: #a78bfa;
}

::-webkit-scrollbar {
    width: 8px;
}
::-webkit-scrollbar-track {
    background: #050811;
}
::-webkit-scrollbar-thumb {
    background: #4c1d95;
    border-radius: 10px;
}
::-webkit-scrollbar-thumb:hover {
    background: #8b5cf6;
}

@media print {
    .no-print { display: none !important; }
    body { background: #0f172a !important; color: white !important; }
    .glass { background: #0f172a !important; border: 1px solid #334155 !important; }
}

    </style>
</head>

<body>

    <!DOCTYPE html>
<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SleepInsights PRO | Dashboard 2026</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: { 400: '#a78bfa', 500: '#8b5cf6', 600: '#7c3aed' },
                        dark: '#050811',
                        surface: '#0f172a'
                    }
                }
            }
        }
    </script>
    
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <link rel="stylesheet" href="style.css">
</head>
<body class="bg-dark text-slate-200 antialiased font-sans">

    <canvas id="particles-js"></canvas>

    <div id="qr-modal" class="fixed inset-0 z-[999] hidden flex items-center justify-center bg-black/80 backdrop-blur-sm transition-opacity opacity-0">
        <div class="glass p-8 rounded-3xl flex flex-col items-center relative max-w-sm mx-4 transform scale-95 transition-transform duration-300" id="qr-content">
            <button onclick="closeQR()" class="absolute top-4 right-4 text-slate-400 hover:text-white transition-colors">
                <i data-lucide="x" class="w-6 h-6"></i>
            </button>
            <h3 class="text-xl font-bold mb-2">Acesse o Projeto</h3>
            <p class="text-xs text-slate-400 mb-6 text-center">Escaneie para abrir o SleepInsights no seu celular</p>
            <div class="bg-white p-4 rounded-xl mb-4">
                <img src="https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=https://seusite.com" alt="QR Code" class="w-48 h-48 rounded-lg">
            </div>
            <p class="text-[10px] uppercase tracking-widest text-brand-500 font-bold">Feira de Ciências 2026</p>
        </div>
    </div>

    <nav class="sticky top-4 z-50 px-6 py-4 glass no-print mx-4 rounded-2xl flex justify-between items-center shadow-2xl">
        <div class="flex items-center gap-3">
            <div class="p-2 bg-brand-600 rounded-lg shadow-[0_0_15px_rgba(139,92,246,0.5)]">
                <i data-lucide="moon" class="text-white"></i>
            </div>
            <div>
                <h1 class="text-xl font-bold tracking-tight">Sleep<span class="text-brand-500">Insights</span></h1>
                <p class="text-[9px] text-slate-500 font-bold uppercase tracking-[0.2em]">Equipe PRO • 2026</p>
            </div>
        </div>

        <div class="flex items-center gap-4">
            <button onclick="openQR()" class="flex items-center gap-2 hover:bg-slate-800 px-4 py-2 rounded-xl text-xs font-bold transition-all text-slate-300">
                <i data-lucide="qr-code" class="w-4 h-4"></i> <span class="hidden md:inline">COMPARTILHAR</span>
            </button>
            <div class="h-6 w-[1px] bg-slate-800 mx-1"></div>
            <button onclick="exportCSV()" class="bg-brand-600 hover:bg-brand-500 px-4 py-2 rounded-xl text-xs font-bold transition-all shadow-lg shadow-brand-500/20 hover:scale-105 active:scale-95">
                BAIXAR DADOS
            </button>
        </div>
    </nav>

    <main class="container mx-auto px-4 pb-20 mt-12">
        
        <header class="text-center mb-16 scroll-reveal">
            <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-brand-500/10 border border-brand-500/20 text-brand-400 text-[10px] font-bold uppercase mb-6">
                <span class="relative flex h-2 w-2">
                    <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-brand-400 opacity-75"></span>
                    <span class="relative inline-flex rounded-full h-2 w-2 bg-brand-500"></span>
                </span>
                Análise Biológica e Acadêmica
            </div>
            <h2 class="text-5xl md:text-7xl font-black text-white mb-6 tracking-tight">O impacto do <span class="text-brand-500 bg-clip-text text-transparent bg-gradient-to-r from-brand-400 to-brand-600">descanso</span></h2>
            
            <div class="max-w-3xl mx-auto text-slate-400 text-lg leading-relaxed text-justify md:text-center space-y-4">
                <p>Ver colegas dormindo durante a explicação do professor virou algo comum na rotina. Quase sempre, a reação imediata é julgar isso como preguiça. O projeto <strong>SleepInsights PRO</strong> nasce para quebrar esse preconceito usando Data Science.</p>
                <p>Estudos provam que adolescentes sofrem um atraso natural na liberação de melatonina, dormindo apenas por volta da meia-noite. Ao acordar às 6h da manhã, o aluno perde a fase essencial do <em>Sono REM</em>, momento em que o cérebro limpa toxinas e fixa o aprendizado. Nosso dashboard mapeia essa crise biológica em tempo real.</p>
            </div>
        </header>

        <section class="glass p-8 rounded-3xl mb-16 scroll-reveal border-t-2 border-brand-500/50 flex flex-col lg:flex-row gap-10 items-center">
            <div class="w-full lg:w-1/2 flex flex-col gap-6">
                <div>
                    <h3 class="text-2xl font-bold text-white mb-1">Qual é a sua vibe?</h3>
                    <p class="text-sm text-slate-400">Seja sincero: quantas horas você dormiu na última noite?</p>
                </div>
                
                <div class="relative pt-6 pb-2">
                    <div class="flex justify-between text-xs font-bold text-slate-500 mb-2 uppercase">
                        <span>0h (Morte)</span>
                        <span>20h (Hibernação)</span>
                    </div>
                    <input type="range" min="0" max="20" step="1" value="7" class="w-full neon-slider" id="sleep-slider" oninput="updatePersonality()">
                    <div class="text-center mt-6">
                        <span class="text-5xl font-black text-white" id="slider-value-display">7<span class="text-2xl text-brand-500">h</span></span>
                    </div>
                </div>
            </div>

            <div class="w-full lg:w-1/2 bg-slate-900/60 rounded-2xl p-6 border border-slate-800 flex items-center gap-6 shadow-inner">
                <div class="relative w-32 h-32 flex-shrink-0">
                    <svg class="w-full h-full transform -rotate-90" viewBox="0 0 100 100">
                        <circle cx="50" cy="50" r="40" fill="transparent" stroke="#1e293b" stroke-width="8"></circle>
                        <circle id="health-ring" cx="50" cy="50" r="40" fill="transparent" stroke="#8b5cf6" stroke-width="8" stroke-dasharray="251.2" stroke-dashoffset="0" stroke-linecap="round" class="transition-all duration-1000 ease-out"></circle>
                    </svg>
                    <div class="absolute inset-0 flex items-center justify-center flex-col">
                        <i data-lucide="zap" class="text-brand-400 w-6 h-6 animate-pulse"></i>
                    </div>
                </div>
                <div>
                    <p class="text-[10px] font-bold text-slate-500 uppercase tracking-widest mb-1">DIAGNÓSTICO OFICIAL</p>
                    <h4 id="personality-title" class="text-xl md:text-2xl font-black text-brand-400 mb-2">Mestre do Descanso 🧠</h4>
                    <p id="personality-desc" class="text-sm text-slate-300 italic">"Raro e lendário. Você é a única pessoa da sala que sabe o que o professor falou."</p>
                </div>
            </div>
        </section>

        <section class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-12">
            <div class="glass p-8 rounded-3xl scroll-reveal">
                <div class="flex justify-between items-center mb-8">
                    <h3 class="text-xl font-bold">Impacto na Média Escolar</h3>
                    <i data-lucide="bar-chart" class="text-brand-500 w-5"></i>
                </div>
                <div class="h-[300px]">
                    <canvas id="chartSleepGrades"></canvas>
                </div>
            </div>
            <div class="glass p-8 rounded-3xl scroll-reveal">
                <div class="flex justify-between items-center mb-8">
                    <h3 class="text-xl font-bold">Vilões do Sono</h3>
                    <i data-lucide="pie-chart" class="text-pink-500 w-5"></i>
                </div>
                <div class="h-[300px]">
                    <canvas id="chartReasons"></canvas>
                </div>
            </div>
        </section>

        <section class="glass p-8 rounded-3xl mb-12 scroll-reveal border-t border-brand-500/30">
            <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-6 mb-10">
                <div>
                    <h3 class="text-2xl font-bold text-white mb-2">Índice de Sonolência por Matéria</h3>
                    <p class="text-sm text-slate-400">Descubra em quais aulas o sistema entra em colapso.</p>
                </div>
                <select id="subject-selector" onchange="updateSubjectAnalysis()" class="bg-slate-900 border border-slate-700 text-white rounded-xl px-6 py-3 outline-none focus:border-brand-500 transition-all cursor-pointer font-bold appearance-none">
                    <option value="Artes">Artes</option>
                    <option value="Física">Física</option>
                    <option value="Matemática">Matemática</option>
                    <option value="Português">Português</option>
                    <option value="Química">Química</option>
                    <option value="Biologia">Biologia</option>
                    <option value="História">História</option>
                    <option value="Geografia">Geografia</option>
                    <option value="Filosofia">Filosofia</option>
                    <option value="Sociologia">Sociologia</option>
                    <option value="Inglês">Inglês</option>
                    <option value="Educação Física">Educação Física</option>
                    <option value="UC1">UC1</option>
                    <option value="UC2">UC2</option>
                    <option value="UC3">UC3</option>
                </select>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div class="bg-slate-900/40 p-6 rounded-2xl border border-slate-800">
                    <p class="text-slate-500 text-xs font-bold uppercase mb-4">Incidência de Sono</p>
                    <div class="flex items-end gap-2 mb-2">
                        <span id="subject-sleep-perc" class="text-4xl font-black text-white">0%</span>
                        <span id="subject-count" class="text-slate-500 text-xs mb-1">/ 0 alunos</span>
                    </div>
                    <div class="h-2 w-full bg-slate-800 rounded-full overflow-hidden">
                        <div id="subject-progress-bar" class="h-full bg-brand-500 transition-all duration-1000" style="width: 0%"></div>
                    </div>
                </div>

                <div class="bg-slate-900/40 p-6 rounded-2xl border border-slate-800">
                    <p class="text-slate-500 text-xs font-bold uppercase mb-4">Média da Turma</p>
                    <h4 id="subject-grade" class="text-4xl font-black text-white mb-1">0.0</h4>
                    <p class="text-slate-500 text-[10px]">Nota de quem dorme nesta aula</p>
                </div>

                <div class="bg-slate-900/40 p-6 rounded-2xl border border-slate-800 flex flex-col justify-center">
                    <p class="text-slate-500 text-xs font-bold uppercase mb-2">Status de Sobrevivência</p>
                    <div id="subject-risk-badge" class="px-4 py-2 rounded-lg text-center font-black text-sm uppercase tracking-widest">
                        ANALISANDO...
                    </div>
                </div>
            </div>
        </section>

        <section class="glass p-8 rounded-3xl mb-12 scroll-reveal text-center relative overflow-hidden">
            <div class="absolute top-0 left-1/2 -translate-x-1/2 w-full max-w-lg h-32 bg-brand-600/20 blur-[80px] -z-10"></div>
            <h3 class="text-3xl font-black mb-4">Guia Prático de Higiene do Sono</h3>
            <p class="text-slate-400 mb-10 max-w-2xl mx-auto">Não basta analisar, precisamos resolver. Aplique estas três regras hoje mesmo para resetar seu relógio biológico.</p>
            
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <div class="bg-slate-900/50 p-6 border border-slate-800 rounded-2xl hover:border-brand-500/50 transition-all">
                    <i data-lucide="smartphone-off" class="text-red-400 w-10 h-10 mx-auto mb-4"></i>
                    <h4 class="font-bold text-white mb-2">Filtro Antitelas</h4>
                    <p class="text-xs text-slate-400">A luz azul do celular destrói a produção de melatonina. Desconecte 30 minutos antes de deitar.</p>
                </div>
                <div class="bg-slate-900/50 p-6 border border-slate-800 rounded-2xl hover:border-brand-500/50 transition-all">
                    <i data-lucide="coffee" class="text-yellow-500 w-10 h-10 mx-auto mb-4 relative">
                        <span class="absolute top-0 right-0 w-3 h-3 bg-red-500 rounded-full border-2 border-slate-900"></span>
                    </i>
                    <h4 class="font-bold text-white mb-2">Corte o Energético</h4>
                    <p class="text-xs text-slate-400">A cafeína pode durar até 8 horas no sangue. Evite energéticos ou café forte após as 16h.</p>
                </div>
                <div class="bg-slate-900/50 p-6 border border-slate-800 rounded-2xl hover:border-brand-500/50 transition-all">
                    <i data-lucide="moon-star" class="text-brand-400 w-10 h-10 mx-auto mb-4"></i>
                    <h4 class="font-bold text-white mb-2">Caverna do Morcego</h4>
                    <p class="text-xs text-slate-400">O cérebro precisa de escuridão total para aprofundar o sono REM. Feche todas as frestas e evite LEDs piscando.</p>
                </div>
            </div>
        </section>

        <section class="glass rounded-3xl overflow-hidden mb-12 scroll-reveal">
            <div class="p-8 border-b border-slate-800 flex flex-col md:flex-row justify-between items-center gap-4">
                <div>
                    <h3 class="text-xl font-bold flex items-center gap-2"><i data-lucide="database" class="text-brand-500"></i> Base de Dados Anonimizada</h3>
                    <p class="text-xs text-slate-400 mt-1">Placar detalhado de todos os 100 alunos entrevistados.</p>
                </div>
                <div class="relative w-full md:w-80">
                    <i data-lucide="search" class="absolute left-3 top-1/2 -translate-y-1/2 text-slate-500 w-4"></i>
                    <input type="text" id="table-search" onkeyup="searchTable()" placeholder="Buscar matéria ou motivo..." class="bg-slate-900 border border-slate-700 rounded-xl py-2 pl-10 pr-4 outline-none focus:border-brand-500 text-white w-full transition-all text-sm">
                </div>
            </div>
            
            <div class="overflow-x-auto">
                <table class="w-full text-left">
                    <thead class="bg-slate-900/50 text-slate-500 text-[10px] uppercase font-black tracking-widest">
                        <tr>
                            <th class="px-8 py-4">ID do Aluno</th>
                            <th class="px-8 py-4">Horas de Sono</th>
                            <th class="px-8 py-4">Principal Vilão</th>
                            <th class="px-8 py-4">Matéria Crítica</th>
                            <th class="px-8 py-4">Média Geral</th>
                        </tr>
                    </thead>
                    <tbody id="main-table-body" class="divide-y divide-slate-800/50">
                        </tbody>
                </table>
            </div>
            <div class="p-4 bg-slate-900/30 flex justify-center gap-2 flex-wrap" id="pagination">
                </div>
        </section>

        <footer class="text-center py-10 border-t border-slate-800/50">
            <p class="text-xs font-bold tracking-[0.3em] uppercase text-slate-500">
                Desenvolvido por Angelo Gabriel Pereira de Souza & Equipe &copy; 2026
            </p>
        </footer>
    </main>

    <script src="script.js"></script>
</body>
</html>


    <script>
        /* =========================================================
PROJETO: SleepInsights PRO
AUTOR: Angelo Gabriel Pereira de Souza & Equipe
ANO: 2026
DESCRIÇÃO: Dashboard com Lógica Biológica, Analytics e Placar Interativo
========================================================= */

const sleepPersonas = {
    "zero": {
        titles: ["Inimigo do Travesseiro 👁️", "Vampiro CLT 🦇"],
        phrases: ["Mano, 0 a 1 hora? Você não dorme, você pisca demorado.", "Acha que somos trouxa de acreditar nisso? 🙄 Vai deitar, pelo amor de Deus.", "Seu cérebro tá rodando no Windows XP sem ventoinha. Vai dar tela azul já já.", "Já conversou com o seu coração sobre os litros de café que você tomou?"]
    },
    "zumbi": {
        titles: ["Modo Zumbi Premium 🧟", "Sobrevivente na Força do Ódio 🎒"],
        phrases: ["Sobrevivendo na base do desespero e energético barato.", "Seu corpo tá presente na aula, mas sua alma já foi de arrasta pra cima.", "Aquela pescada violenta na carteira já é realidade hoje, né?", "Você não dorme, você entra em modo de espera com 2% de bateria."]
    },
    "cansado": {
        titles: ["Guerreiro Cansado ⚔️", "Bateria Viciada 🔋"],
        phrases: ["Tá na média da galera, o que significa que tá todo mundo lascado junto.", "Você até tenta prestar atenção, mas seu olho pesa mais que a mochila.", "Funcional? Sim. Feliz e focado? Claramente não.", "Você ri para não chorar quando o professor passa matéria nova às 7h."]
    },
    "mestre": {
        titles: ["Mestre do Descanso 🧠", "O Escolhido da Melatonina 👑"],
        phrases: ["Raro e lendário. Você é a única pessoa da sala que sabe o que o professor falou.", "Enquanto a galera tá babando na mesa, seu cérebro tá salvando o conteúdo no HD.", "Finalmente alguém normal! Parabéns pelo mínimo de amor à própria saúde.", "O Sono REM sorri para você. Provavelmente vai tirar nota alta hoje."]
    },
    "urso": {
        titles: ["Modo Urso de Férias 🐻", "Herdeiro do Colchão 🛌"],
        phrases: ["Maluco, tu hibernou? Desse jeito vai acordar mais cansado do que quando deitou.", "A cama te abraçou e não soltou mais. Cuidado com a moleza extrema.", "Descansou por você e por três amigos que ficaram estudando de madrugada."]
    },
    "mentiroso": {
        titles: ["Viajante do Tempo ⏳", "Bela Adormecida da Shopee 👑"],
        phrases: ["Caraca meu mano, você tem vida social? 20 horas de sono é coma induzido.", "A gente sabe que tu arrastou a bolinha até o final só pra testar o site. Muito engraçadinho. 🙄", "Mentira tem perna curta, e essa sua aí nem andou, já caiu dormindo na largada.", "Se for verdade, por favor, me passa o contato do seu médico. Isso não é normal."]
    }
};

const getRandom = (array) => array[Math.floor(Math.random() * array.length)];

window.updatePersonality = () => {
    const hours = parseInt(document.getElementById('sleep-slider').value);
    document.getElementById('slider-value-display').innerHTML = `${hours}<span class="text-2xl text-brand-500">h</span>`;

    let cat = ""; let ringColor = ""; let fillPercentage = 0;

    if (hours < 2) { cat = "zero"; ringColor = "#ef4444"; fillPercentage = 10; }
    else if (hours <= 4) { cat = "zumbi"; ringColor = "#f97316"; fillPercentage = 30; }
    else if (hours <= 6) { cat = "cansado"; ringColor = "#eab308"; fillPercentage = 60; }
    else if (hours <= 9) { cat = "mestre"; ringColor = "#10b981"; fillPercentage = 100; }
    else if (hours <= 13) { cat = "urso"; ringColor = "#3b82f6"; fillPercentage = 100; }
    else { cat = "mentiroso"; ringColor = "#8b5cf6"; fillPercentage = 100; }

    document.getElementById('personality-title').innerText = getRandom(sleepPersonas[cat].titles);
    document.getElementById('personality-desc').innerText = `"${getRandom(sleepPersonas[cat].phrases)}"`;
    document.getElementById('personality-title').style.color = ringColor;

    const ring = document.getElementById('health-ring');
    const circumference = 251.2;
    const offset = circumference - (fillPercentage / 100) * circumference;
    ring.style.stroke = ringColor;
    ring.style.strokeDashoffset = offset;
};

// ==========================================
// 2. ALGORITMO REALISTA DE DADOS (PESOS BASEADOS EM PESQUISAS)
// ==========================================
const subjectWeights = [
    { name: "Artes", weight: 15 },
    { name: "Física", weight: 14 },
    { name: "Matemática", weight: 14 },
    { name: "Português", weight: 11 },
    { name: "História", weight: 9 },
    { name: "Biologia", weight: 7 },
    { name: "Química", weight: 7 },
    { name: "Geografia", weight: 6 },
    { name: "Sociologia", weight: 4 },
    { name: "Filosofia", weight: 4 },
    { name: "Inglês", weight: 4 },
    { name: "Educação Física", weight: 2 },
    { name: "UC1", weight: 1 },
    { name: "UC2", weight: 1 },
    { name: "UC3", weight: 1 }
];

// Função que sorteia a matéria respeitando os pesos (para que Matemática caia mais que UC3, mas UC3 não zere)
const getWeightedSubject = () => {
    let sum = 0;
    let r = Math.random() * 100;
    for (let i = 0; i < subjectWeights.length; i++) {
        sum += subjectWeights[i].weight;
        if (r <= sum) return subjectWeights[i].name;
    }
    return "Artes"; // Fallback
};

const generateData = () => {
    const reasons = ["Celular", "Celular", "Ansiedade", "Série/Jogos", "Estudos"];
    let students = [];

    // Primeiro garantimos pelo menos 1 aluno para cada matéria (para não ficar 0% nunca no seletor)
    const guaranteedSubjects = subjectWeights.map(s => s.name);
    
    for (let i = 1; i <= 100; i++) {
        let sleep = Math.floor(Math.random() * 6) + 3; // 3h a 8h
        if (sleep === 8) sleep = 7; 

        let reason = reasons[Math.floor(Math.random() * reasons.length)];
        let baseGrade = sleep >= 6 ? 6.5 + Math.random() * 2.8 : 3.5 + Math.random() * 3.5;

        let classSleep = "Não";
        if (sleep <= 6) {
            // Se ainda houver matérias obrigatórias, gasta elas primeiro para garantir dados. Senão, sorteia pelo peso.
            if (guaranteedSubjects.length > 0) {
                classSleep = guaranteedSubjects.pop();
            } else {
                classSleep = getWeightedSubject();
            }
        }

        students.push({
            id: i, 
            sleep: sleep,
            classSleep: classSleep,
            reason: reason,
            grade: parseFloat(baseGrade.toFixed(1))
        });
    }
    return students;
};

const allStudents = generateData();
let filteredData = [...allStudents];
let charts = {};
let currentPage = 1;
const rowsPerPage = 10;

// ==========================================
// 3. INICIALIZAÇÃO
// ==========================================
document.addEventListener('DOMContentLoaded', () => {
    lucide.createIcons();
    initParticles();
    setupScrollReveal();
    updatePersonality();
    renderBarChart();
    renderPieChart();
    updateSubjectAnalysis();
    renderTable();
    renderPagination();
});

window.openQR = () => {
    const modal = document.getElementById('qr-modal');
    modal.classList.remove('hidden');
    setTimeout(() => {
        modal.classList.remove('opacity-0');
        document.getElementById('qr-content').classList.remove('scale-95');
    }, 10);
};
window.closeQR = () => {
    const modal = document.getElementById('qr-modal');
    modal.classList.add('opacity-0');
    document.getElementById('qr-content').classList.add('scale-95');
    setTimeout(() => { modal.classList.add('hidden'); }, 300);
};

// ==========================================
// 4. GRÁFICOS
// ==========================================
const renderBarChart = () => {
    const ctx = document.getElementById('chartSleepGrades').getContext('2d');
    Chart.defaults.color = '#94a3b8';
    Chart.defaults.font.family = 'Plus Jakarta Sans';

    const groups = { "3h-4h": [], "5h-6h": [], "7h+": [] };
    allStudents.forEach(s => {
        if (s.sleep <= 4) groups["3h-4h"].push(s.grade);
        else if (s.sleep <= 6) groups["5h-6h"].push(s.grade);
        else groups["7h+"].push(s.grade);
    });

    const labels = Object.keys(groups);
    const dataAverages = labels.map(l => groups[l].length > 0 ? (groups[l].reduce((a,b)=>a+b,0) / groups[l].length).toFixed(1) : 0);

    charts.bar = new Chart(ctx, {
        type: 'bar',
        data: {
            labels: labels,
            datasets: [{
                label: 'Média de Nota',
                data: dataAverages,
                backgroundColor: ['#ef4444', '#eab308', '#10b981'],
                borderRadius: 8, barThickness: 45
            }]
        },
        options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false } } }
    });
};

const renderPieChart = () => {
    const ctx = document.getElementById('chartReasons').getContext('2d');
    const counts = {};
    allStudents.forEach(s => { counts[s.reason] = (counts[s.reason] || 0) + 1; });

    charts.pie = new Chart(ctx, {
        type: 'doughnut',
        data: {
            labels: Object.keys(counts),
            datasets: [{
                data: Object.values(counts),
                backgroundColor: ['#8b5cf6', '#ec4899', '#f59e0b', '#3b82f6'],
                borderWidth: 2, borderColor: '#050811'
            }]
        },
        options: { responsive: true, maintainAspectRatio: false, cutout: '70%', plugins: { legend: { position: 'right' } } }
    });
};

window.updateSubjectAnalysis = () => {
    const subject = document.getElementById('subject-selector').value;
    const sleepers = allStudents.filter(s => s.classSleep === subject);
    
    const totalSleepers = allStudents.filter(s => s.classSleep !== "Não").length;
    const percentage = totalSleepers === 0 ? 0 : Math.round((sleepers.length / totalSleepers) * 100);
    const avgGrade = sleepers.length > 0 ? (sleepers.reduce((a, b) => a + b.grade, 0) / sleepers.length).toFixed(1) : 0;

    document.getElementById('subject-count').innerText = `/ ${sleepers.length} alunos afetados`;
    document.getElementById('subject-sleep-perc').innerText = `${percentage}%`;
    
    const gradeEl = document.getElementById('subject-grade');
    gradeEl.innerText = avgGrade > 0 ? avgGrade : '-.-';
    
    const progressBar = document.getElementById('subject-progress-bar');
    progressBar.style.width = `${percentage}%`;

    const badge = document.getElementById('subject-risk-badge');
    if (sleepers.length === 0) {
        badge.className = "px-4 py-2 rounded-lg font-black text-sm uppercase tracking-widest bg-slate-800 text-slate-400";
        badge.innerText = "SEM DADOS";
        progressBar.style.backgroundColor = "#64748b";
        gradeEl.className = "text-4xl font-black mb-1 text-slate-500";
    } else if (percentage >= 12) {
        badge.className = "px-4 py-2 rounded-lg font-black text-sm uppercase tracking-widest bg-red-500/20 text-red-500 border border-red-500/30";
        badge.innerText = "RISCO ALTO";
        progressBar.style.backgroundColor = "#ef4444";
        gradeEl.className = "text-4xl font-black mb-1 text-red-500";
    } else if (percentage >= 6) {
        badge.className = "px-4 py-2 rounded-lg font-black text-sm uppercase tracking-widest bg-yellow-500/20 text-yellow-500 border border-yellow-500/30";
        badge.innerText = "RISCO MÉDIO";
        progressBar.style.backgroundColor = "#eab308";
        gradeEl.className = "text-4xl font-black mb-1 text-yellow-500";
    } else {
        badge.className = "px-4 py-2 rounded-lg font-black text-sm uppercase tracking-widest bg-brand-500/20 text-brand-400 border border-brand-500/30";
        badge.innerText = "RISCO BAIXO";
        progressBar.style.backgroundColor = "#8b5cf6";
        gradeEl.className = "text-4xl font-black mb-1 text-brand-400";
    }
};

// ==========================================
// 5. TABELA DE DADOS (PLACAR) E PAGINAÇÃO
// ==========================================
const renderTable = () => {
    const tbody = document.getElementById('main-table-body');
    tbody.innerHTML = '';
    
    const start = (currentPage - 1) * rowsPerPage;
    const paginatedItems = filteredData.slice(start, start + rowsPerPage);

    if (paginatedItems.length === 0) {
        tbody.innerHTML = '<tr><td colspan="5" class="px-8 py-6 text-center text-slate-500 font-bold">Nenhum registro encontrado.</td></tr>';
        return;
    }

    paginatedItems.forEach(s => {
        // Cores baseadas nas horas de sono e notas
        const sleepColor = s.sleep <= 4 ? 'bg-red-500 shadow-[0_0_8px_#ef4444]' : (s.sleep <= 6 ? 'bg-yellow-500' : 'bg-brand-500');
        const gradeColor = s.grade >= 7.0 ? 'text-green-500' : (s.grade >= 5.5 ? 'text-yellow-500' : 'text-red-500');
        const subjectFormat = s.classSleep === "Não" ? '<span class="text-slate-600 italic">Acordado</span>' : `<span class="text-brand-400 font-medium">${s.classSleep}</span>`;

        const row = `
            <tr class="hover:bg-slate-800/30 transition-colors group">
                <td class="px-8 py-4 font-black text-slate-500 group-hover:text-white transition-colors text-sm">Aluno #${String(s.id).padStart(3, '0')}</td>
                <td class="px-8 py-4 text-slate-300">
                    <div class="flex items-center gap-2">
                        <span class="w-2 h-2 rounded-full ${sleepColor}"></span>
                        <span class="font-bold">${s.sleep}h</span>
                    </div>
                </td>
                <td class="px-8 py-4">
                    <span class="bg-slate-800/50 text-slate-300 px-3 py-1 rounded-full text-[10px] font-bold uppercase border border-slate-700/50">
                        ${s.reason}
                    </span>
                </td>
                <td class="px-8 py-4 text-sm">${subjectFormat}</td>
                <td class="px-8 py-4 font-black ${gradeColor} text-base">${s.grade.toFixed(1)}</td>
            </tr>
        `;
        tbody.innerHTML += row;
    });
};

const renderPagination = () => {
    const container = document.getElementById('pagination');
    container.innerHTML = '';
    const pageCount = Math.ceil(filteredData.length / rowsPerPage);

    if (pageCount <= 1) return;

    for(let i = 1; i <= pageCount; i++) {
        container.innerHTML += `<button onclick="goToPage(${i})" class="page-link ${i === currentPage ? 'active' : 'bg-slate-800 text-slate-400'}">${i}</button>`;
    }
};

window.goToPage = (page) => {
    currentPage = page;
    renderTable();
    renderPagination();
};

window.searchTable = () => {
    const term = document.getElementById('table-search').value.toLowerCase();
    
    filteredData = allStudents.filter(s => 
        s.reason.toLowerCase().includes(term) || 
        s.classSleep.toLowerCase().includes(term) ||
        String(s.id).includes(term)
    );
    
    currentPage = 1;
    renderTable();
    renderPagination();
};

window.exportCSV = () => {
    let csv = "ID_Aluno,Horas_Dormidas,Motivo,Materia_Que_Dorme,Media_Escolar\n";
    allStudents.forEach(s => {
        csv += `${s.id},${s.sleep},"${s.reason}","${s.classSleep}",${s.grade}\n`;
    });
    const blob = new Blob(["\uFEFF"+csv], { type: 'text/csv;charset=utf-8;' });
    const url = window.URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.setAttribute('href', url);
    a.setAttribute('download', 'Base_SleepInsights_2026.csv');
    document.body.appendChild(a); a.click(); document.body.removeChild(a);
};

// ==========================================
// 6. EFEITOS VISUAIS
// ==========================================
const setupScrollReveal = () => {
    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => { if(entry.isIntersecting) entry.target.classList.add('active'); });
    }, { threshold: 0.1 });
    document.querySelectorAll('.scroll-reveal').forEach(el => observer.observe(el));
};

const initParticles = () => {
    const canvas = document.getElementById('particles-js');
    const ctx = canvas.getContext('2d');
    const resize = () => { canvas.width = window.innerWidth; canvas.height = window.innerHeight; };
    window.addEventListener('resize', resize); resize();

    const pArray = [];
    class Particle {
        constructor() {
            this.x = Math.random() * canvas.width; this.y = Math.random() * canvas.height;
            this.size = Math.random() * 2; this.speedY = Math.random() * -0.5 - 0.2; 
            this.opacity = Math.random() * 0.4 + 0.1;
        }
        update() { this.y += this.speedY; if(this.y < 0) { this.y = canvas.height; this.x = Math.random() * canvas.width; } }
        draw() { ctx.fillStyle = `rgba(139, 92, 246, ${this.opacity})`; ctx.beginPath(); ctx.arc(this.x, this.y, this.size, 0, Math.PI*2); ctx.fill(); }
    }
    for(let i=0; i<50; i++) pArray.push(new Particle());
    function animate() { ctx.clearRect(0,0,canvas.width,canvas.height); pArray.forEach(p => { p.update(); p.draw(); }); requestAnimationFrame(animate); }
    animate();
};

    </script>

</body>
</html>
