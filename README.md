import React, { useState, useEffect, useRef } from 'react';
import { 
  GraduationCap, BookOpen, Video, FileText, Award, MessageSquare, Map, 
  Upload, Shield, Activity, Compass, Folder, CheckCircle2, Download, 
  Search, Menu, X, ChevronRight, User, Send, BookMarked, FileCheck, 
  ArrowRight, Clock, HeartPulse, Brain, Layers, AlertCircle, Sparkles, 
  Bot, Lock, Mail, UserPlus, ArrowLeft, Info, Calendar, RefreshCw, 
  Play, Check, HelpCircle, CheckSquare, UserCheck, ClipboardList, 
  Edit, Save, PlusCircle, FileSpreadsheet, Phone, Instagram, Database, Globe
} from 'lucide-react';

const CURSO_INFO = {
  nome: "Técnico em Enfermagem",
  modulo: "Módulo I - Núcleo da Área de Saúde",
  projetoFinal: {
    titulo: "A Saúde como Condição de Cidadania: Educação para a Saúde",
    descricao: "Utilizar conhecimentos multidisciplinares para uma análise da situação de saúde de uma área descrita do seu Município, propondo ações de promoção e prevenção no âmbito de Educação em Saúde.",
    cargaHoraria: "120h"
  }
};

const UNIDADES_CURRICULARES = [
  {
    id: "unidade-1",
    titulo: "Unidade I: Saúde Pública, Saneamento e Cidadania",
    cargaHoraria: "39h",
    descricao: "Aborda os princípios de saneamento, ecologia, políticas públicas do SUS e os direitos dos cidadãos.",
    modulos: [
      {
        id: "mod-1",
        titulo: "Princípios de Higiene, Saneamento e Meio Ambiente",
        cargaHoraria: "9h",
        videoUrl: "https://www.w3schools.com/html/mov_bbb.mp4",
        pdfTitulo: "Manual de Saneamento Básico e Saúde Coletiva.pdf",
        mapaMental: {
          central: "Saneamento e Saúde",
          ramos: ["Saneamento do Ar", "Tratamento de Água", "Gestão do Lixo/Descarte", "Ambientes de Trabalho", "Processo Saúde-Doença"]
        },
        questoes: [
          {
            pergunta: "Quais fatores de saneamento interferem diretamente no controle de doenças de transmissão hídrica na comunidade?",
            opcoes: [
              "O saneamento do ar e a emissão de gases industriais.",
              "A qualidade do tratamento da água e a destinação correta de esgoto e lixo.",
              "A iluminação pública e a pavimentação de vias.",
              "A organização de associações de moradores locais."
            ],
            respostaCorreta: 1
          }
        ]
      },
      {
        id: "mod-2",
        titulo: "Políticas Públicas de Saúde e SUS",
        cargaHoraria: "12h",
        videoUrl: "https://www.w3schools.com/html/movie.mp4",
        pdfTitulo: "Historia_da_Saude_Publica_no_Brasil.pdf",
        mapaMental: {
          central: "SUS & Cidadania",
          ramos: ["Evolução Histórica", "Universalidade", "Integralidade", "Equidade", "Participação Social"]
        },
        questoes: [
          {
            pergunta: "Qual princípio do SUS garante que todos os cidadãos tenham direito ao acesso a todos os níveis de assistência de saúde?",
            opcoes: [
              "Privatização subsidiada",
              "Descentralização municipal restrita",
              "Universalidade e Integralidade",
              "Centralização de recursos estaduais"
            ],
            respostaCorreta: 2
          }
        ]
      }
    ]
  },
  {
    id: "unidade-2",
    titulo: "Unidade II: Imunização, Anatomia e Práticas",
    cargaHoraria: "32h",
    descricao: "Enfoca a atuação do técnico na imunização, conhecimentos do corpo humano e saúde preventiva.",
    modulos: [
      {
        id: "mod-3",
        titulo: "Educação para o Autocuidado e Promoção da Saúde",
        cargaHoraria: "15h",
        videoUrl: "https://www.w3schools.com/html/movie.mp4",
        pdfTitulo: "Promocao_Saude_Autocuidado.pdf",
        mapaMental: {
          central: "Autocuidado",
          ramos: ["Hábitos de Vida Saudáveis", "Papel do Técnico de Enfermagem", "Atividade Física", "Prevenção Primária"]
        },
        questoes: [
          {
            pergunta: "Qual o principal objetivo do profissional de saúde ao atuar como agente educativo na comunidade?",
            opcoes: [
              "Substituir o médico na prescrição de medicamentos genéricos.",
              "Apenas aplicar vacinas e aferir pressão arterial.",
              "Ajudar os indivíduos a adquirirem autonomia e autocuidado na manutenção da própria saúde.",
              "Impor regras de conduta sem considerar o contexto cultural local."
            ],
            respostaCorreta: 2
          }
        ]
      }
    ]
  }
];

const BIBLIOTECA_DIGITAL = [
  { id: 1, titulo: "Anatomia Básica", autores: "D’ANGELO, J. G. e FATTINI, C. A.", ano: "1983", link: "#", categoria: "Anatomia" },
  { id: 2, titulo: "Epidemiologia & Saúde - 6ª Ed.", autores: "ROUQUAYROL, M. Z. & ALMEIDA FILHO, N.", ano: "1999", link: "#", categoria: "Saúde Pública" }
];

