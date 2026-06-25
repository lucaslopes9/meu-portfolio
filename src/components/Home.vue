<script setup lang="ts">
import { ref, computed } from 'vue'
// Importe o seu componente de Portfólio aqui (ajuste o caminho se necessário)
import Portfolio from './Portfolio.vue' 

// Importando o PDF dinamicamente com o caminho relativo correto e nome limpo
import curriculoPdf from '../assets/Curriculo Lucas-Lopes-Desenvolvedor.pdf'

// Controle de qual tela está visível: 'home' ou 'portfolio'
const telaAtiva = ref('home')

// Controle de Idioma
const idiomaAtual = ref<'pt' | 'en'>('pt')

function alternarIdioma() {
  idiomaAtual.value = idiomaAtual.value === 'pt' ? 'en' : 'pt'
}

// Dicionário de Textos
const textos = {
  pt: {
    faleComigo: 'Fale Comigo',
    home: 'Home',
    sobre: 'Sobre mim',
    servicos: 'Serviços',
    tecnologias: 'Tecnologias',
    portfolio: 'Portfólio',
    curriculo: 'Baixe meu Currículo',
    heroH1: 'Você achou a melhor agência digital',
    heroSub: 'Desenvolvedor Full Stack',
    heroDesc: 'Desenvolvedor Full Stack especializado na criação de sistemas, sites e aplicativos mobile sob medida para elevar a presença online e a eficiência do seu negócio. Combino tecnologia de ponta, design moderno e estratégias inteligentes para transformar ideias inovadoras em soluções digitais que geram resultados reais e impulsionam seus canais de vendas. Estou pronto para tirar o seu projeto do papel e transformá-lo em sucesso.',
    btnHero: 'Veja meu Portfólio',
    servicosH1: 'O que posso fazer pelo seu negócio',
    servicosDesc: 'Transformo suas necessidades em soluções robustas, eficientes e escaláveis. Utilizo as melhores tecnologias do mercado para entregar sistemas inovadores, sites de alta conversão e aplicativos modernos.',
    s1Titulo: 'Criação de Sites e Sistemas',
    s1Desc: 'Development of platforms modern, rápidas e responsivas, focadas em usabilidade e na melhor experiência para o Usuário.',
    s2Titulo: 'Soluções Mobile',
    s2Desc: 'Criação de aplicativos nativos e híbridos intuitivos, com foco em performance e interface moderna para conectar sua marca aos usuários mobile.',
    s3Titulo: 'Infraestrutura Cloud & AWS',
    s3Desc: 'Sua aplicação trava ou fica lenta quando recebe muitos acessos? Eu configuro a arquitetura técnica que sustenta o seu crescimento: servidores escaláveis na AWS.',
    s4Titulo: 'Identidade Visual',
    s4Desc: 'Criação de identidades visuais estratégicas, desde logotipos até sistemas de aplicação, garantindo consistência e conexão com seu público.',
    sobreH2: 'Sobre Me',
    sobreH3: 'Profissional focado em transformar código em valor de negócio',
    sobreP1: 'Muito prazer! Eu sou o Lucas, desenvolvedor de software especializado em criar sistemas robustos, aplicativos dinâmicos e sites de alta conversão. Minha missão é entender as dores do seu negócio e construir a ferramenta digital exata para resolver seus problemas e automatizar seus processos.',
    sobreP2: 'Com uma sólida bagagem técnica e um olhar estratégico, busco entregar produtos que não apenas funcionam perfeitamente, mas que oferecem uma experiência incrível e geram resultados reais de faturamento e engajamento.',
    btnSobre: 'Vamos conversar?',
    techH1: 'Minha Stack Técnica',
    techP: 'Um mapa visual das tecnologias e ferramentas que utilizo no meu dia a dia profissional.',
    footerDesc: 'Transformando ideias complexas em aplicações web e mobile de alto impacto. Pronto para levar a sua empresa ao próximo nível digital.',
    footerNav: 'Navegação',
    footerContatoDesc: 'Tem um projeto em mente? Vamos construir juntos!',
    btnFooter: 'Iniciar Projeto'
  },
  en: {
    faleComigo: 'Contact Me',
    home: 'Home',
    sobre: 'About me',
    servicos: 'Services',
    tecnologias: 'Technologies',
    portfolio: 'Portfolio',
    curriculo: 'Download Resume',
    heroH1: 'You found the best digital agency',
    heroSub: 'Full Stack Developer',
    heroDesc: 'Full Stack Developer specialized in creating custom systems, websites, and mobile applications to elevate your online presence and business efficiency. I combine cutting-edge technology, modern design, and smart strategies to transform innovative ideas into digital solutions that deliver real results and drive your sales channels. I am ready to get your project off the paper and turn it into success.',
    btnHero: 'View My Portfolio',
    servicosH1: 'What I can do for your business',
    servicosDesc: 'I transform your needs into robust, efficient, and scalable solutions. I use the best technologies on the market to deliver innovative systems, high-converting websites, and modern applications.',
    s1Titulo: 'Websites & Systems Creation',
    s1Desc: 'Development of modern, fast, and responsive platforms, focused on usability and the best User Experience.',
    s2Titulo: 'Mobile Solutions',
    s2Desc: 'Creation of intuitive native and hybrid applications, focusing on performance and modern interfaces to connect your brand to mobile users.',
    s3Titulo: 'Cloud Infrastructure & AWS',
    s3Desc: 'Does your application crash or slow down under high traffic? I configure the technical architecture that supports your growth: scalable servers on AWS.',
    s4Titulo: 'Visual Identity',
    s4Desc: 'Creation of strategic visual identities, from logos to application systems, ensuring consistency and connection with your audience.',
    sobreH2: 'About Me',
    sobreH3: 'Professional focused on turning code into business value',
    sobreP1: 'Nice to meet you! I am Lucas, a software developer specialized in creating robust systems, dynamic applications, and high-converting websites. My mission is to understand your business pain points and build the exact digital tool to solve your problems and automate your processes.',
    sobreP2: 'With a solid technical background and a strategic mindset, I aim to deliver products that not only work perfectly but also offer an incredible experience and generate real revenue and engagement results.',
    btnSobre: 'Let\'s talk?',
    techH1: 'My Technical Stack',
    techP: 'A visual map of the technologies and tools I use in my professional daily routine.',
    footerDesc: 'Transforming complex ideas into high-impact web and mobile applications. Ready to take your company to the next digital level.',
    footerNav: 'Navigation',
    footerContatoDesc: 'Have a project in mind? Let\'s build it together!',
    btnFooter: 'Start Project'
  }
}

