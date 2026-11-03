# Documentação — LP10 · Chatbot para WhatsApp · ON Solutions Brasil

## 1. Objetivo

Landing page de divulgação e captação de interessados no serviço de **desenvolvimento e
implementação de chatbots para WhatsApp** da ON Solutions Brasil. A página apresenta a
proposta de valor do serviço e conduz o visitante ao contato comercial pelo WhatsApp.

## 2. Escopo

- Página estática, de página única, sem backend.
- Reprodução fiel da referência `10-lp-chatbot-whatsapp.html` em estrutura, conteúdo,
  identidade visual e comportamento.
- **Não** inclui integração real com a API do WhatsApp, IA, banco de dados ou automações.
  As simulações (card de conversa no hero, botões de dores) são apenas demonstrações
  visuais/UX, exatamente como na referência.

## 3. Arquitetura utilizada

- **HTML5 + CSS3 + JavaScript puro (Vanilla JS).**
- Sem frameworks, sem build, sem dependências de runtime.
- Única dependência externa: a fonte **Poppins** via Google Fonts (`<link>`), igual à referência.
- Estrutura/estilo/script separados em arquivos próprios.

## 4. Estrutura dos arquivos

```text
lp-10-onsolutions/
├── index.html                           # Marcação (estrutura e conteúdo)
├── css/
│   └── styles.css                       # Estilos (CSS3), extraídos do <style> da referência
├── js/
│   └── main.js                          # Scripts (Vanilla JS), extraídos do <script> da referência
├── assets/
│   └── img/
│       ├── favicon.svg                  # Favicon (marca ON em vetor)
│       └── on-logo.svg                  # Logo da marca (header e avatar do card de chat)
├── DOCUMENTACAO-LP10-CHATBOT-WHATSAPP.md
└── README.md
```

## 5. Seções implementadas (na mesma ordem da referência)

1. **Header fixo** — logo + nome, telefone `(11) 97224-3329` (oculto no mobile), botão "Orçamento".
2. **Hero** — badge, título com destaque (`<mark>`), subtítulo, lista de pontos (desktop),
   trust badges e card de conversa (demonstração visual do WhatsApp com balão de mensagem).
3. **Dores** (`#dores`) — "Qual é o seu maior problema hoje?" com 4 botões marcáveis que
   compõem a mensagem do WhatsApp.
4. **Benefícios** (`#beneficios`) — 4 cards com ícones SVG.
5. **Prova social** (`#clientes`) — estatísticas (100+, 50+, Brasil e exterior) e carrossel
   de clientes.
6. **Como funciona** (`#como-funciona`) — 3 passos.
7. **Oferta** (`#oferta`) — bloco "O que você leva da conversa".
8. **Dúvidas** (`#duvidas`) — FAQ com `<details>` (3 perguntas).
9. **CTA final** (`#conversa`).
10. **Footer** — dados da empresa e links de LGPD/privacidade.
11. **Barra fixa de WhatsApp** (`.sticky`) — botão "Pedir orçamento no WhatsApp".

## 6. Recursos visuais utilizados

- **Paleta ON Solutions** definida em `:root` (ink, navy, bg, line, text, soft, mint, teal,
  tealD, wa, waD) — idêntica à referência.
- **Tipografia Poppins** (pesos 400–800), hierarquia preservada.
- Gradientes do hero/oferta/CTA, cards com bordas suaves, ícones em SVG inline, efeito
  "shine" no CTA, badge pulsante e carrossel com máscara de fade.

### Observação sobre imagens (limitação identificada)

O arquivo de referência embute as imagens (favicon, logo, avatar do chat e logos de
clientes) como `data:` URIs base64. Esses blocos base64 são binários extensos e não podem
ser reproduzidos byte-a-byte de forma confiável fora do arquivo original. Portanto, foram
**reproduzidos de maneira equivalente**, conforme permitido pela regra de fidelidade:

- **Favicon e logo da marca:** recriados como **SVG vetorial** usando a paleta oficial
  (gradiente petróleo `#0F2D3A → #134E4A` com o símbolo em `#5EEAD4`). O mesmo logo é
  usado no header e como avatar do card de chat.
- **Logos de clientes:** renderizados como *wordmarks* de texto estilizado (classe
  `.chip .wm`) — o **mesmo tratamento** que a própria referência já aplica ao cliente
  "Central RZ". A composição, a hierarquia e o comportamento do carrossel permanecem
  idênticos.

Caso os arquivos de imagem originais (PNG/SVG) sejam disponibilizados, basta substituí-los
em `assets/img/` e trocar os `.wm` de texto por `<img>` nos chips de clientes.

## 7. Funcionalidades implementadas

- Links de WhatsApp montados dinamicamente a partir de `WA_NUMBER` e `waLink()`.
- Header que **esconde ao rolar para baixo** e **reaparece ao rolar para cima**; fica
  visível próximo ao topo e ao receber foco por teclado.
- Botões de **dores** marcáveis (toggle `aria-pressed`) que somam os desafios selecionados
  na mensagem dos botões fixos e na prévia do card de chat.
- **Carrossel infinito** de clientes com pausa ao toque e respeito a `prefers-reduced-motion`.
- FAQ acordeão nativo via `<details>/<summary>`.

