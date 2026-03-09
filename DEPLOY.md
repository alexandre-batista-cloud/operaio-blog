# Deploy — blog.operaio.com.br no Cloudflare Pages

## Passo 1 — Criar repositório no GitHub

```bash
gh repo create operaio-blog --public --source=. --remote=origin --push
```

## Passo 2 — Conectar no Cloudflare Pages

1. Acesse: https://dash.cloudflare.com → Pages → Create application → Connect to Git
2. Selecione o repo `operaio-blog`
3. Configurações de build:
   - **Build command:** `npm run build`
   - **Build output directory:** `dist`
   - **Node version:** `20` (variável de ambiente: `NODE_VERSION=20`)
4. Clique em "Save and Deploy"

## Passo 3 — Configurar domínio customizado

1. No Cloudflare Pages → seu projeto → Custom domains
2. Adicione: `blog.operaio.com.br`
3. No DNS da Cloudflare (zona operaio.com.br), o registro CNAME é criado automaticamente:
   - Nome: `blog`
   - Destino: `operaio-blog.pages.dev`

## Passo 4 — Deploy automático

Todo push na branch `main` dispara deploy automático no Cloudflare Pages. Zero configuração extra.

## Estrutura do projeto

```
operaio-blog/
├── src/
│   ├── content/blog/     # Artigos em Markdown/MDX
│   ├── layouts/BlogPost.astro   # Layout de artigo (Kantar pattern)
│   ├── pages/
│   │   ├── index.astro   # Home com grid de artigos (Hackr pattern)
│   │   └── blog/         # Listing + rotas de artigos
│   ├── components/       # Header, Footer, HeaderLink, etc.
│   └── styles/global.css # Dark theme Operaio
├── astro.config.mjs      # site: https://blog.operaio.com.br
└── wrangler.toml         # Cloudflare Pages config
```

## Adicionar novo artigo

1. Crie `src/content/blog/seu-titulo.md`
2. Frontmatter obrigatório:
   ```yaml
   ---
   title: 'Título do Artigo'
   description: 'Descrição curta (150-160 chars para SEO)'
   pubDate: 'YYYY-MM-DD'
   heroImage: '../../assets/blog-placeholder-1.jpg'
   ---
   ```
3. Escreva o conteúdo em Markdown
4. `git add . && git commit -m "content: nome do artigo" && git push`

## Paleta de cores

| Variável      | Valor     | Uso                  |
|---------------|-----------|----------------------|
| `--bg`        | `#0f1923` | Background principal |
| `--bg-card`   | `#16232e` | Cards e componentes  |
| `--accent`    | `#f05a28` | Laranja Operaio      |
| `--text`      | `#e2e8f0` | Texto principal      |
| `--text-muted`| `#94a3b8` | Texto secundário     |
| `--border`    | `#1e2d3d` | Bordas               |