// Computed property para pegar os textos reativos baseados no idioma selecionado
const t = computed(() => textos[idiomaAtual.value])

// Função para mudar de tela e gerenciar a rolagem
function navegarPara(tela: string, secaoId?: string) {
  telaAtiva.value = tela
  
  if (secaoId) {
    setTimeout(() => {
      const elemento = document.getElementById(secaoId)
      if (elemento) {
        elemento.scrollIntoView({ behavior: 'smooth' })
      }
    }, 50)
  } else {
    window.scrollTo({ top: 0, behavior: 'smooth' })
  }
}
</script>

<template>
  <div class="top-header">
    <div class="contato-link">
     <a href="https://wa.me/5519971630276?text=Olá%20Lucas,%20vi%20seu%20portfólio%20e%20gostaria%20de%20conversar%20sobre%20um%20projeto!" target="_blank" rel="noopener">{{ t.faleComigo }}</a>
    </div> 
    
    <div class="seletor-idioma">
      <button @click="alternarIdioma" class="btn-idioma">
        🌐 {{ idiomaAtual === 'pt' ? 'EN' : 'PT' }}
      </button>
    </div>

    <div class="redes-sociais">
      <a href="https://linkedin.com" target="_blank" rel="noopener">LinkedIn</a>
      <a href="https://github.com" target="_blank" rel="noopener">GitHub</a>
     <a href="https://wa.me/5519971630276?text=Olá%20Lucas,%20gostaria%20de%20fazer%20um%20orçamento." target="_blank" rel="noopener">WhatsApp</a>
    </div>
  </div>

  <header class="meu-header">
    <div class="logo-container">
      <h2 style="cursor: pointer" @click="navegarPara('home')">lucas.dev</h2>
    </div>

    <nav class="menu-container">
      <a href="#" @click.prevent="navegarPara('home')">{{ t.home }}</a>
      <a href="#" @click.prevent="navegarPara('home', 'sobre')">{{ t.sobre }}</a>
      <a href="#" @click.prevent="navegarPara('home', 'servicos')">{{ t.servicos }}</a>
      <a href="#" @click.prevent="navegarPara('home', 'tecnologias')">{{ t.tecnologias }}</a>
      <a href="#" @click.prevent="navegarPara('portfolio')">{{ t.portfolio }}</a>

