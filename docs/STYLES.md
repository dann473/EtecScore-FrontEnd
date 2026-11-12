# EtecScore — CSS modular

Pacote inicial de estilos baseado nas seis referências visuais enviadas. O projeto pode continuar sendo desenvolvido em HTML, CSS e JavaScript puro; não há dependência de framework ou pré-processador.

## Estrutura

```text
etecscore-ui/
├── css/
│   ├── index.css                 # importe este arquivo no HTML
│   ├── tokens.css                # cores, tipografia, espaçamento e raios
│   ├── base.css                  # reset, estilos globais e acessibilidade
│   └── components/
│       ├── layout.css
│       ├── icons.css
│       ├── navigation.css
│       ├── buttons.css
│       ├── forms.css
│       ├── badges.css
│       ├── match-card.css
│       ├── highlights.css
│       ├── standings.css
│       ├── tournament-tabs.css
│       ├── bracket.css
│       └── podium.css
└── README.md
```

## Instalação

1. Copie a pasta `css/` para a raiz do seu front-end (ou ajuste os caminhos dos `@import`).
2. No `<head>` do HTML, carregue o CSS principal:

```html
<link rel="stylesheet" href="./css/index.css">
```

3. Carregue a fonte Geist no projeto. A família já está declarada nos tokens; basta disponibilizar os arquivos localmente ou adicionar a fonte ao HTML. Sem isso, o navegador usará os fallbacks do sistema.
4. Para ícones, use Lucide no HTML/JavaScript. Exemplo com Lucide via pacote ou CDN:

```html
<i data-lucide="house" class="es-icon"></i>
<i data-lucide="trophy" class="es-icon"></i>
<i data-lucide="users" class="es-icon"></i>

<!-- Depois de carregar lucide, execute: lucide.createIcons(); -->
```

Os estilos não dependem de Shadow Icons. Os ícones devem herdar `currentColor`, respeitando a cor do componente pai.

## Componentes e classes

| Referência | Componente CSS | Classes principais |
|---|---|---|
| Todas as páginas | Tokens e base | `:root`, `body`, `.es-container`, `.es-page` |
| Header | Navegação | `.es-header`, `.es-nav`, `.es-nav__link`, `.es-header__search` |
| Botões | Botões | `.es-btn`, `.es-btn--primary`, `.es-btn--secondary`, `.es-btn--icon` |
| Inputs | Formulários | `.es-field`, `.es-field--floating`, `.es-search` |
| Badges | Status | `.es-badge`, `.es-badge--completed`, `--scheduled`, `--postponed`, `--cancelled` |
| Homepage — Jogos | Partida | `.es-match-card` e elementos `__header`, `__teams`, `__score` |
| Homepage — Destaques | Jogador/equipe | `.es-spotlight-card`, `.es-spotlight-card--player`, `.es-spotlight-stats` |
| Homepage — classificação | Tabela | `.es-standings`, `.es-standings__table` |
| Mata-mata — etapas | Abas | `.es-round-tabs`, `.es-round-tabs__item` |
| Mata-mata — chave | Confrontos | `.es-bracket-layout`, `.es-bracket`, `.es-bracket-match` |
| Mata-mata — resultado | Pódio/ranking | `.es-ranking-card`, `.es-podium`, `.es-ranking-table` |

## Exemplo de marcação

### Header

```html
<header class="es-header es-container">
  <a class="es-header__brand" href="#">EtecScore</a>
  <nav class="es-nav" aria-label="Navegação principal">
    <a class="es-nav__link" href="#central" aria-current="page">
      <i data-lucide="house" class="es-icon"></i> Central
    </a>
    <span class="es-nav__separator" aria-hidden="true"></span>
    <a class="es-nav__link" href="#mata-mata">
      <i data-lucide="trophy" class="es-icon"></i> Mata-mata
    </a>
    <span class="es-nav__separator" aria-hidden="true"></span>
    <a class="es-nav__link" href="#equipes">
      <i data-lucide="users" class="es-icon"></i> Equipes
    </a>
  </nav>
  <div class="es-header__search">
    <label class="es-search">
      <i data-lucide="search" class="es-search__icon"></i>
      <input class="es-search__input" type="search" placeholder="Pesquisar">
      <span class="es-search__shortcut">⌘ + K</span>
    </label>
  </div>
</header>
```

### Botão, campo e badge

```html
<button class="es-btn es-btn--primary" type="button">
  <i data-lucide="tag" class="es-btn__icon"></i> Primary
</button>
<button class="es-btn es-btn--secondary" type="button">Secondary</button>

<div class="es-field es-field--floating">
  <label class="es-field__label" for="team-name">Equipe</label>
  <input class="es-field__input" id="team-name" type="text">
</div>

<span class="es-badge es-badge--completed">Finalizada</span>
<span class="es-badge es-badge--scheduled">Agendada</span>
<span class="es-badge es-badge--postponed">Adiada</span>
<span class="es-badge es-badge--cancelled">Cancelada</span>
```

### Card de partida

```html
<article class="es-match-card">
  <header class="es-match-card__header">
    <span class="es-match-card__sport">Futsal</span>
    <span class="es-badge es-badge--completed">Finalizada</span>
  </header>
  <div class="es-match-card__teams">
    <div class="es-match-card__team">
      <span class="es-match-card__team-name">Equipe A</span>
      <strong class="es-match-card__score">3</strong>
    </div>
    <div class="es-match-card__team">
      <span class="es-match-card__team-name">Equipe B</span>
      <strong class="es-match-card__score">2</strong>
    </div>
  </div>
</article>
```

## Observações de implementação

- As cores principais foram conferidas diretamente nos pixels da prancha: `#08131F` (fundo), `#E8EBF0` (texto claro) e `#80A2DA` (azul de destaque).
- As cores de status foram extraídas da prancha de badges. Os gradientes de vencedor, ouro, prata e bronze foram aproximados a partir da tela do mata-mata.
- A referência mostra componentes em desktop. Os estilos incluem breakpoints iniciais para cards, navegação e chave; valide os tamanhos com o conteúdo real e com os pontos de quebra definidos pelo projeto.
- Os conectores da chave eliminatória são elementos separados (`.es-bracket__connector--horizontal`, `--vertical` e `--elbow`). O posicionamento de cada ligação deve ser calculado/definido no HTML ou pelo JavaScript conforme a quantidade de equipes e rodadas.
- Os estilos não implementam comportamento: navegação, busca por `⌘ + K`, carrossel de destaques, seleção de abas e geração da chave continuam sendo responsabilidade do JavaScript.
- As imagens de atleta e escudo devem ser inseridas como `<img>` usando `.es-spotlight-card__portrait` e `.es-spotlight-card__team-logo`.
