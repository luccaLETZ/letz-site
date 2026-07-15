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
10.1. Quiz — entrada rápida (nova, entre reviews e oferta): pergunta "Qual é seu principal
      momento de baixa energia?" + 4 opções + selo "60 segundos" → abre o overlay do quiz
      com a pergunta 2 já respondida, direto pra pergunta 3
11. Oferta / Kits (3 cards: Experimente / Kit Energia / Assinatura + trust badges;
    `data-plan="experimente|kit|assinatura"` em cada `.kcard` pro destaque do resultado do quiz)
12. Newsletter (bloco escuro, input + botão, cupom 10%)
13. FAQ (accordion com `<details>`)
14. Footer (accordion mobile, colunas desktop, disclaimers legais)
15. Sticky ATC mobile (barra fixa no bottom, aparece após hero, só mobile)

## Overlays (fora do fluxo linear de scroll)
- **Popup de saída** (`#exitBackdrop`/`#exitModal`): modal 1x por visitante
  (localStorage `letz_exit_intent_shown`), dispara após 8s na página por mouseleave no topo
  (desktop), scroll 40%+ com retorno rápido de 120px+ entre dois eventos consecutivos, ou 35s
  de inatividade (sem scroll/touch). Foco preso, ESC/backdrop fecham, foco retorna ao elemento
  anterior, scroll do body travado enquanto aberto. Form "continuar depois" exige e-mail +
  checkbox LGPD.
- **Quiz** (`#quizOv`): overlay fullscreen, 7 perguntas (nome, momento, energia, frequência,
  cafeína, benefício, forma de compra) → captura de lead (nome opcional, e-mail + checkbox LGPD
  obrigatórios) → resultado com plano recomendado (`recommendPlan()`) e destaque visual do
  `.kcard[data-plan]` correspondente na seção 11. Estado em localStorage `letz_quiz` (retoma de
  onde parou). Deep-link via `#quiz`. Mesma trava de foco/scroll do popup de saída.

## Animações e interações (JS vanilla)
- **Reveal on scroll:** classe `.rv` + IntersectionObserver → adiciona `.in`
- **Contadores animados:** `[data-count]` + `[data-suffix]` → cubic ease-out 1.2s
- **Header hide/show:** compara scrollY atual vs anterior
- **Carrossel de vídeos:** pointer events pra drag + botões prev/next
- **Sticky ATC mobile:** aparece quando scrollY > hero height (só < 768px)
- **Botão topo:** aparece após 1.6× hero height
- **Popup de saída + Quiz:** ver seção "Overlays" acima
- **Tracking:** `trackEvent(nome,dados)` — só console.log por enquanto (TODO Meta Pixel).
  NUNCA passar PII (e-mail/WhatsApp/nome) pro trackEvent — só pro `enviarLead()`
- **Lead:** `enviarLead(dados)` — POST pra `LEAD_WEBHOOK_URL` (hoje vazia, só loga no console)

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
9. **Webhook do lead (quiz + popup de saída + newsletter)** — `LEAD_WEBHOOK_URL` no `<script>`
   está vazio. Preencher com a URL do webhook n8n pra receber os leads de verdade.
10. **Meta Pixel** — `trackEvent()` só faz console.log. Plugar o pixel e mapear `quiz_complete`
    pro evento `Lead` (comentário TODO já deixado em `trackEvent`, com aviso explícito de nunca
    passar PII nesse evento).
11. **Link Yampi no resultado do quiz** — o CTA "Quero esse plano" hoje só fecha o overlay e
    destaca o card na seção 11 (os hrefs ainda são `#`). Quando os links reais existirem, ligar
    direto no checkout do plano recomendado (comentário TODO já deixado em `renderResult`).

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