<a :href="curriculoPdf" download="Curriculo_Lucas_Lopes.pdf" target="_blank">{{ t.curriculo }}</a>    </nav> 
  </header>

  <Portfolio v-if="telaAtiva === 'portfolio'" @voltar="navegarPara('home')" />

  <div v-else>
    <section class="hero-section">
      <div class="hero-content">
        <h1>{{ t.heroH1 }}</h1>
        <h3>{{ t.heroSub }}</h3>
        <p>{{ t.heroDesc }}</p>
        <a href="#" @click.prevent="navegarPara('portfolio')" class="btn-primary">{{ t.btnHero }}</a>
      </div>

      <div class="hero-image">
         <img src="@/assets/fundo_transparente-removebg-preview.png" alt="Fundo">
      </div>
    </section>

    <section id="servicos" class="services-section"> 
      <div class="services-header">
        <h1>{{ t.servicosH1 }}</h1>
        <p>{{ t.servicosDesc }}</p>
      </div>

      <div class="cards-container">
        <div class="service-card light-card">
          <div class="icon-circle"><span class="icon-placeholder">💻</span></div>
          <h2>{{ t.s1Titulo }}</h2>
          <p>{{ t.s1Desc }}</p>
        </div>

        <div class="service-card gradient-card">
          <div class="icon-circle"><span class="icon-placeholder">▶</span></div>
          <h2>{{ t.s2Titulo }}</h2>
          <p>{{ t.s2Desc }}</p>
        </div>

        <div class="service-card light-card">
          <div class="icon-circle"><span class="icon-placeholder">aws</span></div>
          <h2>{{ t.s3Titulo }}</h2>
          <p>{{ t.s3Desc }}</p>
        </div>

        <div class="service-card gradient-card">
          <div class="icon-circle"><span class="icon-placeholder">🖼️</span></div>
          <h2>{{ t.s4Titulo }}</h2>
          <p>{{ t.s4Desc }}</p>
        </div>
      </div>
    </section>

    <section id="sobre" class="about-section">
      <div class="about-container">
        <div class="about-image">
          <img src="@/assets/Gemini_Generated_Braçços_cruzados.png" alt="Foto de Lucas" />
        </div>

        <div class="about-content">
          <h2>{{ t.sobreH2 }}</h2>
          <h3>{{ t.sobreH3 }}</h3>
          <p>{{ t.sobreP1 }}</p>
          <p>{{ t.sobreP2 }}</p>
          <a href="#contato" @click.prevent="navegarPara('home', 'contato')" class="btn-secondary-outline">{{ t.btnSobre }}</a>
        </div>
      </div>
    </section>

    <section id="tecnologias" class="tech-section">
      <div class="tech-header">
        <h1>{{ t.techH1 }}</h1>
        <p>{{ t.techP }}</p>
      </div>

      <div class="tech-tree">
        <div class="tech-branch">
          <div class="branch-title">Front-End Skills</div>
          <div class="branch-connector"></div>
          <div class="tech-box">
            <ul>
              <li>HTML5, CSS3, JavaScript (ES6+)</li>
              <li>Vue.js / Angular</li>
              <li>React / React Native</li>
            </ul>
          </div>
        </div>
        <div class="tech-branch">
          <div class="branch-title">Back-End Skills</div>
          <div class="branch-connector"></div>
          <div class="tech-box">
            <ul>
              <li>Node.js / C# (.NET)</li>
              <li>PHP (Laravel)</li>
              <li>Python (Flask)</li>
            </ul>
          </div>
        </div>
        <div class="tech-branch">
          <div class="branch-title">Database Skills</div>
          <div class="branch-connector"></div>
          <div class="tech-box">
            <ul>
              <li>MySQL / MariaDB</li>
              <li>Firebase</li>
              <li>SQL Server</li>
            </ul>
          </div>
        </div>
        <div class="tech-branch">
          <div class="branch-title">Basic Design</div>
          <div class="branch-connector"></div>
          <div class="tech-box">
            <ul>
              <li>UI / UX / Figma</li>
              <li>Design Responsivo</li>
            </ul>
          </div>
        </div>
        <div class="tech-branch">
          <div class="branch-title">Web Hosting</div>
          <div class="branch-connector"></div>
          <div class="tech-box">
            <ul>
              <li>Vercel / Netlify</li>
              <li>AWS Cloud / Docker</li>
            </ul>
          </div>
        </div>
        <div class="tech-branch">
          <div class="branch-title">Version Control</div>
          <div class="branch-connector"></div>
          <div class="tech-box">
            <ul>
              <li>Git / GitHub</li>
            </ul>
          </div>
        </div>
      </div>
    </section>
  </div>

  <section id="contato" class="footer-section">
    <div class="footer-container">
      <div class="footer-box brand-box">
        <h2>lucas.dev</h2>
        <p>{{ t.footerDesc }}</p>
        <span class="copyright">© 2026 lucas.dev. Todos os direitos reservados.</span>
      </div>

      <div class="footer-box links-box">
        <h3>{{ t.footerNav }}</h3>
        <ul>
          <li><a href="#" @click.prevent="navegarPara('home')">{{ t.home }}</a></li>
          <li><a href="#" @click.prevent="navegarPara('home', 'sobre')">{{ t.sobre }}</a></li>
          <li><a href="#" @click.prevent="navegarPara('home', 'servicos')">{{ t.servicos }}</a></li>
          <li><a href="#" @click.prevent="navegarPara('portfolio')">{{ t.portfolio }}</a></li>
        </ul>
      </div>

      <div class="footer-box contact-box">
        <h3>{{ t.servicos }}</h3>
        <p>{{ t.footerContatoDesc }}</p>
        <ul class="contact-list">
          <li>📧 lucas@labtech.software</li>
          <li>📱 (19) 971630276</li>
          <li>📍 Brasil</li>
        </ul>
        <a href="https://wa.me/seu-numero" target="_blank" rel="noopener" class="btn-footer">
          {{ t.btnFooter }}
        </a>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* --- TOP HEADER --- */