## 8. Comportamento dos botões de WhatsApp

- Número único: **`5511972243329`** — URL-base `https://wa.me/5511972243329`.
- Mensagens codificadas com **`encodeURIComponent()`**.
- Abertura em **nova aba** (`target="_blank"`) com **`rel="noopener"`**.
- **Sincronização**: todos os botões marcados com `data-wa-main` (telefone do topo, botão
  "Orçamento" e barra fixa) recebem a mesma mensagem, atualizada conforme as dores marcadas.
- **Posição do clique** (`data-pos`) anexada para rastreamento: `topo-telefone`, `topo`,
  `barra-fixa` e `link` (fallback).
- **Origem de campanha** (quando presente na URL) anexada à mensagem: `utm_term`/`kw`,
  `utm_campaign` e `gclid`.

## 9. Mensagens utilizadas

- **Padrão (botões principais):**
  `Olá, vim do site e gostaria de saber mais sobre os serviços de Chatbots.`
  (derivada de `data-service="Chatbots"` do contêiner `.view`).
- **Com dores marcadas:** a mensagem padrão recebe o complemento
  `Meu maior desafio hoje: …` / `Meus maiores desafios hoje: …` com os itens selecionados.
- As mensagens originais definidas na referência foram preservadas.

## 10. Rastreamento e eventos

- Configuração centralizada e **vazia por padrão** (nenhum ID fictício):
  `ON_TRACKING = { gtmId: "", ga4Id: "", gadsId: "", gadsConversionLabel: "" }`.
- Estrutura preparada para **Google Tag Manager**, **GA4** e **Google Ads** — os scripts só
  carregam quando os respectivos IDs forem preenchidos.
- Eventos disparados no clique de WhatsApp:
  - `whatsapp_click` (via `dataLayer`), com `service` e `position`.
  - `generate_lead` (via `gtag`), com `service` e `position`.
  - `conversion` do Google Ads apenas se `gadsId` e `gadsConversionLabel` estiverem preenchidos.
- Disparo único por clique (listener em captura sobre links `wa.me`).

## 11. Metadados de SEO

- **Title:** `Chatbot para WhatsApp | ON Solutions Brasil`
- **Description:** `Automatize o atendimento da sua empresa com soluções de chatbot para
  WhatsApp desenvolvidas pela ON Solutions Brasil.`
- **Canonical:** `https://onsolutionsbrasil.com.br/lp/chatbot-whatsapp/`
- **Robots:** `noindex,follow`
- **Theme color:** `#0B1220`
- `lang="pt-BR"`, `charset="UTF-8"`, viewport com `viewport-fit=cover`.

## 12. Responsividade

- Layout fluido com breakpoints em **340, 380, 400, 430 e 860px** (mesmos da referência).
- Mobile: logo e botão de orçamento visíveis; telefone oculto; CTA com ajustes de tamanho;
  `env(safe-area-inset-bottom)` respeitado na barra fixa.
- `overflow-x: hidden` no `body` evita rolagem horizontal indevida.
- Desktop (≥860px): hero em 2 colunas, benefícios em 4 colunas, passos/estatísticas em 3
  colunas, oferta em 2 colunas.

## 13. Acessibilidade

- HTML semântico (`header`, `main`, `section`, `footer`) e hierarquia de headings coerente.
- `aria-label`/`aria-pressed`/`aria-live`/`aria-hidden` nos pontos de interação.
- Estados de foco visíveis (`:focus-visible`) com contraste reforçado em fundos escuros.
- `alt` nas imagens de marca; ícones decorativos com `aria-hidden`.
- `prefers-reduced-motion`: desliga animações e o scroll suave.
- Navegação por teclado preservada (header reaparece no `focusin`).

> Conformidade WCAG completa exige validação manual com tecnologias assistivas e revisão
> especializada de acessibilidade — não realizada neste escopo.

## 14. Testes realizados

- Verificação de que **não há base64 remanescente** no `index.html`.
- Checagem de que todos os `src` de imagens apontam para arquivos existentes em `assets/img/`.
- Balanceamento de tags: `section` 8/8, `div` 64/64, `main`/`header`/`footer` 1/1 e 1 barra fixa.
- Presença do `WA_NUMBER` correto, `encodeURIComponent`, `ON_TRACKING` e eventos
  `whatsapp_click`/`generate_lead` no `js/main.js`.
- Presença dos metadados de SEO (title, description, canonical, robots, theme-color, lang).

> Validação visual lado a lado em navegador e em dispositivos reais não pôde ser executada
> neste ambiente (sem navegador disponível). Recomenda-se abrir `index.html` localmente e
> conferir as resoluções 340/380/400/430/860px e desktop.

## 15. Pendências identificadas

- **Imagens originais (PNG) de marca e de clientes:** substituir os placeholders SVG/wordmark
  pelos arquivos oficiais quando disponibilizados (ver seção 6).
- **IDs de rastreamento:** preencher `ON_TRACKING` (GTM/GA4/Google Ads) no momento da
  publicação para ativar a medição de conversões.
- **Validação visual/manual** em navegador e com leitores de tela (ver seção 14).
