# Portfólio — Raul Guilherme

Página única com CSS e JS embutidos no `index.html`. Sem framework, sem build, sem `node_modules`. Abre direto no navegador com dois cliques.

Duas dependências externas, ambas opcionais para a página funcionar: as fontes do Google Fonts (sem internet cai para a fonte do sistema) e um arquivo de imagem, o avatar.

**Arquivos:**

| arquivo | o que é |
|---|---|
| `index.html` | o site inteiro: HTML, CSS e JS |
| `assets/avatar.png` | o avatar do hero. **Precisa ir junto para o GitHub Pages** |
| `README.md` | este arquivo: o que falta e como publicar |
| `MELHORIAS.md` | dicas detalhadas de como escolher os números, os projetos e o que melhorar |
| `PALETAS.md` | cinco paletas prontas para colar e testar, com contraste já verificado |
| `DADOS.md` | o formulário que você preencheu. Pode apagar quando quiser |

O caminho `assets/avatar.png` no HTML é relativo. Se você mover a imagem de pasta, o hero fica com o texto alternativo no lugar do desenho.

**Seções da página:** hero · 01 sobre · 02 projetos · 03 segurança e redes · 04 stack · 05 trajetória · 06 contato.

---

## 1. O que ainda falta preencher

**Procure por `FALTA:` no `index.html`** — são 5 marcas, cada uma com a instrução no lugar.

### a) O número de chamados resolvidos (seção 01)

Três dos quatro números já são reais e verificáveis: saem da sua trajetória e da sua stack. Só falta o primeiro.

```html
<b data-num="[N]">[N]</b>
<span>chamados resolvidos em 2025</span>
```

Troque nos **dois lugares**: `data-num` é o alvo da contagem animada, e o texto dentro do `<b>` é o que aparece se o JavaScript estiver desligado. Se o número for 470, escreva `data-num="400"` e `+400` — arredonde sempre para baixo, é o que você consegue defender numa entrevista.

Há também `data-prefixo` e `data-sufixo` para o `+` e o `º`, que a contagem preserva.

**Como escolher: `MELHORIAS.md`, seção 1.**

### b) Os três cartões de projeto (seção 02)

Hoje são três cartões **reservados** — borda tracejada, "reservado para a API". É proposital: vazio assumido comunica melhor que `[NOME_DO_PROJETO_1]` no ar.

Para publicar um projeto, troque um `<article class="projeto reservado">` inteiro pelo template que está comentado logo acima dele no HTML. O template já tem a estrutura certa: tag, título, descrição do problema, chips de stack e link do repositório.

Para criar uma categoria nova (ex: `dados`):

1. Adicione o botão dentro de `<div class="filtros">`:
   ```html
   <button class="filtro" type="button" data-filtro="dados" aria-pressed="false">dados</button>
   ```
2. No cartão, use a mesma string em dois lugares: `data-tag="dados"` no `<article>` e o texto do `<p class="tag">`.

As strings precisam bater exatamente — o JS compara texto puro. Se um filtro ficar sem nenhum projeto, apague o botão.

**Como escolher e descrever os projetos: `MELHORIAS.md`, seção 2.**

### c) O ID do Formspree

Procure por `SEU_ID_AQUI`. Instruções na seção 2 abaixo.

### d) O currículo em PDF (quando tiver)

O bloco está comentado no HTML, na lista de contato da seção 06. Quando tiver o link do Drive, descomente e troque `URL_DO_CURRICULO_PDF`.

### e) Ferramentas de segurança (opcional, seção 03)

A lista `<ul class="conceitos">` tem os conceitos que já estão na sua stack. Quando começar a usar Wireshark, Nmap ou tcpdump **de verdade**, adicione ali. Item que você não sabe defender numa entrevista custa mais caro do que a linha a mais vale.

---

## 2. Configurar o formulário (Formspree)

Sem isso o formulário não envia nada.

1. Crie uma conta grátis em <https://formspree.io>
2. **New Form** → escolha o e-mail que vai receber as mensagens
3. Ele mostra um endpoint no formato `https://formspree.io/f/xayzbwqd`. Copie a parte final — o ID (`xayzbwqd`)
4. No `index.html`, procure por `SEU_ID_AQUI` e troque:
   ```html
   <form class="revelar" action="https://formspree.io/f/xayzbwqd" method="POST">
   ```
5. Envie uma mensagem de teste. No primeiro envio o Formspree pede confirmação por e-mail.

O plano grátis aceita **50 envios por mês**. O campo `_gotcha` já está no formulário: é uma armadilha invisível que o Formspree usa para descartar robôs — não mexa nele.