.top-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 8px 20px;
  background-color: #111111;
  border-bottom: 1px solid #2a2a2a;
  font-size: 0.9rem;
}

.top-header a {
  color: #888888;
  text-decoration: none;
  transition: 0.3s;
}

.top-header a:hover {
  color: #42b883;
}

.redes-sociais {
  display: flex;
  gap: 15px;
}

/* --- HEADER PRINCIPAL --- */
.meu-header {
  display: flex;       
  width: 100%;         
  padding: 20px;
  background-color: #1a1a1a; 
  color: white;
  border-bottom: 1px solid #2a2a2a;
}

.logo-container {
  flex: 1;              
  display: flex;
  align-items: center; 
}

.menu-container {
  flex: 1;              
  display: flex;
  justify-content: flex-end; 
  align-items: center;     
  gap: 20px;                
}

.menu-container a {
  color: #42b883;          
  text-decoration: none;
  font-weight: bold;
  transition: 0.3s;
}

.menu-container a:hover {
  color: white;            
}

/* --- HERO SECTION --- */
.hero-section {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  min-height: calc(100vh - 120px); 
  padding: 40px 20px;
  background-color: #2E3A46;
  color: white;
  gap: 40px;

  /* === ADICIONE ESSAS 3 LINHAS ABAIXO === */
  animation: fadeInHero 1.5s ease-out forwards;
  opacity: 0; /* Começa invisível para o efeito funcionar */
}

