# Portfólio de Gustavo Vilela

Site de portfólio de projetos para apresentar a trajetória de Gustavo Finder Vilela de Farias, estudante do segundo período de Ciência da Computação.

## Projetos apresentados

- Alfabeto Monstruoso: trabalho de Experiência Criativa, com IA restrita à melhoria estética final.
- Sistema bancário: trabalho em grupo de Lógica de Programação, sem IA, avaliado com nota máxima.
- Commit: aplicativo pessoal de organização em desenvolvimento, com Cursor e Grok 4.6 como apoio ao aprendizado.

Os textos estão em `src/projects.ts`. O visual está em `src/style.css`; a composição da página está em `src/App.vue`.

## Executar localmente

Use uma versão de Node.js compatível com o campo `engines` do projeto e pnpm.

```sh
pnpm install --frozen-lockfile
pnpm dev
```

## Gerar a versão de publicação

```sh
pnpm build
pnpm preview
```

## Vercel

O projeto está preparado para importar o repositório `GustavoFVilela/portifolio` na Vercel com Vite. A saída de publicação é a pasta `dist`. Não há variáveis de ambiente, autenticação, formulários ou banco de dados.

O código está preparado para publicação na Vercel. Enviar os arquivos ao GitHub não publica automaticamente o site: é necessário conectar o repositório à Vercel e concluir a implantação.

## Uso de IA

O Codex, da OpenAI, auxiliou na estruturação do site, adaptação do visual, organização dos textos e preparação para publicação na Vercel. A seção “Como usei IA” distingue esse apoio do uso de IA em cada projeto.

## Créditos

Base técnica e referência visual: [portfólio de João Zupeli](https://github.com/joaozupeli/portfolio), disponibilizado sob licença MIT. O arquivo `LICENSE.reference` preserva os termos da referência. O código e os textos foram adaptados para os projetos e a identidade de Gustavo.

A imagem do Alfabeto Monstruoso foi obtida dos arquivos do próprio trabalho acadêmico. Sua presença no site não atribui a autoria original da ilustração a Gustavo.
