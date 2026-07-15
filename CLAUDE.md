# CLAUDE.md — Let'z Energy Gum · Site B2C

## Projeto
Site institucional e de conversão B2C da **Let'z Energy Gum** — o primeiro chiclete energético do Brasil.

## Stack
- **HTML + CSS + JS puro** (arquivo único `index.html`, ~48KB)
- **Sem frameworks, sem build step** — edita e funciona
- **Deploy:** Vercel auto-deploy no `main` (push direto, nunca PR)
- **Repo:** `github.com/luccaLETZ/letz-site`
- **Imagens:** pasta `img/` (logo-letz.png, pacote-letz.png, verso-letz.jpg, ativacao-letz.jpg)
- **Fontes externas:** Google Fonts (Space Grotesk + Inter) — única dependência externa

## Identidade visual
| Token | Valor | Uso |
|-------|-------|-----|
| `--pink` | `#FF1493` | Cor primária, CTAs de destaque, badges |
| `--pink-soft` | `#F979E0` | Suporte, gradientes |
| `--paper` | `#F9F9F4` | Background base (off-white) |
| `--volt` | `#C1FF00` | CTAs de ação, destaques sobre fundo escuro |
| `--green` | `#3BDB8B` | Checks, badges de economia |
| `--ink` | `#141916` | Texto principal, fundo escuro |
| `--ink-soft` | `#4a514c` | Texto secundário |
| `--display` | `Space Grotesk` | Títulos, botões, badges, números |
| `--body` | `Inter` | Corpo de texto, parágrafos |

## Estrutura de seções (ordem no HTML)
00. Announcement marquee (faixa preta + volt, loop infinito)
01. Header sticky (esconde ao rolar pra baixo, volta ao subir, backdrop-filter)
02. Pills de ocasião (scroll horizontal: Pré-treino, Trabalho, Estudo, Manhãs, Kits)
03. Hero (headline + chips de benefício + CTAs + imagem do pacote com float animation)
04. Vitrine de vídeos UGC (carrossel 9:16, snap scroll, drag, setas)
05. Marquee de claims (faixa pink rotacionada -1.4deg)
06. Showcase do produto único (split: galeria com thumbnail clicável + infos e specs nutricionais)
07. Benefícios + contadores animados (75mg cafeína, 180mg taurina, 200% B12)
08. História da marca (split: imagem + texto)
09. Onde encontrar (strip de logos de parceiros — placeholder)
10. Reviews (esteira automática, pausa no hover)
11. Oferta / Kits (3 cards: Experimente / Kit Energia / Assinatura + trust badges)
12. Newsletter (bloco escuro, input + botão, cupom 10%)
13. FAQ (accordion com `<details>`)
14. Footer (accordion mobile, colunas desktop, disclaimers legais)
15. Sticky ATC mobile (barra fixa no bottom, aparece após hero, só mobile)

## Animações e interações (JS vanilla, ~30 linhas)
- **Reveal on scroll:** classe `.rv` + IntersectionObserver → adiciona `.in`
- **Contadores animados:** `[data-count]` + `[data-suffix]` → cubic ease-out 1.2s
- **Header hide/show:** compara scrollY atual vs anterior
- **Carrossel de vídeos:** pointer events pra drag + botões prev/next
- **Sticky ATC mobile:** aparece quando scrollY > hero height (só < 768px)
- **Botão topo:** aparece após 1.6× hero height

## Produto
- **Nome:** Let'z Energy Gum
- **Sabor:** Menta (único SKU atual)
- **Formato:** Goma de mascar, 12 unidades por pacote
- **Porção (3 gomas):** 75mg cafeína, 180mg taurina, vitamina B6 (115% VD), vitamina B12 (200% VD), 8 kcal, zero açúcar
- **Restrições:** Não recomendado para menores de 19 anos, gestantes, lactantes
- **Fabricante:** Florestal Alimentos S/A
- **Site:** letzgum.com.br | **Instagram:** @letz.gum
- **WhatsApp comercial:** +55 31 97591-4447

## ⚠️ PENDÊNCIAS (trocar antes de ir pra produção real)
1. **Preços** — valores atuais são placeholder (R$ 34,90 / R$ 89,90 / R$ 74,90/mês). Confirmar preços reais.
2. **Links de checkout** — todos os botões de compra estão com `href="#"`. Substituir pelos links Yampi reais.
3. **Depoimentos** — seção 10 tem reviews genéricos ("Cliente Let'z"). Trocar por avaliações reais de clientes.
4. **Logos de parceiros** — seção 09 tem placeholders "Logo parceiro". Inserir logos reais das lojas que vendem Let'z.
5. **% do cupom** — seção 12 mostra "10% OFF" como sugestão. Confirmar valor real e conectar form ao e-mail marketing / Yampi.
6. **Texto da história** — seção 08 tem versão provisória. Validar história oficial com Yann.
7. **Vídeos UGC** — seção 04 tem 5 cards placeholder. Substituir pelos vídeos reais (manter estrutura `.vcard`).
8. **Contagem de avaliações** — estrelas na seção 06 mostram "(avaliações)" como placeholder.

## Workflow de edição
1. `git pull` (ou clone se novo)
2. Editar `index.html` (tudo num arquivo só: HTML + CSS + JS)
3. Testar local: abrir `index.html` no navegador (funciona offline, exceto Google Fonts)
4. `git add . && git commit -m "descrição" && git push` → Vercel deploya automático

## Convenções
- **Commits:** direto no `main`, nunca PR
- **CSS:** custom properties em `:root`, mobile-first, breakpoints em 768px e 1024px
- **Classes de animação:** `.rv` = reveal on scroll, `.rv-d1`/`.rv-d2`/`.rv-d3` = delay stagger
- **Seções com fundo alternado:** classe `.sec-tint` aplica `background: #f1f1ea`
- **Botões:** `.btn-volt` (ação primária), `.btn-pink` (destaque), `.btn-dark` (sobre fundo claro), `.btn-ghost` (secundário)
- **Imagens:** sempre em `img/`, nomes kebab-case, sem espaços ou acentos

## Contexto da marca
- Fundador: Yann Rodrigues (conectado à comunidade BORA de corrida)
- Base: Belo Horizonte, MG
- Posicionamento: energia prática pra rotina real (treino, trabalho, estudo)
- Diferencial vs. energéticos: cabe no bolso, zero açúcar, refresca o hálito, sem preparo
- Tom de voz: direto, jovem, sem ser forçado. Fala "masca", não "consuma".
