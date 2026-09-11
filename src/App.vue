<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'
import { gsap } from 'gsap'
import { projects } from './projects'

const activeSection = ref('inicio')
let observer: IntersectionObserver | undefined
let animation: gsap.Context | undefined

onMounted(() => {
  observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) activeSection.value = entry.target.id
    })
  }, { rootMargin: '-15% 0px -55% 0px', threshold: 0 })
  document.querySelectorAll('main > section[id]').forEach((section) => observer?.observe(section))
  if (!window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    animation = gsap.context(() => {
      gsap.from('.hero-reveal', { opacity: 0, y: 20, duration: 0.7, stagger: 0.09, ease: 'power3.out', clearProps: 'all' })
    })
  }
})

onUnmounted(() => {
  observer?.disconnect()
  animation?.revert()
})
</script>

<template>
  <a class="skip-link" href="#projetos">Pular para os projetos</a>
  <header class="header">
    <div class="header-inner container">
      <a class="brand" href="#inicio" aria-label="Gustavo Vilela, início">
        <span class="brand-mark" aria-hidden="true">gv</span>
        <span>Gustavo Vilela</span>
      </a>
      <nav class="navigation" aria-label="Navegação principal">
        <a href="#projetos" :class="{ active: activeSection === 'projetos' }" :aria-current="activeSection === 'projetos' ? 'location' : undefined">Projetos</a>
        <a href="#uso-de-ia" :class="{ active: activeSection === 'uso-de-ia' }" :aria-current="activeSection === 'uso-de-ia' ? 'location' : undefined">Uso de IA</a>
      </nav>
      <a class="github-top" href="https://github.com/GustavoFVilela" target="_blank" rel="noopener noreferrer">
        GitHub <span aria-hidden="true">↗</span>
      </a>
    </div>
  </header>

  <main>
    <section id="inicio" class="hero container" aria-labelledby="page-title">
      <div class="hero-topline hero-reveal">
        <span class="eyebrow">Ciência da Computação</span>
        <span class="edition">2026</span>
      </div>
      <h1 id="page-title" class="hero-reveal">Portfólio de<br><span>projetos<span class="title-period">.</span></span></h1>
      <div class="hero-bottom hero-reveal">
        <div class="identity">
          <p class="full-name">Gustavo Finder Vilela de Farias</p>
          <p class="student">19 anos <span aria-hidden="true">/</span> Segundo período</p>
        </div>
        <a class="explore" href="#projetos">Conheça os projetos <span class="arrow-circle" aria-hidden="true">↓</span></a>
      </div>
    </section>

    <section id="projetos" class="projects-section container" aria-labelledby="projects-title">
      <div class="section-heading">
        <div>
          <p class="eyebrow section-kicker">01 / Projetos</p>
          <h2 id="projects-title">O que tenho feito</h2>
        </div>
        <p class="section-aside">Na faculdade e por iniciativa própria.</p>
      </div>

      <div class="projects-grid">
        <article v-for="project in projects" :key="project.id" class="project-card" :id="project.id" :aria-labelledby="`${project.id}-title`">
          <div class="project-visual" :class="`visual-${project.id}`">
            <template v-if="project.id === 'alfabeto'">
              <img class="alphabet-image" src="/projects/alfabeto-monstruoso.png" width="740" height="740" alt="Letras coloridas em forma de monstros usadas no Alfabeto Monstruoso" loading="lazy">
              <span class="visual-caption">Imagem utilizada no projeto</span>
            </template>
            <template v-else-if="project.id === 'banco'">
              <div class="terminal-example" aria-label="Exemplo de operações no sistema bancário">
                <div class="terminal-top"><span class="terminal-glyph" aria-hidden="true">&gt;_</span><span>sistema_bancario.py</span></div>
                <div class="terminal-lines"><span class="terminal-muted"># Exemplo de operações</span><span>Depósito <b>+ R$ 200,00</b></span><span>Saque <b>- R$ 50,00</b></span><span class="terminal-result">Saldo <b>R$ 150,00</b></span></div>
              </div>
              <span class="visual-caption">Demonstração com dados fictícios</span>
            </template>
            <template v-else>
              <div class="commit-overview" aria-label="Estrutura atual do Commit: navegação entre Commit, Datas e Calendário">
                <div class="commit-wordmark">Commit<span aria-hidden="true">_</span></div>
                <span class="commit-caption">Organização para a minha rotina.</span>
                <div class="commit-tabs"><span class="selected">Commit</span><span>Datas</span><span>Calendário</span></div>
              </div>
              <span class="visual-caption">Estrutura das abas do protótipo</span>
            </template>
          </div>

          <div class="project-body">
            <div class="project-meta"><span>{{ project.kind }}</span><span>{{ project.number }}</span></div>
            <h3 :id="`${project.id}-title`">{{ project.title }}</h3>
            <p class="project-context">{{ project.category }}<br>{{ project.date }}</p>
            <p class="project-description">{{ project.description }}</p>
            <h4>Minha participação</h4>
            <p>{{ project.contribution }}</p>
            <p class="project-process">{{ project.process }}</p>
            <ul class="tags" aria-label="Tecnologias e temas"><li v-for="tag in project.tags" :key="tag">{{ tag }}</li></ul>
            <div class="project-ending">
              <span class="project-status" :class="{ 'status-highlight': project.id === 'banco' }">{{ project.status }}</span>
              <a :href="project.repo" target="_blank" rel="noopener noreferrer" :aria-label="`Ver código de ${project.title} no GitHub`">Ver código <span aria-hidden="true">↗</span></a>
            </div>
          </div>
        </article>
      </div>
      <p class="repository-note">Os links dos trabalhos da faculdade levam às pastas dos projetos em um repositório compartilhado. A participação descrita aqui se refere a esses trabalhos.</p>
    </section>

    <section id="uso-de-ia" class="ai-section container" aria-labelledby="ai-title">
      <div class="section-heading ai-heading">
        <div><p class="eyebrow section-kicker">02 / Transparência</p><h2 id="ai-title">Como usei IA</h2></div>
      </div>
      <div class="ai-layout">
        <div class="site-ai">
          <h3>Neste portfólio</h3>
          <p>Usei o <strong>Codex, da OpenAI</strong>, como apoio para estruturar o site, adaptar o visual, organizar os textos e preparar o projeto para publicação na Vercel.</p>
          <p>As descrições partem das minhas experiências e dos projetos que desenvolvi ou dos quais participei.</p>
        </div>
        <dl class="project-ai-list">
          <div v-for="project in projects" :key="project.id"><dt>{{ project.title }}</dt><dd>{{ project.ai }}</dd></div>
        </dl>
      </div>
    </section>
  </main>

  <footer class="footer container"><span>© 2026 Gustavo Vilela</span><span>Portfólio de projetos</span><a href="#inicio">Voltar ao início <span aria-hidden="true">↑</span></a></footer>
</template>