const QUESTOES_PROVA_FINAL = [
  {
    id: 1,
    enunciado: "O saneamento básico é fundamental para evitar a propagação de patógenos. Qual dos seguintes métodos de descarte é considerado ecologicamente seguro para resíduos sólidos urbanos não recicláveis?",
    alternativas: [
      "A) Descarte em lixões a céu aberto.",
      "B) Incineração doméstica descontrolada.",
      "C) Disposição em aterros sanitários devidamente impermeabilizados e monitorados.",
      "D) Descarte em leitos de rios de fluxo rápido.",
      "E) Enterramento simples no quintal residencial."
    ],
    correta: 2
  },
  {
    id: 2,
    enunciado: "Em relação ao saneamento da água, qual a principal finalidade da etapa de cloração na Estação de Tratamento de Água (ETA)?",
    alternativas: [
      "A) Retirar o sabor metálico e os sais minerais pesados.",
      "B) Eliminar microrganismos patogênicos remanescentes e garantir a desinfecção.",
      "C) Promover a coagulação de partículas orgânicas suspensas.",
      "D) Ajustar o pH para torná-la ácida.",
      "E) Filtrar a areia fina."
    ],
    correta: 1
  }
];

const TUTOR_IA_SYSTEM_PROMPT = `
Você é o Tutor IA do Instituto EADUCAR, um orientador e assistente virtual de inteligência artificial de altíssimo nível, amigável, acolhedor, profissional e com profundo conhecimento prático, clínico e teórico na área de Saúde de modo geral (nacional e mundial), além de atuar como assistente institucional do Instituto EADUCAR.

Você tem acesso em tempo real à internet por meio da sua ferramenta de pesquisa integrada (Google Search Grounding). Suas respostas devem ser atualizadas e embasadas.

SUAS ATRIBUIÇÕES E CONHECIMENTOS:
1. CONHECIMENTOS GERAIS DE SAÚDE: Responder sobre anatomia, fisiologia, procedimentos de enfermagem, farmacologia básica, cenário epidemiológico (Dengue, Covid, Febre Oropouche, etc.), saúde pública mundial e nacional, sem se restringir apenas ao SUS.
2. CURRÍCULO DO TÉCNICO DE ENFERMAGEM EADUCAR: "A Saúde como Condição de Cidadania".
3. REGRAS DO PORTAL E AVALIAÇÕES ACADÊMICAS:
   - O avanço nos tópicos do AVA é linear (exige vídeo e quiz correto).
   - Sistema de Avaliações Finais: P1 (oficial, prazo 7 dias, média 7.0), P2 (segunda chamada, média 7.0) e P3 (recuperação, média 6.0).
4. REGRAS DO TFC E SECRETARIA: O TFC é baseado no bairro do aluno. A secretaria tem prazo de 2 a 5 dias úteis para emissão de documentos.

Seja categórico, profissional e empático ao tratar de assuntos do Instituto EADUCAR e temas médicos. Incentive o aprendizado ativo.
`;