.hero-content {
  flex: 1; 
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.hero-content h1 {
  font-size: 3rem;
  font-weight: 700;
  color: white;
}

.hero-content h3 {
  font-size: 1.5rem;
  color: #42b883; 
}

.hero-content p {
  font-size: 1.1rem;
  color: #cccccc;
  line-height: 1.6;
  max-width: 500px;
}

.btn-primary {
  display: inline-block;
  align-self: center; 
  padding: 12px 24px;
  background-color: #42b883;
  color: #1a1a1a;
  text-decoration: none;
  font-weight: bold;
  border-radius: 4px;
  transition: 0.3s;
}

.btn-primary:hover {
  background-color: white;
  transform: translateY(-2px); 
}

.hero-image {
  flex: 1; 
  display: flex;
  justify-content: center;
  align-items: center;
}

.hero-image img {
  max-width: 100%;
  height: auto;
  border-radius: 8px; 
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5); 
}

/* --- SEÇÃO DE SERVIÇOS --- */
.services-section {
  width: 100%;
  padding: 80px 20px;
  background-color: #1a1a1a;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.services-header {
  text-align: center;
  max-width: 800px;
  margin-bottom: 60px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.services-header h1 {
  font-size: 2.5rem;
  font-weight: 700;
  color: white;
  position: relative;
  display: inline-block;
  padding-bottom: 10px;
}

.services-header h1::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 4px;
  background-color: #42b883;
  border-radius: 2px;
}

.services-header p {
  font-size: 1.15rem;
  color: #cccccc;
  line-height: 1.7;
}

/* --- GRID / CONTAINER DOS CARTÕES --- */
.cards-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 25px;
  width: 100%;
  max-width: 1200px;
  padding: 0 10px;
}

.service-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding: 40px 25px;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.service-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 35px rgba(66, 184, 131, 0.2);
}

.icon-circle {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  background-color: #5dade2;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 25px;
  color: white;
  font-weight: bold;
}

.icon-placeholder {
  font-size: 1.8rem;
}

/* Cartões Claros */
.light-card {
  background-color: #f9f9f9;
  color: #1a1a1a;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.light-card h2 {
  color: #5dade2;
  font-size: 1.4rem;
  font-weight: 700;
  margin-bottom: 15px;
}

.light-card p {
  color: #555555;
  font-size: 0.95rem;
  line-height: 1.6;
}

/* Cartões Escuros Gradientes */
.gradient-card {
  background: linear-gradient(to bottom, #2ecc71 0%, #1e4620 50%, #111111 100%);
  color: white;
}

.gradient-card h2 {
  color: #85e3b3;
  font-size: 1.4rem;
  font-weight: 700;
  margin-bottom: 15px;
}

.gradient-card p {
  color: #e0e0e0;
  font-size: 0.95rem;
  line-height: 1.6;
}

/* --- RESPONSIVIDADE --- */
@media (max-width: 1024px) {
  .cards-container {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .hero-section {
    flex-direction: column-reverse; 
    text-align: center;
    padding: 20px;
  }

  .hero-content {
    align-items: center;
  }

  .hero-content h1 {
    font-size: 2.2rem;
  }

  .btn-primary {
    align-self: center; 
  }

  .services-section {
    padding: 60px 20px;
  }
  
  .services-header h1 {
    font-size: 2rem;
  }

  .services-header p {
    font-size: 1rem;
  }

  .cards-container {
    grid-template-columns: 1fr;
    gap: 20px;
  }
}

.greetings {
  margin-top: 40px;
  text-align: center;
}

/* --- 3* SEÇÃO SOBRE MIM --- */
.about-section {
  width: 100%;
  padding: 100px 20px;
  background-color: #1f1f1f;
  color: white;
  display: flex;
  justify-content: center;
}

.about-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  max-width: 1200px;
  gap: 60px;
}

/* Bloco da Foto */
.about-image {
  flex: 1;
  display: flex;
  justify-content: center;
}

.about-image img {
  max-width: 100%;
  max-height: 400px;
  border-radius: 12px;
  border: 2px solid #42b883;
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.6);
  object-fit: cover;
}

