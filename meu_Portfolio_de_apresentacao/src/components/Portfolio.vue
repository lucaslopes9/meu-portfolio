<script setup lang="ts">
import { ref, computed } from 'vue'

import certificadoTecnico from '../assets/Certificado_Desenvolvedor_web.pdf';

defineEmits(['voltar'])

// 1. Botões de filtro superiores baseados nas camadas da Stack
const filtros = ref([
  { id: 'todos', nome: 'Todos', icone: '📂' },
  { id: 'web_base', nome: 'Web Base', icone: '🌐' },
  { id: 'git', nome: 'Git e GitHub', icone: '🐙' },
  { id: 'frameworks', nome: 'Frameworks', icone: '🟢' },
  { id: 'banco_dados', nome: 'Banco de Dados', icone: '🗄️' },
  { id: 'back_end', nome: 'Back-End', icone: '⚙️' }
])

const filtroSelecionado = ref('todos')

// 2. Seus Sistemas (Todos alinhados com a nova propriedade git)
const meusProjetos = ref([
  {
    id: 1,
    titulo: 'UaiGo - App de Mobilidade',
    descricao: 'Aplicativo de corrida compartilhado com rastreamento e mapas em tempo real para motoristas e passageiros.',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: ['React Native'],
    banco_dados: ['Firebase'],
    git: [],
    back_end: ['Node.js'],
    link: '#',
    imagem: 'https://images.unsplash.com/photo-1549576490-b0b4831ef60a?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 5,
    titulo: 'Relógio Digital Dinâmico',
    descricao: 'Aplicação web interativa que realiza consumo de API externa para sincronização da hora real em tempo real, utilizando manipulação de estado do DOM para alternância de temas visuais (Dark/Light Mode).',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: [],
    banco_dados: [],
    git: ['Git', 'GitHub'], // <-- CORRIGIDO: Chave correta e tags adicionadas
    back_end: [],
    link: 'https://relogio-digital-zeta.vercel.app/',
    imagem: 'https://images.unsplash.com/photo-1508962914676-134849a727f0?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 2,
    titulo: 'Conecta Talentos',
    descricao: 'Plataforma corporativa web de recrutamento, triagem e vagas de emprego automatizadas para o mercado de trabalho.',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: ['Vue.js'],
    banco_dados: ['PostgreSQL'],
    git: [],
    git: ['Git', 'GitHub'],
    back_end: ['Node.js'],
    link: 'https://conecta-talentos-lope.vercel.app',
    imagem: 'https://images.unsplash.com/photo-1586281380349-632531db7ed4?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 3,
    titulo: 'Sistema de Rifas Automatizado',
    descricao: 'Plataforma de sorteios online com geração de cotas e integração completa de pagamentos via Multicaixa Express.',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: ['Vue.js'],
    banco_dados: ['MySQL'],
    git: ['Git', 'GitHub'],
    back_end: ['PHP', 'Laravel'],
    link: '#',
    imagem: 'https://images.unsplash.com/photo-1518609878373-06d740f60d8b?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 6,
    titulo: 'Make Your Dog',
    descricao: 'Sistema completo e responsivo, para gerenciamento, personalização e pedidos de montagem de cachorros-quentes gourmet.',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: ['Vue.js', 'Vue Router'],
    banco_dados: ['JSON Server'],
    git: ['Git', 'GitHub'],
    back_end: ['Node.js'],
    link: 'https://makeyour-d-og-oficial-neon.vercel.app/', 
    imagem: 'https://images.unsplash.com/photo-1619740455993-9e612b1af08a?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 7,
    titulo: 'Loja Virtual de Jogos',
    descricao: '🏆 [PROJETO DE CONCLUSÃO DE CURSO LIVRE: desenvolvimento web] Um e-commerce interativo com catálogo responsivo, carrinho de compras funcional e filtros de busca avançados.',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: [],
    banco_dados: [],
    git: ['Git', 'GitHub'], // <-- Adicionado para você poder filtrar este também por Git
    back_end: [],
    link: 'https://loja-virtual-de-jogos-finalizada.vercel.app',
    certificado: certificadoTecnico,
    imagem: 'https://images.unsplash.com/photo-1538481199705-c710c4e965fc?w=500&auto=format&fit=crop&q=60'
  },

 {
    id: 8,
    titulo: 'Codifica Projeto Chat',
    descricao: 'Projeto de chat desenvolvido durante o curso livre de desenvolvimento web que simula a comunicação em tempo real entre dois usuários. A aplicação utiliza manipulação dinâmica do DOM e lógica de programação para renderização de mensagens e controle de fluxos da interface.',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: [], 
    banco_dados: [], 
    git: ['Git', 'GitHub'],
    back_end: [], 
    certificado: certificadoTecnico,
    link: 'https://codifica-projeto-chat.vercel.app/',
    imagem: 'https://images.unsplash.com/photo-1611532736597-de2d4265fba3?w=500&auto=format&fit=crop&q=60'
  }







])