export default function App() {
  const [isAuthenticated, setIsAuthenticated] = useState(false);
  const [authMode, setAuthMode] = useState('login'); 
  const [authForm, setAuthForm] = useState({
    nome: '', email: '', senha: '', cidade: 'Belém', bairro: 'Umarizal', estado: 'PA', role: 'aluno'
  });
  const [currentUser, setCurrentUser] = useState(null);

  // Estados de Navegação
  const [activeTab, setActiveTab] = useState('dashboard'); // dashboard, trilha, secretaria, documentos, biblioteca, tfc, tutor, admin, professor, suporte, faq
  const [currentModule, setCurrentModule] = useState(UNIDADES_CURRICULARES[0].modulos[0]);
  const [currentUnidade, setCurrentUnidade] = useState(UNIDADES_CURRICULARES[0]);
  const [currentContentTab, setCurrentContentTab] = useState('video'); 
  const [secretariaSubTab, setSecretariaSubTab] = useState('documentos'); 
  const [professorSubTab, setProfessorSubTab] = useState('diario'); 
  const [bibliotecaSubTab, setBibliotecaSubTab] = useState('livros'); 
  const [bibliotecaSearch, setBibliotecaSearch] = useState(''); 
  
  const [isEditingProfile, setIsEditingProfile] = useState(false);
  const [tempProfile, setTempProfile] = useState({ cidade: '', bairro: '' });

  // Progresso
  const [progressoModulos, setProgressoModulos] = useState(() => {
    return {
      "mod-1": { assistido: false, nota: null, concluido: false },
      "mod-2": { assistido: false, nota: null, concluido: false },
      "mod-3": { assistido: false, nota: null, concluido: false }
    };
  });

  const [tfcUpload, setTfcUpload] = useState({
    nomeArquivo: "", status: "Não Enviado", nota: null, comentarioOrientador: "", dataEnvio: ""
  });

  // Configuração Admin
  const [adminConfig, setAdminConfig] = useState({
    p1Liberada: true, p1PeriodoSimulado: 'dentro_prazo', p2Liberada: false, p3Liberada: false,
    historicoProvas: {
      P1: { realizada: false, acertos: 0, nota: 0, status: 'Pendente' },
      P2: { realizada: false, acertos: 0, nota: 0, status: 'Pendente' },
      P3: { realizada: false, acertos: 0, nota: 0, status: 'Pendente' }
    },
    statusAcademicoFinal: 'Em Progresso'
  });

  // Gestão Professor
  const [estudantesTurma, setEstudantesTurma] = useState([
    { id: 'al-1', nome: 'Ana Lúcia Oliveira', matricula: 'EAD-2026-09A', frequencia: 96, faltas: 1, notaQuiz: 10, notaP1: null, notaP2: null, notaP3: null, notaTFC: null, notaTrab: null, status: 'Em Progresso' },
  ]);

  const [diarioConteudos, setDiarioConteudos] = useState([
    { id: 1, data: "12/05/2026", modulo: "Princípios de Higiene", conteudo: "Apresentação do ecossistema", ch: "9h" }
  ]);

  const [novoConteudoData, setNovoConteudoData] = useState("23/05/2026");
  const [novoConteudoModulo, setNovoConteudoModulo] = useState("Princípios de Higiene");
  const [novoConteudoDesc, setNovoConteudoDesc] = useState("");
  const [novoConteudoCH, setNovoConteudoCH] = useState("6h");
  const [editingStudentId, setEditingStudentId] = useState(null);
  const [tempGrades, setTempGrades] = useState({ notaP1: '', notaP2: '', notaP3: '', notaTFC: '', notaTrab: '', frequencia: '', faltas: '' });

  // Exames e Quizzes
  const [isExamRunning, setIsExamRunning] = useState(false);
  const [examType, setExamType] = useState('P1'); 
  const [examQuestions, setExamQuestions] = useState([]);
  const [examAnswers, setExamAnswers] = useState({}); 
  const [examTimeRemaining, setExamTimeRemaining] = useState(3 * 60 * 60); 
  const [quizAnswer, setQuizAnswer] = useState(null);
  const [quizFeedback, setQuizFeedback] = useState(null);

  // Chatbot (Tutor IA)
  const [chatMessages, setChatMessages] = useState([
    {
      id: "welcome-msg",
      sender: "bot",
      text: "Olá! Sou o Tutor IA do Instituto EADUCAR. Estou habilitado para responder dúvidas profundas de saúde, patologias, anatomia e epidemiologia (no Brasil e no Mundo), além de esclarecer todas as regras acadêmicas do seu curso e do TFC. Como posso te orientar hoje?",
      timestamp: "Agora",
      attributions: []
    }
  ]);
  const [chatInput, setChatInput] = useState("");
  const [isChatLoading, setIsChatLoading] = useState(false);

  // Documentos
  const [docsEnviados, setDocsEnviados] = useState({
    rg: { nome: "rg_frente_verso.pdf", status: "Aprovado", data: "12/05/2026" }
  });
  const [solicitacoes, setSolicitacoes] = useState([]);
  const [docSolicitacaoSelecionado, setDocSolicitacaoSelecionado] = useState("Declaração de Matrícula Ativa");

  const [activeFaqIndex, setActiveFaqIndex] = useState(null);
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);
  const [systemAlert, setSystemAlert] = useState(null);

  const timerRef = useRef(null);
  const messagesEndRef = useRef(null);

  const showAlert = (message, type = "success") => {
    setSystemAlert({ message, type });
    setTimeout(() => setSystemAlert(null), 5000);
  };

  const modulosOrdem = ["mod-1", "mod-2", "mod-3"];
  const todosModulosConcluidos = modulosOrdem.every(id => progressoModulos[id]?.concluido);

  const handleLogin = (e) => {
    e.preventDefault();
    if (!authForm.email || !authForm.senha) {
      showAlert("Preencha todos os campos para fazer o login.", "error");
      return;
    }
    const user = {
      name: authForm.email.split('@')[0].toUpperCase(),
      email: authForm.email,
      avatar: authForm.email.substring(0, 2).toUpperCase(),
      cidade: authForm.cidade || "Belém",
      bairro: authForm.bairro || "Umarizal",
      estado: authForm.estado || "PA",
      role: authForm.role
    };
    setCurrentUser(user);
    setTempProfile({ cidade: user.cidade, bairro: user.bairro });
    setIsAuthenticated(true);

    if (user.role === 'professor') {
      setActiveTab('professor');
      showAlert("Acesso liberado. Bem-vindo(a) à área docente do Instituto EADUCAR!");
    } else {
      setActiveTab('dashboard');
      showAlert("Bem-vindo de volta ao portal de estudos do Instituto EADUCAR!");
    }
  };

  const handleRegister = (e) => {
    e.preventDefault();
    if (!authForm.nome || !authForm.email || !authForm.senha || !authForm.cidade || !authForm.bairro) {
      showAlert("Todos os campos de cadastro são obrigatórios.", "error");
      return;
    }
    const user = {
      name: authForm.nome, email: authForm.email, avatar: authForm.nome.substring(0, 2).toUpperCase(),
      cidade: authForm.cidade, bairro: authForm.bairro, estado: authForm.estado, role: authForm.role
    };
    setCurrentUser(user);
    setTempProfile({ cidade: user.cidade, bairro: user.bairro });
    setIsAuthenticated(true);

    if (user.role === 'professor') {
      setActiveTab('professor');
      showAlert("Conta docente cadastrada com sucesso! Bem-vindo(a).");
    } else {
      setActiveTab('dashboard');
      showAlert("Conta cadastrada com sucesso! Bem-vindo(a) ao Instituto EADUCAR.");
    }
  };

  const handleDemoLogin = (role = 'aluno') => {
    if (role === 'professor') {
      const demoProf = { name: "Prof. Carlos Silva", email: "carlos@eaducar.com.br", avatar: "CS", cidade: "Belém", bairro: "Nazaré", estado: "PA", role: "professor" };
      setCurrentUser(demoProf);
      setTempProfile({ cidade: demoProf.cidade, bairro: demoProf.bairro });
      setIsAuthenticated(true);
      setActiveTab('professor');
      showAlert("Acesso rápido autorizado com o perfil de Professor.");
    } else {
      const demoUser = { name: "Ana Lúcia Oliveira", email: "ana@eaducar.com.br", avatar: "AL", cidade: "Belém", bairro: "Umarizal", estado: "PA", role: "aluno" };
      setCurrentUser(demoUser);
      setTempProfile({ cidade: demoUser.cidade, bairro: demoUser.bairro });
      setIsAuthenticated(true);
      setActiveTab('dashboard');
      showAlert("Acesso rápido autorizado com o perfil de testes de Aluno.");
    }
  };

  const handleLogout = () => {
    setIsAuthenticated(false); setCurrentUser(null); setActiveTab('dashboard');
    showAlert("Sessão encerrada com sucesso.");
  };

  const handleSendMessage = async (e) => {
    if (e) e.preventDefault();
    if (!chatInput.trim()) return;

    const userMsg = chatInput.trim();
    setChatInput("");
    setChatMessages(prev => [...prev, { id: `msg-${Date.now()}-user`, sender: "user", text: userMsg }]);
    setIsChatLoading(true);

    setTimeout(() => {
      setChatMessages(prev => [...prev, { 
        id: `msg-${Date.now()}-bot`, 
        sender: "bot", 
        text: `Com base nas diretrizes de saúde mundial e parâmetros do Instituto EADUCAR, aqui está a resposta sobre sua dúvida: "${userMsg}". Lembre-se, o avanço nos módulos exige a conclusão do quiz e a secretaria tem prazo de emissão de documentos de 2 a 5 dias.`, 
        attributions: [] 
      }]);
      setIsChatLoading(false);
    }, 1500);
  };

  useEffect(() => {
    if (messagesEndRef.current) messagesEndRef.current.scrollIntoView({ behavior: 'smooth' });
  }, [chatMessages]);

  if (isExamRunning) {
    return (
      <div className="min-h-screen bg-slate-950 text-slate-100 flex flex-col font-sans animate-fadeIn">
        <header className="bg-slate-900 border-b border-slate-800 py-4 px-6 flex justify-between items-center sticky top-0 z-50">
          <div className="flex items-center gap-3">
            <Shield className="w-6 h-6 text-amber-500" />
            <h1 className="text-sm font-bold text-white">Exame Monitorado: {examType}</h1>
          </div>
          <button onClick={() => setIsExamRunning(false)} className="bg-red-500 px-4 py-2 rounded font-bold text-xs">Finalizar Prova</button>
        </header>
        <main className="flex-1 max-w-4xl w-full mx-auto p-8 space-y-6">
          {examQuestions.map((q, idx) => (
             <div key={q.id} className="bg-slate-900 border border-slate-800 rounded-xl p-6">
               <p className="text-sm font-bold mb-4">{q.enunciado}</p>
               <div className="space-y-2">
                 {q.alternativas.map((alt, aIdx) => (
                   <button key={aIdx} className="w-full text-left p-3 rounded-lg bg-slate-950 border border-slate-800 text-xs hover:bg-slate-800">{alt}</button>
                 ))}
               </div>
             </div>
          ))}
        </main>
      </div>
    );
  }

  if (!isAuthenticated) {
    return (
      <div className="min-h-screen bg-slate-950 text-slate-100 flex flex-col justify-center items-center px-4 py-10 relative overflow-hidden font-sans">
        <div className="absolute top-1/4 left-1/4 w-96 h-96 bg-teal-500/10 rounded-full blur-3xl -z-10"></div>
        <div className="absolute bottom-1/4 right-1/4 w-96 h-96 bg-indigo-600/10 rounded-full blur-3xl -z-10"></div>

        <div className="max-w-md w-full bg-slate-900 border border-slate-800 rounded-3xl shadow-2xl p-6 sm:p-8 space-y-6 relative animate-fadeIn">
          
          <div className="flex flex-col items-center text-center space-y-2">
            <div className="w-16 h-16 rounded-2xl bg-teal-500/10 flex items-center justify-center border border-teal-500/20 shadow-lg">
              <GraduationCap className="w-9 h-9 text-teal-400" />
            </div>
            <div>
              <span className="text-xl font-bold tracking-wider text-white">INSTITUTO</span>
              <span className="text-xl font-extrabold tracking-wider text-teal-400 ml-1">EADUCAR</span>
            </div>
            <p className="text-xs text-slate-400 font-medium">LMS Integrado para Enfermagem</p>
          </div>

          <div className="grid grid-cols-2 bg-slate-950 p-1 rounded-xl border border-slate-800/60">
            <button onClick={() => setAuthMode('login')} className={`py-2 rounded-lg text-xs font-bold transition-all ${authMode === 'login' ? 'bg-teal-500 text-slate-950 shadow' : 'text-slate-400 hover:text-white'}`}>Acessar Conta</button>
            <button onClick={() => setAuthMode('register')} className={`py-2 rounded-lg text-xs font-bold transition-all ${authMode === 'register' ? 'bg-teal-500 text-slate-950 shadow' : 'text-slate-400 hover:text-white'}`}>Nova Matrícula</button>
          </div>

          <div className="flex flex-col space-y-1">
             <label className="text-[10px] uppercase font-bold text-slate-400 block text-center">Selecione seu Perfil de Acesso</label>
             <div className="grid grid-cols-2 gap-2">
                <button type="button" onClick={() => setAuthForm({ ...authForm, role: 'aluno' })} className={`py-2 rounded-xl text-xs font-bold flex justify-center items-center gap-2 border ${authForm.role === 'aluno' ? 'bg-slate-800 border-teal-500 text-teal-400' : 'bg-slate-950 border-slate-800 text-slate-500'}`}>
                  <GraduationCap className="w-4 h-4" /> Aluno
                </button>
                <button type="button" onClick={() => setAuthForm({ ...authForm, role: 'professor' })} className={`py-2 rounded-xl text-xs font-bold flex justify-center items-center gap-2 border ${authForm.role === 'professor' ? 'bg-slate-800 border-indigo-500 text-indigo-400' : 'bg-slate-950 border-slate-800 text-slate-500'}`}>
                  <UserCheck className="w-4 h-4" /> Professor
                </button>
             </div>
          </div>

          {authMode === 'login' ? (
            <form onSubmit={handleLogin} className="space-y-4 font-sans animate-fadeIn">
              <input type="email" required placeholder="Email" value={authForm.email} onChange={(e) => setAuthForm({ ...authForm, email: e.target.value })} className="w-full bg-slate-950 border border-slate-800 rounded-xl py-2.5 px-4 text-xs text-white" />
              <input type="password" required placeholder="Senha" value={authForm.senha} onChange={(e) => setAuthForm({ ...authForm, senha: e.target.value })} className="w-full bg-slate-950 border border-slate-800 rounded-xl py-2.5 px-4 text-xs text-white" />
              <button type="submit" className="w-full bg-teal-500 text-slate-950 font-bold py-3 rounded-xl text-xs">Entrar no Ambiente de Aula</button>
            </form>
          ) : (
            <form onSubmit={handleRegister} className="space-y-4 font-sans animate-fadeIn">
              <input type="text" required placeholder="Nome Completo" value={authForm.nome} onChange={(e) => setAuthForm({ ...authForm, nome: e.target.value })} className="w-full bg-slate-950 border border-slate-800 rounded-xl py-2.5 px-4 text-xs text-white" />
              <input type="email" required placeholder="Email" value={authForm.email} onChange={(e) => setAuthForm({ ...authForm, email: e.target.value })} className="w-full bg-slate-950 border border-slate-800 rounded-xl py-2.5 px-4 text-xs text-white" />
              <div className="grid grid-cols-2 gap-2">
                <input type="text" required placeholder="Cidade" value={authForm.cidade} onChange={(e) => setAuthForm({ ...authForm, cidade: e.target.value })} className="w-full bg-slate-950 border border-slate-800 rounded-xl py-2.5 px-4 text-xs text-white" />
                <input type="text" required placeholder="Bairro" value={authForm.bairro} onChange={(e) => setAuthForm({ ...authForm, bairro: e.target.value })} className="w-full bg-slate-950 border border-slate-800 rounded-xl py-2.5 px-4 text-xs text-white" />
              </div>
              <input type="password" required placeholder="Senha" value={authForm.senha} onChange={(e) => setAuthForm({ ...authForm, senha: e.target.value })} className="w-full bg-slate-950 border border-slate-800 rounded-xl py-2.5 px-4 text-xs text-white" />
              <button type="submit" className="w-full bg-teal-500 text-slate-950 font-bold py-3 rounded-xl text-xs">Confirmar Inscrição</button>
            </form>
          )}

          <div className="grid grid-cols-2 gap-3 pt-4 border-t border-slate-800 mt-2">
            <button type="button" onClick={() => handleDemoLogin('aluno')} className="w-full bg-slate-950 text-teal-400 border border-teal-500/30 hover:bg-teal-500/10 transition-colors py-2.5 rounded-xl text-xs font-bold flex items-center justify-center gap-2">
              <Sparkles className="w-4 h-4" /> Teste Aluno
            </button>
            <button type="button" onClick={() => handleDemoLogin('professor')} className="w-full bg-slate-950 text-indigo-400 border border-indigo-500/30 hover:bg-indigo-500/10 transition-colors py-2.5 rounded-xl text-xs font-bold flex items-center justify-center gap-2">
              <Sparkles className="w-4 h-4" /> Teste Professor
            </button>
          </div>
        </div>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-slate-900 text-slate-100 font-sans flex flex-col antialiased">
      
      {/* HEADER */}
      <header className="bg-slate-950 border-b border-slate-800 sticky top-0 z-40">
        <div className="max-w-7xl mx-auto px-4 h-16 flex items-center justify-between">
          <div className="flex items-center gap-3 cursor-pointer" onClick={() => setActiveTab('dashboard')}>
            <GraduationCap className="w-6 h-6 text-teal-400" />
            <span className="text-lg font-bold">EADUCAR</span>
          </div>

          <div className="hidden md:flex items-center gap-4">
            {currentUser?.role === 'professor' && (
              <>
                <button onClick={() => setActiveTab('professor')} className="bg-slate-900 text-teal-400 border border-slate-800 py-1.5 px-3 rounded-lg text-xs font-bold flex items-center gap-1.5">
                  <UserCheck className="w-4 h-4" /> Área do Professor
                </button>
                <button onClick={() => setActiveTab('admin')} className="bg-slate-900 text-indigo-400 border border-slate-800 py-1.5 px-3 rounded-lg text-xs font-bold flex items-center gap-1.5">
                  <Shield className="w-4 h-4" /> Coordenação
                </button>
              </>
            )}
            
            <div className="flex items-center gap-3 border-l border-slate-800 pl-4">
              <div className="w-8 h-8 rounded-full bg-teal-500 text-slate-950 flex items-center justify-center font-bold">{currentUser?.avatar}</div>
              <div className="text-xs">
                <p className="font-bold">{currentUser?.name}</p>
                <button onClick={handleLogout} className="text-[10px] text-red-400 hover:text-red-300">Sair da Conta</button>
              </div>
            </div>
          </div>
          
          <button onClick={() => setMobileMenuOpen(!mobileMenuOpen)} className="md:hidden text-slate-400 p-2">
            {mobileMenuOpen ? <X className="w-6 h-6" /> : <Menu className="w-6 h-6" />}
          </button>
        </div>
      </header>

      {/* MOBILE MENU */}
      {mobileMenuOpen && (
        <div className="md:hidden bg-slate-950 border-b border-slate-800 p-4 space-y-2">
          <button onClick={() => { setActiveTab('dashboard'); setMobileMenuOpen(false); }} className="w-full text-left p-3 text-sm font-medium text-slate-300">Painel de Controle</button>
          <button onClick={() => { setActiveTab('trilha'); setMobileMenuOpen(false); }} className="w-full text-left p-3 text-sm font-medium text-slate-300">Trilha de Aprendizagem</button>
          {currentUser?.role === 'professor' && (
            <button onClick={() => { setActiveTab('professor'); setMobileMenuOpen(false); }} className="w-full text-left p-3 text-sm font-medium text-teal-400">Área do Professor</button>
          )}
          <button onClick={() => { setActiveTab('suporte'); setMobileMenuOpen(false); }} className="w-full text-left p-3 text-sm font-medium text-slate-300">Suporte Técnico</button>
          <button onClick={() => { setActiveTab('faq'); setMobileMenuOpen(false); }} className="w-full text-left p-3 text-sm font-medium text-slate-300">Dúvidas / FAQ</button>
          <button onClick={() => { setActiveTab('tutor'); setMobileMenuOpen(false); }} className="w-full text-left p-3 text-sm font-medium text-teal-400">Tutor IA EADUCAR</button>
        </div>
      )}

      {/* MAIN LAYOUT */}
      <div className="flex-1 flex max-w-7xl w-full mx-auto px-4 py-6 gap-6">
        
        {/* SIDEBAR DESKTOP */}
        <aside className="hidden md:block w-64 flex-shrink-0 space-y-4">
          <nav className="bg-slate-950 border border-slate-800 rounded-2xl p-4 shadow-xl space-y-1">
            <button onClick={() => setActiveTab('dashboard')} className={`w-full text-left px-4 py-3 rounded-xl text-sm font-medium ${activeTab === 'dashboard' ? 'bg-teal-500/10 text-teal-400' : 'text-slate-400 hover:text-white hover:bg-slate-900'}`}>Início / Portal</button>
            <button onClick={() => setActiveTab('trilha')} className={`w-full text-left px-4 py-3 rounded-xl text-sm font-medium ${activeTab === 'trilha' ? 'bg-teal-500/10 text-teal-400' : 'text-slate-400 hover:text-white hover:bg-slate-900'}`}>Trilha do AVA</button>
            
            {currentUser?.role === 'professor' && (
              <button onClick={() => setActiveTab('professor')} className={`w-full text-left px-4 py-3 rounded-xl text-sm font-medium ${activeTab === 'professor' ? 'bg-teal-500/15 text-teal-300' : 'text-teal-400 hover:text-white hover:bg-slate-900'}`}>Área do Professor</button>
            )}

            {/* ABAS SEPARADAS DE SUPORTE E FAQ */}
            <button onClick={() => setActiveTab('suporte')} className={`w-full text-left px-4 py-3 rounded-xl text-sm font-medium ${activeTab === 'suporte' ? 'bg-teal-500/15 text-teal-300' : 'text-slate-400 hover:text-white hover:bg-slate-900'}`}>Suporte Técnico</button>
            <button onClick={() => setActiveTab('faq')} className={`w-full text-left px-4 py-3 rounded-xl text-sm font-medium ${activeTab === 'faq' ? 'bg-teal-500/15 text-teal-300' : 'text-slate-400 hover:text-white hover:bg-slate-900'}`}>Dúvidas / FAQ</button>

            <button onClick={() => setActiveTab('tutor')} className={`w-full text-left px-4 py-3 rounded-xl text-sm font-medium ${activeTab === 'tutor' ? 'bg-teal-500/10 text-teal-400' : 'text-slate-400 hover:text-white hover:bg-slate-900'}`}>Tutor Inteligente IA</button>
            <button onClick={() => setActiveTab('secretaria')} className={`w-full text-left px-4 py-3 rounded-xl text-sm font-medium ${activeTab === 'secretaria' ? 'bg-indigo-500/10 text-indigo-400' : 'text-slate-400 hover:text-white hover:bg-slate-900'}`}>Secretaria Acadêmica</button>
            <button onClick={() => setActiveTab('biblioteca')} className={`w-full text-left px-4 py-3 rounded-xl text-sm font-medium ${activeTab === 'biblioteca' ? 'bg-teal-500/10 text-teal-400' : 'text-slate-400 hover:text-white hover:bg-slate-900'}`}>Biblioteca Digital</button>
            <button onClick={() => setActiveTab('tfc')} className={`w-full text-left px-4 py-3 rounded-xl text-sm font-medium ${activeTab === 'tfc' ? 'bg-teal-500/10 text-teal-400' : 'text-slate-400 hover:text-white hover:bg-slate-900'}`}>Projeto Final (TFC)</button>
          </nav>
        </aside>

        {/* CONTENT AREA */}
        <main className="flex-1 min-w-0 bg-slate-950 rounded-2xl border border-slate-800 p-6 flex flex-col justify-between shadow-2xl">
          
          {/* Dashboard Aba */}
          {activeTab === 'dashboard' && (
            <div className="space-y-6 animate-fadeIn">
              <h1 className="text-2xl font-black text-white">Bem-vindo, {currentUser?.name}</h1>
              <p className="text-sm text-slate-400">Este é o painel de controle principal do Instituto EADUCAR. Navegue pelas abas para continuar seus estudos e gerenciar suas documentações.</p>
              
              <div className="bg-slate-900 p-6 rounded-2xl border border-slate-800 text-center">
                 <GraduationCap className="w-16 h-16 text-teal-500 mx-auto mb-4" />
                 <h2 className="text-xl font-bold text-white mb-2">Continue de onde parou</h2>
                 <button onClick={() => setActiveTab('trilha')} className="bg-teal-500 text-slate-950 font-bold px-6 py-3 rounded-xl text-sm shadow-lg">Acessar Trilha de Estudos</button>
              </div>
            </div>
          )}

          {/* Trilha Aba Básica */}
          {activeTab === 'trilha' && (
            <div className="space-y-6 animate-fadeIn">
               <h1 className="text-2xl font-black text-white border-b border-slate-800 pb-4">Ambiente Virtual de Aprendizagem (AVA)</h1>
               <div className="bg-slate-900 p-6 rounded-2xl border border-slate-800 text-center">
                 <Video className="w-16 h-16 text-teal-500 mx-auto mb-4" />
                 <p className="text-sm text-slate-400">Assista aos vídeos e complete as atividades para desbloquear as avaliações.</p>
               </div>
            </div>
          )}

          {/* ABA 100% EXCLUSIVA PARA SUPORTE TÉCNICO */}
          {activeTab === 'suporte' && (
            <div className="space-y-6 animate-fadeIn">
              <div className="pb-4 border-b border-slate-800">
                <span className="text-xs text-teal-400 uppercase tracking-widest font-bold">Atendimento ao Aluno</span>
                <h1 className="text-xl sm:text-2xl font-black text-white mt-1">Central de Suporte Técnico</h1>
                <p className="text-xs text-slate-400 mt-1">Abra um chamado para falar com nossa equipe pedagógica ou resolver problemas técnicos na plataforma.</p>
              </div>
              <div className="bg-slate-900 border border-slate-800 p-6 rounded-2xl max-w-2xl">
                 <form className="space-y-4" onSubmit={(e) => { e.preventDefault(); showAlert('Chamado aberto com sucesso. A equipe do Instituto EADUCAR responderá em breve.', 'success'); }}>
                    <div>
                      <label className="text-xs font-bold text-slate-400 block mb-1">Setor de Atendimento</label>
                      <select className="w-full bg-slate-950 border border-slate-800 rounded-xl px-4 py-2.5 text-xs text-white focus:border-teal-500 focus:outline-none">
                        <option>Suporte Técnico (Erros na plataforma)</option>
                        <option>Coordenação Pedagógica</option>
                        <option>Secretaria Acadêmica</option>
                        <option>Financeiro</option>
                      </select>
                    </div>
                    <div>
                      <label className="text-xs font-bold text-slate-400 block mb-1">Assunto Breve</label>
                      <input type="text" placeholder="Ex: Problema para emitir documento" className="w-full bg-slate-950 border border-slate-800 rounded-xl px-4 py-2.5 text-xs text-white focus:border-teal-500 focus:outline-none" required />
                    </div>
                    <div>
                      <label className="text-xs font-bold text-slate-400 block mb-1">Mensagem Detalhada</label>
                      <textarea rows="5" placeholder="Descreva sua solicitação ou problema..." className="w-full bg-slate-950 border border-slate-800 rounded-xl px-4 py-2.5 text-xs text-white focus:border-teal-500 focus:outline-none" required></textarea>
                    </div>
                    <button type="submit" className="bg-teal-500 hover:bg-teal-600 text-slate-950 font-bold px-6 py-2.5 rounded-xl text-xs transition flex items-center gap-2">
                      <Send className="w-4 h-4" /> Enviar Chamado
                    </button>
                 </form>
              </div>
            </div>
          )}

          {/* ABA 100% EXCLUSIVA PARA FAQ (PERGUNTAS FREQUENTES) */}
          {activeTab === 'faq' && (
            <div className="space-y-6 animate-fadeIn">
              <div className="pb-4 border-b border-slate-800">
                <span className="text-xs text-teal-400 uppercase tracking-widest font-bold">Autoatendimento</span>
                <h1 className="text-xl sm:text-2xl font-black text-white mt-1">Dúvidas Frequentes (FAQ)</h1>
                <p className="text-xs text-slate-400 mt-1">Encontre respostas rápidas para as principais dúvidas sobre a plataforma e o curso.</p>
              </div>
              <div className="space-y-3 max-w-3xl">
                 {[
                   { q: "Como funciona a avaliação oficial (P1) do Módulo I?", a: "Você deve assistir todos os vídeos e acertar os quizzes de fixação (nota 10) para liberar a Prova Oficial P1. A P1 possui duração de 3 horas, deve ser feita no prazo de 7 dias e exige nota mínima 7.0." },
                   { q: "Qual o prazo para solicitar documentos na Secretaria?", a: "O prazo regulamentar para processamento e assinatura digital pela secretaria acadêmica do EADUCAR é de 2 a 5 dias úteis." },
                   { q: "Como escolho o tema do TFC (Projeto Final)?", a: "O TFC deve ser obrigatoriamente voltado ao seu bairro de residência cadastrado no perfil, realizando um diagnóstico territorial e focando na promoção da saúde pública e educação na sua comunidade." },
                   { q: "Posso acessar pelo celular?", a: "Sim, a plataforma EADUCAR é totalmente responsiva e pode ser acessada pelo seu navegador móvel com todos os recursos." },
                   { q: "Perdi o prazo da Prova P1. O que fazer?", a: "Você precisará aguardar a liberação da Avaliação de Segunda Chamada (P2) pela Coordenação, acessando a aba 'Avaliações' na Secretaria." }
                 ].map((faq, i) => (
                   <div key={i} className="bg-slate-900 border border-slate-800 p-5 rounded-xl space-y-2 cursor-pointer hover:border-slate-700 transition" onClick={() => setActiveFaqIndex(activeFaqIndex === i ? null : i)}>
                     <div className="flex justify-between items-center">
                       <h3 className="font-bold text-sm text-slate-200">{faq.q}</h3>
                       <ChevronRight className={`w-4 h-4 text-slate-500 transition-transform ${activeFaqIndex === i ? 'rotate-90' : ''}`} />
                     </div>
                     {activeFaqIndex === i && <p className="text-xs text-slate-400 leading-relaxed pt-3 border-t border-slate-800/50">{faq.a}</p>}
                   </div>
                 ))}
              </div>
            </div>
          )}

          {/* ABA TUTOR IA - TOTALMENTE REFORMULADA E SEM SUGESTÕES LIMITADAS */}
          {activeTab === 'tutor' && (
            <div className="space-y-6 flex flex-col h-full justify-between min-h-[550px] animate-fadeIn">
              <div className="pb-4 border-b border-slate-800 flex justify-between items-center">
                <div className="space-y-1">
                  <div className="flex items-center gap-2 text-teal-400 font-bold">
                    <Bot className="w-5 h-5" />
                    <span className="text-xs uppercase tracking-widest font-bold">Inteligência Artificial Acadêmica</span>
                  </div>
                  <h1 className="text-xl sm:text-2xl font-black text-white">Tutor IA EADUCAR</h1>
                  <p className="text-xs text-slate-400">Faça perguntas sobre saúde, medicina global ou regras da instituição.</p>
                </div>
                <span className="bg-indigo-500/15 text-indigo-300 border border-indigo-500/20 text-[10px] font-bold py-1.5 px-3 rounded-xl flex items-center gap-1.5">
                  <Sparkles className="w-3.5 h-3.5 text-amber-300 animate-spin-slow" /> Conectado Globalmente
                </span>
              </div>

              {/* Chat ocupa toda a largura disponível sem barra lateral de sugestões */}
              <div className="flex-1 flex flex-col justify-between bg-slate-900/40 border border-slate-800 rounded-2xl overflow-hidden h-[500px]">
                <div className="flex-1 overflow-y-auto p-6 space-y-5">
                  {chatMessages.map((msg) => {
                    const isBot = msg.sender === 'bot';
                    return (
                      <div key={msg.id} className={`flex items-start gap-3 max-w-[90%] ${isBot ? 'self-start mr-auto' : 'self-end ml-auto flex-row-reverse'}`}>
                        <div className={`w-10 h-10 rounded-xl flex items-center justify-center font-bold flex-shrink-0 ${isBot ? 'bg-teal-500 text-slate-950 shadow-lg' : 'bg-indigo-600 text-white'}`}>
                          {isBot ? <Bot className="w-5 h-5" /> : currentUser?.avatar}
                        </div>
                        <div className={`p-4 rounded-2xl text-sm leading-relaxed ${isBot ? 'bg-slate-900 border border-slate-800 text-slate-200 rounded-tl-sm shadow-md' : 'bg-indigo-600 text-white rounded-tr-sm shadow-md'}`}>
                          <p className="whitespace-pre-line">{msg.text}</p>
                        </div>
                      </div>
                    );
                  })}
                  {isChatLoading && (
                    <div className="flex items-start gap-3 max-w-[85%] self-start mr-auto">
                      <div className="w-10 h-10 rounded-xl bg-teal-500 text-slate-950 flex items-center justify-center flex-shrink-0 shadow-lg">
                        <Bot className="w-5 h-5 animate-pulse" />
                      </div>
                      <div className="p-4 rounded-2xl bg-slate-900 border border-slate-800 text-sm text-slate-400 italic flex items-center gap-2 shadow-md">
                        <span className="w-2 h-2 rounded-full bg-teal-400 animate-bounce"></span>
                        <span className="w-2 h-2 rounded-full bg-teal-400 animate-bounce [animation-delay:0.2s]"></span>
                        <span>O Tutor IA está processando e pesquisando sua dúvida...</span>
                      </div>
                    </div>
                  )}
                  <div ref={messagesEndRef} />
                </div>

                <form onSubmit={handleSendMessage} className="bg-slate-950 p-4 border-t border-slate-800 flex gap-3">
                  <input
                    type="text"
                    value={chatInput}
                    onChange={(e) => setChatInput(e.target.value)}
                    placeholder="Digite sua pergunta médica, técnica ou sobre o Instituto EADUCAR..."
                    className="flex-1 bg-slate-900 border border-slate-700 focus:border-teal-500 focus:outline-none rounded-xl px-5 py-3.5 text-sm text-white shadow-inner transition-all"
                  />
                  <button type="submit" className="bg-teal-500 hover:bg-teal-600 text-slate-950 font-bold px-6 rounded-xl text-sm transition shadow-lg flex items-center gap-2">
                    <Send className="w-4 h-4" /> Enviar
                  </button>
                </form>
              </div>
            </div>
          )}

          {/* Outras Abas Placeholder */}
          {['secretaria', 'documentos', 'biblioteca', 'tfc', 'admin', 'professor'].includes(activeTab) && activeTab !== 'tutor' && activeTab !== 'suporte' && activeTab !== 'faq' && activeTab !== 'trilha' && activeTab !== 'dashboard' && (
             <div className="bg-slate-900 p-8 rounded-2xl border border-slate-800 text-center animate-fadeIn">
                <FileText className="w-16 h-16 text-teal-500 mx-auto mb-4" />
                <h2 className="text-xl font-bold text-white mb-2">Aba {activeTab.toUpperCase()}</h2>
                <p className="text-sm text-slate-400">Conteúdo simulado ativo. Navegue pelas outras opções para explorar a plataforma educacional.</p>
             </div>
          )}

        </main>
      </div>

      {}
      <footer className="bg-slate-950 border-t border-slate-800 py-6 mt-auto">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col md:flex-row justify-between items-center gap-4">
          <div className="flex items-center gap-2">
            <GraduationCap className="w-5 h-5 text-teal-400" />
            <span className="text-white font-bold text-sm">Instituto EADUCAR</span>
          </div>
          
          <div className="flex flex-wrap items-center justify-center gap-6 text-xs font-semibold text-slate-400">
            <a href="https://wa.me/5594981380299" target="_blank" rel="noreferrer" className="flex items-center gap-2 hover:text-teal-400 transition">
              <Phone className="w-4 h-4" /> (94) 98138-0299
            </a>
            <a href="https://instagram.com/institutoeaducar" target="_blank" rel="noreferrer" className="flex items-center gap-2 hover:text-teal-400 transition">
              <Instagram className="w-4 h-4" /> @institutoeaducar
            </a>
            <a href="mailto:institutoeaducar@gmail.com" className="flex items-center gap-2 hover:text-teal-400 transition">
              <Mail className="w-4 h-4" /> institutoeaducar@gmail.com
            </a>
          </div>
        </div>
      </footer>

      {/* Notificações do Sistema */}
      {systemAlert && (
        <div className="fixed bottom-6 right-6 z-50 animate-fadeIn">
          <div className={`flex items-center gap-3 px-5 py-3.5 rounded-xl text-xs font-bold shadow-2xl border ${systemAlert.type === 'error' ? 'bg-red-950/90 text-red-400 border-red-500/50' : 'bg-slate-900 border-teal-500/50 text-teal-400'}`}>
            {systemAlert.type === 'error' ? <AlertCircle className="w-5 h-5" /> : <CheckCircle2 className="w-5 h-5" />}
            <span>{systemAlert.message}</span>
            <button onClick={() => setSystemAlert(null)} className="ml-2 hover:opacity-70"><X className="w-4 h-4" /></button>
          </div>
        </div>
      )}

    </div>
  );
}