/* Bloco do Texto */
.about-content {
  flex: 1.2;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.about-content h2 {
  font-size: 2.5rem;
  font-weight: 700;
  color: #42b883;
}

.about-content h3 {
  font-size: 1.4rem;
  color: #ffffff;
  font-weight: 600;
  line-height: 1.4;
}

.about-content p {
  font-size: 1.1rem;
  color: #cccccc;
  line-height: 1.7;
}

.btn-secondary-outline {
  display: inline-block;
  align-self: flex-start;
  padding: 12px 28px;
  background-color: transparent;
  color: #42b883;
  border: 2px solid #42b883;
  text-decoration: none;
  font-weight: bold;
  border-radius: 4px;
  transition: 0.3s ease;
  text-align: center;
}

.btn-secondary-outline:hover {
  background-color: #42b883;
  color: #1a1a1a;
  transform: translateY(-2px);
}

/* --- SEÇÃO TECNOLOGIAS (VARAL) --- */
.tech-section {
  width: 100%;
  padding: 100px 20px;
  background-color: #1a1a1a;
  color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.tech-header {
  text-align: center;
  margin-bottom: 60px;
}

.tech-header h1 {
  font-size: 2.5rem;
  font-weight: 700;
  color: white;
  margin-bottom: 15px;
}

.tech-header p {
  color: #cccccc;
  font-size: 1.1rem;
}

/* Container do Varal */
.tech-tree {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  width: 100%;
  max-width: 1200px;
  position: relative;
  padding-top: 20px;
  gap: 15px;
}

/* A linha horizontal do "varal" */
.tech-tree::before {
  content: '';
  position: absolute;
  top: 40px;
  left: 5%;
  width: 90%;
  height: 2px;
  background-color: #42b883;
  z-index: 1;
}

/* Cada ramificação */
.tech-branch {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex: 1;
  z-index: 2;
}

/* Título superior */
.branch-title {
  background-color: #2c3e50;
  color: #bfecff;
  padding: 10px 15px;
  border-radius: 4px;
  font-weight: bold;
  font-size: 0.95rem;
  text-align: center;
  min-height: 42px;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

/* A setinha/linha vertical */
.branch-connector {
  width: 2px;
  height: 25px;
  background-color: #42b883;
  position: relative;
}

/* Ponta da setinha para baixo */
.branch-connector::after {
  content: '▼';
  position: absolute;
  bottom: -6px;
  left: 50%;
  transform: translateX(-50%);
  color: #42b883;
  font-size: 0.6rem;
}

/* Caixa branca inferior */
.tech-box {
  background-color: #ffffff;
  color: #1a1a1a;
  padding: 20px 15px;
  border-radius: 6px;
  width: 100%;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
  min-height: 160px;
}

.tech-box ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.tech-box li {
  font-size: 0.95rem;
  font-weight: 600;
  color: #333333;
  text-align: center;
}

/* --- ÚLTIMA SEÇÃO (FOOTER / TRÊS DIVISÕES) --- */
.footer-section {
  width: 100%;
  padding: 80px 20px 40px 20px;
  background-color: #111111;
  color: white;
  border-top: 1px solid #2a2a2a;
  display: flex;
  justify-content: center;
}

.footer-container {
  display: grid;
  grid-template-columns: 1.5fr 1fr 1.2fr;
  gap: 40px;
  width: 100%;
  max-width: 1200px;
}

.footer-box {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.footer-box h2 {
  font-size: 1.8rem;
  color: white;
  font-weight: 700;
}

.footer-box h3 {
  font-size: 1.3rem;
  color: #42b883;
  font-weight: 600;
  position: relative;
  padding-bottom: 5px;
}

.footer-box p {
  font-size: 1rem;
  color: #aaaaaa;
  line-height: 1.6;
}

/* Customização da Coluna 1 */
.brand-box .copyright {
  font-size: 0.85rem;
  color: #666666;
  margin-top: auto;
}

/* Customização da Coluna 2 */
.links-box ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.links-box a {
  color: #aaaaaa;
  text-decoration: none;
  transition: 0.3s ease;
  font-size: 1rem;
}

.links-box a:hover {
  color: #42b883;
  padding-left: 5px;
}

/* Customização da Coluna 3 */
.contact-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 8px;
  color: #cccccc;
  font-size: 0.95rem;
}

.btn-footer {
  display: inline-block;
  align-self: flex-start;
  padding: 10px 20px;
  background-color: #42b883;
  color: #111111;
  text-decoration: none;
  font-weight: bold;
  border-radius: 4px;
  font-size: 0.9rem;
  transition: 0.3s ease;
  text-align: center;
  margin-top: 10px;
}

.btn-footer:hover {
  background-color: white;
  transform: translateY(-2px);
}

/* --- RESPONSIVIDADE (MOBILE) --- */
@media (max-width: 850px) {
  .footer-container {
    grid-template-columns: 1fr;
    gap: 40px;
    text-align: center;
  }

  .footer-box {
    align-items: center;
  }

  .btn-footer {
    align-self: center;
  }

  .brand-box .copyright {
    margin-top: 20px;
  }
}

@media (max-width: 968px) {
  .tech-tree::before {
    display: none;
  }

  .tech-tree {
    flex-direction: column;
    gap: 30px;
    align-items: center;
    max-width: 450px;
  }

  .tech-branch {
    width: 100%;
  }

  .branch-connector {
    height: 15px;
  }
  
  .tech-box {
    min-height: auto;
  }
}



@media (max-width: 768px) {
  .meu-header {
    flex-direction: column;
    gap: 15px;
    align-items: center;
    text-align: center;
  }

  .menu-container {
    flex-direction: row;
    flex-wrap: wrap; /* Permite que os links quebrem linha se não couberem */
    justify-content: center;
    gap: 12px;
    font-size: 0.9rem;
  }
}



@media (max-width: 968px) {
  .tech-tree::before {
    display: none;
  }

  .tech-tree {
    flex-direction: column;
    gap: 30px;
    align-items: center;
    width: 100%; /* Garante que use o espaço disponível */
    max-width: 100%;
    padding: 0 10px; /* Margem de segurança para o celular */
  }

  .tech-branch {
    width: 100%;
    max-width: 400px; /* Limita o tamanho para não ficar gigante em tablets */
  }

  .branch-connector {
    height: 15px;
  }
  
  .tech-box {
    min-height: auto;
    width: 100%;
    box-sizing: border-box; /* Garante que o padding não aumente o tamanho da caixa */
  }
}





.seletor-idioma {
  display: flex;
  align-items: center;
}

.btn-idioma {
  background: transparent;
  border: 1px solid #42b883;
  color: #42b883;
  padding: 4px 10px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  font-size: 0.8rem;
  transition: 0.3s ease;
}

.btn-idioma:hover {
  background-color: #42b883;
  color: #111111;
}


/* === ANIMAÇÃO DE FADE IN === */
@keyframes fadeInHero {
  from {
    opacity: 0;
    transform: translateY(20px); /* Dá um leve efeito de subir enquanto surge */
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>