---

## 3. Publicar no GitHub Pages

Repositório: `Guitts8/Guitts8.github.io`. Como o nome bate exatamente com o usuário, o site cai no endereço raiz **`https://guitts8.github.io`**, sem sufixo — é esse o link para colar no currículo e no LinkedIn.

O arquivo precisa se chamar `index.html` e estar na raiz do repositório.

1. No terminal, dentro desta pasta:

   ```bash
   git add index.html assets/ README.md MELHORIAS.md
   git commit -m "portfólio"
   git push -u origin main
   ```

   Se não quiser publicar as anotações junto, suba só `index.html` e `assets/` — sem a pasta `assets` o avatar não aparece no site publicado.

2. No GitHub: **Settings** → **Pages** → em *Source* escolha **Deploy from a branch** → branch `main`, pasta `/ (root)` → **Save**.

3. Espere um ou dois minutos e recarregue a página de Settings — o link aparece no topo.

Cada `git push` novo republica o site sozinho. A propagação leva até um minuto.

---

## 4. Notas técnicas

### Cores

Só existem **8 cores nomeadas por tema**, todas no bloco `:root` do topo do CSS. Não há nenhum hexadecimal no resto do arquivo — hovers, brilhos e transparências saem de `color-mix()` sobre os tokens. Para trocar a identidade visual inteira, mexa só nesses 16 valores (8 do escuro + 8 do claro).

| token | para que serve |
|---|---|
| `--bg` | fundo da página |
| `--bg-alt` | faixa das seções alternadas (`.faixa`) |
| `--surface` | cartão, campo de formulário, chip |
| `--line` | divisória e borda de cartão |
| `--text` | texto principal |
| `--muted` | texto secundário e borda de campo |
| `--accent` | destaque, links, barras, botão cheio |
| `--accent-2` | **só forma decorativa.** Nunca carrega texto |

### Contraste

Verificado com a fórmula de luminância relativa da WCAG, lida direto dos tokens do arquivo — não estimado. Todos os pares de texto passam AA (mínimo 4.5:1):

| par | escuro | claro |
|---|---|---|
| texto / fundo | 17.14:1 | 17.44:1 |
| texto / faixa | 16.48:1 | 15.90:1 |
| texto / cartão | 15.44:1 | 19.08:1 |
| apagado / fundo | 6.91:1 | 6.43:1 |
| apagado / faixa | 6.65:1 | 5.86:1 |
| apagado / cartão | 6.23:1 | 7.03:1 |
| acento / fundo | 11.70:1 | 6.49:1 |
| acento / cartão | 10.54:1 | 7.10:1 |
| fundo sobre acento (botão cheio) | 11.70:1 | 6.49:1 |

Se você trocar as cores, **refaça a conta** antes de publicar: <https://webaim.org/resources/contrastchecker/>.

O acento do tema claro (`#0A5E86`) é bem mais escuro que o do escuro (`#4FD6FF`) de propósito: o ciano claro dá 1.5:1 sobre fundo branco, seria ilegível.

`--accent-2` não aparece na tabela porque nunca carrega texto — é só a elipse e o brilho do hero.

### Tipografia

Três famílias, uma função cada:

- **Archivo Black** (`--f-display`) — só títulos, sempre em caixa alta. É o que dá o peso da página
- **Space Grotesk** (`--f-sans`) — parágrafos de leitura corrida (o "sobre", a trajetória)
- **JetBrains Mono** (`--f-mono`) — todo o resto: rótulo, botão, chip, terminal, formulário, rodapé

### Elementos gráficos

Fora o avatar, todos são CSS ou SVG inline.

**Avatar (hero).** `assets/avatar.png`, 880×880 com fundo transparente. O original tinha 1254px e 592 KB; foi reduzido para 880px (o dobro do tamanho em que aparece, o suficiente para tela retina) e 371 KB. Se quiser cortar mais, passe por <https://tinypng.com> ou converta para WebP — é de longe o arquivo mais pesado da página.

O `width` e o `height` no HTML batem com o arquivo para o navegador reservar o espaço antes de baixar, senão a página pula quando a imagem chega.

O personagem é quase todo preto e o fundo do site também. Duas coisas fazem ele aparecer: o disco grande no acento, posicionado atrás do tronco de propósito, e três `drop-shadow` empilhados no CSS. `drop-shadow` segue o recorte transparente do PNG, não a caixa da imagem — é por isso que ele funciona como contorno aqui e um `box-shadow` não funcionaria. No tema claro esse contorno some: o preto já se destaca sozinho sobre fundo claro.