// 3. Filtro dinâmico inteligente pelas camadas da Stack
const projetosFiltrados = computed(() => {
  const filtro = filtroSelecionado.value
  if (filtro === 'todos') {
    return meusProjetos.value
  }
  return meusProjetos.value.filter(projeto => {
    const categoria = projeto[filtro as keyof typeof projeto]
    return Array.isArray(categoria) && categoria.length > 0
  })
})

function selecionarFiltro(id: string) {
  filtroSelecionado.value = id
}
</script>

<template>
  <section class="portfolio-page">
    
    <div class="portfolio-header">
      <button @click="$emit('voltar')" class="btn-back">← Voltar para Home</button>
      <h1>Meus Projetos &amp; Sistemas</h1>
      <p>Selecione uma das camadas da stack abaixo para filtrar as soluções desenvolvidas.</p>
    </div>

    <div class="tech-filters-container">
      <div 
        v-for="item in filtros" 
        :key="item.id"
        class="tech-filter-card"
        :class="{ 'active-card': filtroSelecionado === item.id }"
        @click="selecionarFiltro(item.id)"
      >
        <span class="tech-icon">{{ item.icone }}</span>
        <h3>{{ item.nome }}</h3>
      </div>
    </div>

    <div class="projects-grid">
      <div 
        v-for="projeto in projetosFiltrados" 
        :key="projeto.id" 
        class="project-card"
      >
        <div class="project-image">
          <img :src="projeto.imagem" :alt="projeto.titulo" />
        </div>
        
        <div class="project-info">
          <h2>{{ projeto.titulo }}</h2>
          <p>{{ projeto.descricao }}</p>
          
          <div class="tech-groups-container">
            <div v-if="projeto.web_base.length > 0" class="tech-group-row">
              <span class="group-label">Web Base:</span>
              <div class="project-tags">
                <span v-for="t in projeto.web_base" :key="t" class="tag tag-base">{{ t }}</span>
              </div>
            </div>

            <div v-if="projeto.git && projeto.git.length > 0" class="tech-group-row">
              <span class="group-label">Git / GitHub:</span>
              <div class="project-tags">
                <span v-for="t in projeto.git" :key="t" class="tag tag-back">{{ t }}</span>
              </div>
            </div>

            <div v-if="projeto.frameworks.length > 0" class="tech-group-row">
              <span class="group-label">Frameworks:</span>
              <div class="project-tags">
                <span v-for="t in projeto.frameworks" :key="t" class="tag tag-framework">{{ t }}</span>
              </div>
            </div>

            <div v-if="projeto.banco_dados.length > 0" class="tech-group-row">
              <span class="group-label">Banco de Dados:</span>
              <div class="project-tags">
                <span v-for="t in projeto.banco_dados" :key="t" class="tag tag-db">{{ t }}</span>
              </div>
            </div>

            <div v-if="projeto.back_end.length > 0" class="tech-group-row">
              <span class="group-label">Back-End:</span>
              <div class="project-tags">
                <span v-for="t in projeto.back_end" :key="t" class="tag tag-back">{{ t }}</span>
              </div>
            </div>
          </div>
          
          <div class="project-actions">
            <a :href="projeto.link" target="_blank" rel="noopener" class="btn-project-link">
              Acessar Sistema →
            </a>
            
            <a v-if="projeto.certificado" :href="projeto.certificado" target="_blank" rel="noopener" class="btn-certificate-link">
              🏅 Ver Certificado
            </a>
          </div>
        </div>
      </div>
    </div>

  </section>
</template>