**Terminal (seção "sobre").** Fica ao lado do texto do "sobre", embaixo dos quatro números — é onde `whoami` faz sentido. O conteúdo é texto de verdade, não imagem: leitor de tela lê e busca indexa. As linhas entram em cascata (150ms entre cada) quando o bloco chega na tela; sem JavaScript nascem todas visíveis, porque a opacidade zero só existe dentro de `.js`.

**Formas.** Seis elementos em `.formas`, cada um com sua própria animação de flutuação (9s a 19s). Os tempos são propositalmente primos entre si para nunca sincronizarem — se sincronizassem, a composição inteira pulsaria junto e ficaria mecânica.

**Poeira.** Um SVG com 24 círculos em três grupos, cada grupo cintilando com atraso diferente.

**Trama e brilho.** Duas camadas `position: fixed` com `z-index` negativo. A trama é uma grade de pontos feita com `radial-gradient` repetido, mascarada por um gradiente para sumir na direção do rodapé. O brilho são dois `radial-gradient` grandes atrás do hero.

**Faixas alternadas.** As seções com a classe `.faixa` usam `--bg-alt` e ganham uma linha degradê no topo e na base, para a página não ser um bloco só de preto.

### Comportamento

**Temas.** O atributo `data-theme` fica no `<html>`. Um script no `<head>` aplica o tema salvo *antes* da primeira renderização, para não piscar ao carregar. Na primeira visita segue a preferência do sistema operacional. Todo acesso ao `localStorage` está dentro de `try/catch` — em aba anônima ou com cookies bloqueados a troca continua funcionando, só não sobrevive ao reload.

**Filtro.** Um `addEventListener` só, no container dos botões (delegação de evento). O estado ativo é `aria-pressed`, não uma classe — o CSS estiliza por `[aria-pressed="true"]` e o leitor de tela anuncia sozinho. Os cartões escondidos usam o atributo `hidden`, que tira o elemento do fluxo **e** da ordem de tabulação, então o link de um cartão filtrado não fica capturando o Tab.

**Rolagem.** Um `addEventListener` de scroll só, `passive`, com o trabalho dentro de um `requestAnimationFrame` que não empilha. Ele cuida de três coisas ao mesmo tempo: a barra de progresso, a borda que aparece na nav e o link da seção atual (`aria-current`).

**Revelação e contagem.** `IntersectionObserver`, sem listener de scroll. Cada elemento é revelado uma vez e sai da observação. Os números contam de zero ao chegar na tela; se `data-num` não for numérico — como o `[N]` que ainda falta — a contagem não roda e o texto fica intacto.

**Stack agrupada.** São 20 itens com nível. Em lista corrida viravam uma parede de barras, então estão divididos em grupos, cada um ordenado do maior nível para o menor. Para mover um item, é só recortar o `<div class="nivel">` inteiro.

**Responsividade.** Duas media queries de layout: em 940px o hero vira uma coluna só (e a arte sobe para cima do texto, via `order: -1`), em 620px somem o selo de vaga e os links secundários da nav. Todo o resto se adapta por `clamp()` nos tamanhos e `repeat(auto-fill, minmax(...))` nas grades.

**Movimento reduzido.** A última media query zera animação, transição e rolagem suave para quem pediu menos movimento no sistema. Nesse modo o terminal aparece inteiro de uma vez, as barras já nascem preenchidas e os números vão direto ao valor final — nada fica preso invisível.

**Teclado.** Link "pular para o conteúdo" como primeiro item do Tab, `:focus-visible` com contorno de 2px em tudo que recebe foco, e `:focus:not(:focus-visible)` para não poluir o clique de mouse. As seções têm `scroll-margin-top` para a barra fixa não cobrir o título ao navegar por âncora.

---

## 5. Antes de publicar

- [ ] Nenhuma marca `FALTA:` sobrou sem resolver — busque por `FALTA:` no arquivo
- [ ] O `[N]` dos chamados trocado nos dois lugares (`data-num` e o texto do `<b>`)
- [ ] Os três cartões `reservado` viraram projetos de verdade
- [ ] `SEU_ID_AQUI` trocado pelo ID real do Formspree
- [ ] Formulário testado com um envio de verdade
- [ ] Todos os links de repositório abrem
- [ ] Nenhuma credencial (`.env`, string de conexão, chave de API) nos repositórios que você linkou
- [ ] Testado nos dois temas
- [ ] Testado navegando só de Tab, sem mouse
- [ ] Aberto em um celular de verdade, não só no simulador do navegador