<style scoped>
/* --- CONFIGURAÇÃO GERAL DA PÁGINA --- */
.portfolio-page {
  width: 100%;
  min-height: 100vh;
  padding: 40px 20px 80px 20px;
  background-color: #1a1a1a; 
  color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.portfolio-header {
  text-align: center;
  max-width: 700px;
  margin-bottom: 50px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
}

.btn-back {
  background: transparent;
  border: 1px solid #42b883;
  color: #42b883;
  padding: 8px 18px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  transition: 0.3s ease;
}

.btn-back:hover {
  background-color: #42b883;
  color: #1a1a1a;
}

.portfolio-header h1 {
  font-size: 2.5rem;
  font-weight: 700;
}

.portfolio-header p {
  color: #aaaaaa;
  font-size: 1.1rem;
}

/* --- ESTILO DOS CARTÕES DE FILTRO --- */
.tech-filters-container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 20px;
  width: 100%;
  max-width: 1000px;
  margin-bottom: 60px;
}

.tech-filter-card {
  background-color: #1f1f1f;
  border: 2px solid #2a2a2a;
  padding: 20px 25px;
  border-radius: 12px;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  min-width: 150px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 5px 15px rgba(0,0,0,0.2);
}

.tech-icon {
  font-size: 1.8rem;
  background-color: #0b5394;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
}

.tech-filter-card:hover {
  border-color: #42b883;
  transform: translateY(-4px);
}

.tech-filter-card.active-card {
  background-color: #242424;
  border-color: #42b883;
  box-shadow: 0 0 20px rgba(66, 184, 131, 0.3);
}

.tech-filter-card h3 {
  font-size: 0.95rem;
  color: white;
  font-weight: 600;
}

/* --- GRID E CAIXAS DOS SISTEMAS FINAIS --- */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr); 
  gap: 40px;
  width: 100%;
  max-width: 1100px;
}

.project-card {
  background-color: #1f1f1f;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0,0,0,0.4);
  border: 1px solid #2a2a2a;
  display: flex;
  flex-direction: column;
  transition: all 0.3s ease;
}

.project-image img {
  width: 100%;
  height: 220px;
  object-fit: cover;
  border-bottom: 1px solid #2a2a2a;
}

.project-info {
  padding: 25px;
  display: flex;
  flex-direction: column;
  gap: 15px;
  flex: 1;
}

.project-info h2 {
  font-size: 1.4rem;
  color: white;
  font-weight: 700;
}

.project-info p {
  color: #cccccc;
  font-size: 0.95rem;
  line-height: 1.6;
}

/* CONTAINER DOS CONJUNTOS INTERNOS DE TECNOLOGIA */
.tech-groups-container {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-top: 10px;
  background-color: #151515;
  padding: 15px;
  border-radius: 8px;
  border: 1px solid #262626;
}

.tech-group-row {
  display: flex;
  align-items: center;
  gap: 10px;
}

.group-label {
  font-size: 0.8rem;
  font-weight: 700;
  color: #888888;
  min-width: 110px;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.tag {
  font-size: 0.7rem;
  font-weight: 700;
  padding: 3px 8px;
  border-radius: 4px;
  letter-spacing: 0.3px;
}

.tag-base { background-color: #2c3e50; color: #bfecff; }
.tag-framework { background-color: #1e4620; color: #85e3b3; }
.tag-db { background-color: #b37d14; color: #ffeebf; }
.tag-back { background-color: #4d235a; color: #f7bfff; }

/* CONTAINER DAS AÇÕES - ALINHAMENTO CORRIGIDO */
.project-actions {
  display: flex;
  gap: 20px;
  align-items: center;
  margin-top: auto;
  padding-top: 15px;
}

.btn-project-link {
  color: #42b883;
  text-decoration: none;
  font-weight: bold;
  font-size: 0.95rem;
  transition: 0.2s ease;
}

.btn-project-link:hover {
  color: white;
  padding-left: 4px;
}

/* NOVO ESTILO DO BOTÃO DE CERTIFICADO */
.btn-certificate-link {
  color: #ffc107;
  text-decoration: none;
  font-weight: bold;
  font-size: 0.95rem;
  transition: 0.2s ease;
  cursor: pointer;
}

.btn-certificate-link:hover {
  color: white;
  transform: translateY(-1px);
}

/* --- RESPONSIVIDADE --- */
@media (max-width: 768px) {
  .projects-grid {
    grid-template-columns: 1fr; 
    gap: 30px;
  }
  .portfolio-header h1 { font-size: 2rem; }
  .tech-filters-container { gap: 12px; }
  .tech-filter-card { min-width: 120px; padding: 15px; }
  .tech-group-row { flex-direction: column; align-items: flex-start; gap: 5px; }
  .project-actions { flex-direction: column; align-items: flex-start; gap: 10px; }
}
</style>