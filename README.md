# Portfólio — Raul Guilherme

Página única com CSS e JS embutidos no `index.html`. Sem framework, sem build, sem `node_modules`. Abre direto no navegador com dois cliques.

Duas dependências externas, ambas opcionais para a página funcionar: as fontes do Google Fonts (sem internet cai para a fonte do sistema) e duas imagens, o avatar e o Tux.

**Arquivos:**

| arquivo | o que é |
|---|---|
| `index.html` | o site inteiro: HTML, CSS e JS |
| `assets/avatar.png` | o avatar do hero. **Precisa ir junto para o GitHub Pages** |
| `assets/tux.png` | o pinguim do cartão "1 Tux", seção 01. **Idem** |
| `README.md` | este arquivo: o que falta e como publicar |
| `.gitignore` | o que **não** sobe para o repositório |

E dois que ficam só na sua máquina, fora do git:

| arquivo | o que é |
|---|---|
| `PALETAS.md` | cinco paletas prontas para colar e testar, com contraste já verificado |
| `DADOS.md` | o formulário que serviu para montar o site. Pode apagar quando quiser |

**Este repositório é o próprio site, e é público.** Todo arquivo que não estiver no `.gitignore` fica servido em `guitts8.github.io/<nome-do-arquivo>` com o seu nome em cima — inclusive os que ninguém linkou. É por isso que rascunho, formulário e configuração de editor estão na lista de exclusão. Na dúvida sobre um arquivo novo: ignore primeiro, publique depois de olhar.

Os caminhos `assets/...` no HTML são relativos. Se você mover as imagens de pasta, o hero e o cartão do Tux ficam com o texto alternativo no lugar do desenho.

**Seções da página:** hero · 01 sobre · 02 projetos · 03 jogos · 04 segurança e redes · 05 stack · 06 trajetória · 07 contato.

**Cada área tem um sotaque de cor:** software no âmbar de sempre, jogos em fúcsia, segurança em verde. Só `--accent` e `--accent-2` mudam, dentro de `#jogos` e `#seguranca` (e nos atalhos do menu e do hero que levam até elas). O bloco fica no CSS, procure por "SOTAQUE DE COR POR ÁREA".

**A página é bilíngue (inglês e português).** Todo texto visível existe duas vezes, lado a lado, marcado com `data-l="en"` e `data-l="pt"`:

```html
<span data-l="en">projects</span><span data-l="pt">projetos</span>
```

O CSS esconde o idioma inativo. **Ao mudar um texto, mude os dois.** Atributos (`aria-label`, `placeholder`, `alt`) ficam em inglês no próprio atributo e em português num `data-pt-<atributo>`; o JS troca. O botão `PT`/`EN` no topo alterna e grava a escolha.

Quem decide o idioma, nesta ordem: `?lang=en` ou `?lang=pt` na URL > a escolha salva no navegador > o idioma do navegador (português vira PT, o resto vira EN). **Nos e-mails para empresas de fora, mande `https://guitts8.github.io/?lang=en`** — e, para apontar direto para uma área, `?lang=en#jogos` ou `?lang=en#seguranca`.

---

## 1. O que ainda falta preencher

**Procure por `FALTA:` no `index.html`** — são 2 marcas, cada uma com a instrução no lugar.

### a) O ID do Formspree

É o único item que **bloqueia** a publicação: sem ele o formulário de contato não envia nada. Procure por `SEU_ID_AQUI`. Instruções na seção 2 abaixo.

### b) O currículo em PDF (quando tiver)

O bloco está comentado no HTML, na lista de contato da seção 07. Quando tiver o link do Drive, descomente e troque `URL_DO_CURRICULO_PDF`.

### Opcional: ferramentas de segurança (seção 04)

A lista `<ul class="conceitos">` tem os conceitos que já estão na sua stack. Quando começar a usar Wireshark, Nmap ou tcpdump **de verdade**, adicione ali. Item que você não sabe defender numa entrevista custa mais caro do que a linha a mais vale.

---

## 2. Como mexer nas seções que já estão prontas

### Projetos (seção 02)

Os três cartões reservados viraram projetos de verdade: **domumERP**, **FluxaAI** e **UmbraForge**. Cada `<article class="projeto">` tem tag, título, descrição do problema, chips de stack e link do repositório.

Na descrição, o problema vem primeiro — quem tinha, o que doía. A tecnologia fica na linha de baixo, nos chips. Um cartão que abre com "aplicação Next.js com Prisma" já perdeu o leitor.

Esta seção é só de **software**. Projeto de jogo vai para a grade "projetos de jogos" da seção 03, e projeto de segurança para a grade "projetos de segurança" da seção 04 — cada um na área dele. Os filtros daqui são por tipo: `sistema`, `ia` e `ferramenta`. Projeto com dois tipos leva os dois no `data-tag`, separados por espaço. Para criar uma categoria nova (ex: `dados`):

1. Adicione o botão dentro de `<div class="filtros">`:
   ```html
   <button class="filtro" type="button" data-filtro="dados" aria-pressed="false">dados</button>
   ```
2. No cartão, use a mesma string em dois lugares: `data-tag="dados"` no `<article>` e o texto do `<p class="tag">`.

As strings precisam bater exatamente — o JS compara texto puro. Se um filtro ficar sem nenhum projeto, apague o botão.

O estilo `.projeto.reservado` continua no CSS, para quando você quiser anunciar um projeto que ainda não existe: é um `<article class="projeto reservado revelar">` com tag, `h3` e descrição, sem chips e sem link.

### Stack (seção 05)

Duas colunas: as 18 barras à esquerda, a grade de 12 logos à direita.

As barras são uma lista corrida, ordenada do maior nível para o menor. Para mover ou acrescentar um item, recorte o `<div class="nivel">` inteiro — o valor aparece em dois lugares (o texto do `<span class="valor">` e o `--nivel` da barra) e os dois precisam bater.

A coluna dos logos é `position: sticky`: ela tem 4 fileiras contra 18 barras, então acompanha a rolagem em vez de deixar um vão do lado direito. Se preferir parada, apague o `position: sticky` de `.stack-logos`.

**As cores dos logos estão nos tokens `--m-*`**, não dentro dos SVGs. Para trocar a cor de uma marca, mexa no token. Detalhe do porquê na seção 4.

Os desenhos vieram do [Simple Icons](https://simpleicons.org) (24×24). C# e SQL Server não existem lá — foram removidos por questão de marca —, então esses dois vieram do [Devicon](https://devicon.dev) e têm `viewBox` de 128×128. É por isso que os `viewBox` são diferentes entre si.

### Jogos (seção 03)

Três cartões (história, partida, bug), a grade **projetos de jogos** (por enquanto com um cartão reservado), a grade de motores (Unity, Godot, Unreal, C++, Blender) e a lista do que você trabalha em jogos. O texto diz com todas as letras que é projeto pessoal, não estúdio: mantenha assim até ter experiência em estúdio. Quando publicar um jogo, copie o `<article class="projeto">` de um projeto da seção 02, troque o conteúdo e cole na grade de projetos de jogos, no lugar do cartão reservado. A seção 04 funciona igual para projetos de segurança.

### Trajetória (seção 06)

Sete marcos, do mais recente para o mais antigo, misturando trabalho e formação. Os três primeiros são os cargos na Supermídia.

Os marcos são em primeira pessoa, igual ao resto da página ("instalo", "parei", "entrei"). Ao acrescentar um, siga a mesma voz.

**O título é "Trajetória profissional."**, e não "Como eu cheguei até aqui" como era antes: um título que promete começar do começo, numa lista que começa pelo cargo de hoje, briga com a própria seção. O título nomeia a seção e para por aí; o subtítulo diz o que a trajetória significa (três cargos no mesmo sentido), e não como lê-la. ⚠️ **A seção não se explica em voz alta** — quem mostra que a ordem é do presente para o passado é o desenho: o cartão aceso no topo, o trilho apagando para baixo e as datas em ordem decrescente. Se você sentir vontade de escrever a regra de leitura no subtítulo, o desenho é que está fraco.

Cada marco é um `<li class="marco" data-tipo="…">` com um `.marco-caixa` dentro. Dois atributos governam a aparência:

- **`data-tipo`** vale `cargo`, `virada` ou `formação`. Aparece como etiqueta no `.marco-topo` e, no CSS, só o `cargo` ganha o anel de acento no ponto do trilho — o resto fica em tom de divisória. É o que deixa a lista ser lida na diagonal: dá para achar só os cargos sem ler um parágrafo. Se inventar um quarto tipo, decida no CSS o que ele faz com o ponto.
- **`class="agora"`** no primeiro. É o único marco que vira cartão de verdade — fundo, borda de acento, ponto cheio e o selo "atual" com o pontinho pulsando. Sem esse desnível a lista inteira lê no mesmo peso, e a ordem invertida vira só uma lista de datas.

**O `.marco-caixa` existe para o hover.** O `<li>` não pode receber o fundo direto: ele carrega o `padding-left` que afasta o texto do trilho, e o fundo pintaria por cima do trilho. A borda do cartão nasce `transparent` em vez de ausente — se ela só aparecesse no hover, o cartão cresceria 2px e o texto pularia de linha debaixo do mouse.

**O trilho é um elemento só** (`.linha-tempo::before`), do topo ao fim da lista, e não uma borda por item. Duas razões: não quebra no vão entre os marcos e, principalmente, pode ser um **gradiente**. É o gradiente que carrega a ideia do título — aceso no agora, apagando conforme desce para o passado. O `top: 1.15rem` é o mesmo do primeiro ponto: o trilho nasce dentro dele, nunca acima.

**A seção é de duas colunas**, igual à 04: os marcos à esquerda, o radar grudado à direita. Quem governa a largura é a coluna, e a medida do texto continua controlada pelo `max-width: 62ch` do `.marco p`.

**A divisão `1.12fr / .88fr` não é chute.** A coluna da esquerda precisa caber os 62ch do `.marco p` (uns 575px) mais o recuo do trilho e o padding do cartão — uns 620px dos 1200 disponíveis. Apertar mais que isso estreita a medida do texto, que é a única coisa da seção que não é negociável. O resto foi para a direita, e o `gap` encolheu junto (de `6vw` para `4.5vw`): era ele que empurrava o desenho para longe do texto.

⚠️ Mesma armadilha da 04: **o `.revelar` fica nas colunas, nunca no `.traj-duas`**. A animação de revelar usa `transform`, e um ancestral com `transform` vira o bloco de contenção do `position: sticky` — o radar para de grudar.

#### O radar de topologia

SVG inline no lugar do antigo mapa em árvore. É decoração temática e está assumido como tal: `aria-hidden`, nenhum dado ali que o texto ao lado já não diga. Existe para ocupar o vão e para dizer, sem escrever, de que assunto a seção trata.

**A geometria.** Centro em `(180,180)`, `viewBox` quadrado `0 0 360 360`. Três eixos a 0°, 120° e 240°, com um nó no anel de fora (r=150) e um no de dentro (r=90), mais o núcleo. A leitura é de fora para dentro — o que o cliente encosta a mão fica na borda, o dado fica no meio:

| eixo | nó externo | nó interno |
|---|---|---|
| 0° | `(180,30)` cliente | `(180,90)` rede |
| 120° | `(310,255)` integração | `(258,225)` serviço |
| 240° | `(50,255)` dispositivo | `(102,225)` firewall |

⚠️ **O desenho tem que ficar centrado no `viewBox`.** É isso que deixa o `transform-origin` da varredura ser simplesmente `180px 180px`. Se mudar o `viewBox`, acerte o `transform-origin` de `.radar-varredura` junto, ou a cunha passa a girar torta.

Cinco coisas valem atenção:

- **Cada ligação aparece duas vezes com o mesmo `d`** — uma como traço parado (`.radar-link`) e outra como pacote (`.radar-fluxo`). Se mexer numa coordenada, mexa nas duas: elas andam em par. São nove.
- **O `pathLength="100"`** normaliza toda ligação para 100 unidades, independentemente do comprimento real. É o que deixa um único `stroke-dasharray` no CSS servir para as nove de uma vez. O pacote é um traço curto correndo por `stroke-dashoffset`, e não um círculo com `offset-path`, justamente para não duplicar as coordenadas em mais um lugar.
- **`transform-box: fill-box` + `transform-origin: center`** nos halos e no ping. Sem os dois, o `scale` gira em torno do `(0,0)` do viewBox e o anel sai voando para o canto — em SVG a origem do transform não é o centro do desenho. Na varredura é `transform-box: view-box`, que é outro caso: ali o que se quer é justamente o centro do viewBox, não o da cunha.
- **O gradiente da varredura é `gradientUnits="userSpaceOnUse"`.** No padrão (`objectBoundingBox`) o `cx/cy` de 50% cai no centro da *caixa da cunha*, que fica lá pelo meio do raio, e o brilho vira um borrão solto no meio do nada. E as paradas são pintadas por CSS (`.varre-*`), não por atributo: `var(--accent)` não vale em atributo de apresentação, e a regra da casa é cor nenhuma fora do `:root`.
- **A agulha fica na borda de 70°, não na de 0°.** A cunha vai de 0° a 70° e gira no sentido horário — quem vai na frente é o lado de 70°.

**Os halos não pulsam em ritmo próprio: eles acendem quando a agulha passa.** O `--atraso` de cada nó é o ângulo dele convertido em tempo — `((ângulo − 70 + 360) % 360) / 360 × 9s`, onde 70 é onde a agulha começa e 9s é a volta inteira. Daí os `7.25s` (eixo 0°), `1.25s` (120°) e `4.25s` (240°) no HTML. ⚠️ **Se mudar a duração do giro, os três atrasos mudam junto.**

Já os `--atraso` dos pacotes não são múltiplos redondos de propósito: em passo regular as nove linhas pulsam em bloco e o desenho vira metrônomo. Mesma lógica dos tempos primos das `.formas`.

**Os rótulos são a parte apertada.** Sobram 30 unidades entre o anel de fora e a borda do `viewBox`, e é lá que eles vivem, junto das marcas de bordo. Os dois pares de baixo caem quase na mesma vertical, então os de dentro são puxados para dentro (`244` e `116`, e não `258` e `102`) e os de fora descem até `y=290`. ⚠️ Ao trocar qualquer palavra, **confira sobreposição** — não há folga para uma palavra mais longa.

**O sticky prende uma caixa da altura da janela, não o desenho.** O `.traj-radar` é `height: calc(100vh - var(--alt-nav))` com `display: flex` e `align-items: center`; o SVG fica centralizado dentro dela. Sem isso o desenho gruda colado embaixo da barra e sobra tela vazia debaixo dele enquanto você rola. Funciona porque o `.traj-duas` é muito mais alto que a janela — se a seção encolher para menos de uma tela, não há percurso para grudar e o efeito some.

O `max-height` no `.radar` é a trava para tela baixa: sem ela o desenho estoura a janela de um notebook e o topo sai cortado, justamente por estar centralizado em vez de ancorado no topo.

Abaixo de 900px o radar **sai inteiro** (`display: none`), em vez de descer para baixo dos marcos. Em celular ele custaria uma tela de rolagem para não dizer nada que o texto já não diga. Em movimento reduzido acontece o meio-termo: o desenho e a cunha ficam — cunha parada é forma, não movimento —, e somem os pacotes, o ping e o pulso do selo.

---

## 3. Configurar o formulário (Formspree)

**Já configurado** (ID `xrpqvgpw`, recebe em contato.raulguilherme@gmail.com). Os passos abaixo servem só se um dia você trocar de formulário.

1. Crie uma conta grátis em <https://formspree.io>
2. **New Form** → escolha o e-mail que vai receber as mensagens
3. Ele mostra um endpoint no formato `https://formspree.io/f/xayzbwqd`. Copie a parte final — o ID (`xayzbwqd`)
4. No `index.html`, procure por `SEU_ID_AQUI` e troque:
   ```html
   <form class="revelar" id="form-contato" action="https://formspree.io/f/xayzbwqd" method="POST">
   ```
5. Envie uma mensagem de teste. No primeiro envio o Formspree pede confirmação por e-mail.

O envio é feito por JavaScript: quem escreve continua na página e vê a confirmação embaixo do botão, no idioma em que está lendo. Enquanto `SEU_ID_AQUI` estiver no lugar, o formulário não tenta enviar e mostra um aviso pedindo para usar o e-mail direto, para nenhuma mensagem se perder. O assunto do e-mail que chega para você está no campo `_subject`.

O plano grátis aceita **50 envios por mês**. O campo `_gotcha` já está no formulário: é uma armadilha invisível que o Formspree usa para descartar robôs — não mexa nele.

---

## 4. Publicar no GitHub Pages

Repositório: `Guitts8/Guitts8.github.io`. Como o nome bate exatamente com o usuário, o site cai no endereço raiz **`https://guitts8.github.io`**, sem sufixo — é esse o link para colar no currículo e no LinkedIn.

O arquivo precisa se chamar `index.html` e estar na raiz do repositório.

1. No terminal, dentro desta pasta:

   ```bash
   git add -A
   git commit -m "portfólio"
   git push
   ```

   O `-A` manda tudo que mudou; quem decide o que fica de fora é o `.gitignore`, não a lista do `git add`. Antes de commitar, confira com `git status` — se aparecer algum arquivo que você não quer publicar, ele vai para o `.gitignore`, não para o comando.

   A pasta `assets` precisa ir junto: sem ela o avatar e o Tux não aparecem no site publicado.

2. No GitHub: **Settings** → **Pages** → em *Source* escolha **Deploy from a branch** → branch `main`, pasta `/ (root)` → **Save**.

3. Espere um ou dois minutos e recarregue a página de Settings — o link aparece no topo.

Cada `git push` novo republica o site sozinho. A propagação leva até um minuto.

---

## 5. Notas técnicas

### Cores

Existem **8 cores de tema** e **12 cores de marca**, todas no bloco `:root` do topo do CSS. Não há nenhum hexadecimal no resto do arquivo — hovers, brilhos e transparências saem de `color-mix()` sobre os tokens.

As 8 do tema são as que definem a identidade. Para trocar o visual inteiro, mexa só nesses 16 valores (8 do escuro + 8 do claro).

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

As 12 de marca (`--m-csharp`, `--m-dotnet`, `--m-node`, `--m-java`, `--m-python`, `--m-postgres`, `--m-sqlserver`, `--m-js`, `--m-ts`, `--m-react`, `--m-git`, `--m-linux`) são as cores oficiais de cada tecnologia da grade de logos da seção 04. Elas **não** fazem parte da sua identidade visual e não devem ser trocadas junto com o tema — mexer nelas descaracteriza a marca.

Elas ficam no `:root` em vez de dentro dos SVGs por dois motivos: manter a regra de "nenhuma cor fora do bloco de tokens" e porque cada tema precisa de um valor diferente. No escuro, o roxo do .NET (`#512BD4`) e o preto do Java somem contra o fundo, então os valores estão clareados. No claro acontece o inverso com o amarelo do JavaScript e o ciano do React, e o bloco `[data-theme="light"]` devolve tons mais escuros.

### Contraste

Verificado com a fórmula de luminância relativa da WCAG, lida direto dos tokens do arquivo — não estimado. Todos os pares de texto passam AA (mínimo 4.5:1):

| par | escuro | claro |
|---|---|---|
| texto / fundo | 17.06:1 | 17.32:1 |
| texto / faixa | 16.53:1 | 15.71:1 |
| texto / cartão | 15.88:1 | 18.83:1 |
| apagado / fundo | 6.94:1 | 6.94:1 |
| apagado / faixa | 6.73:1 | 6.29:1 |
| apagado / cartão | 6.46:1 | 7.54:1 |
| acento / fundo | 11.00:1 | 5.87:1 |
| acento / cartão | 10.24:1 | 6.39:1 |
| fundo sobre acento (botão cheio) | 11.00:1 | 5.87:1 |

O acento do tema claro (`#8A5200`) é bem mais escuro que o do escuro (`#FFB13D`) de propósito: o âmbar claro dá 1.8:1 sobre fundo claro, seria ilegível.

`--accent-2` não aparece na tabela porque nunca carrega texto — é só a elipse e o brilho do hero.

**Logos da seção 04.** Não são texto, então a régua que vale é a de objeto gráfico: 3:1. Os 12 passam nos dois temas, com folga. O pior caso é o SQL Server no tema escuro (4.91:1) e o React no claro (4.40:1).

Se você trocar as cores, **refaça a conta** antes de publicar: <https://webaim.org/resources/contrastchecker/>.

### Tipografia

Três famílias, uma função cada:

- **Archivo Black** (`--f-display`) — só títulos, sempre em caixa alta. É o que dá o peso da página
- **Space Grotesk** (`--f-sans`) — parágrafos de leitura corrida (o "sobre", a trajetória)
- **JetBrains Mono** (`--f-mono`) — todo o resto: rótulo, botão, chip, terminal, formulário, rodapé

### Elementos gráficos

Fora as duas imagens, todos são CSS ou SVG inline.

**Avatar (hero).** `assets/avatar.png`, 880×880 com fundo transparente. O original tinha 1254px e 592 KB; foi reduzido para 880px (o dobro do tamanho em que aparece, o suficiente para tela retina) e 371 KB. Se quiser cortar mais, passe por <https://tinypng.com> ou converta para WebP — é de longe o arquivo mais pesado da página.

O `width` e o `height` no HTML batem com o arquivo para o navegador reservar o espaço antes de baixar, senão a página pula quando a imagem chega.

O personagem é quase todo preto e o fundo do site também. Duas coisas fazem ele aparecer: o disco grande no acento, posicionado atrás do tronco de propósito, e três `drop-shadow` empilhados no CSS. `drop-shadow` segue o recorte transparente do PNG, não a caixa da imagem — é por isso que ele funciona como contorno aqui e um `box-shadow` não funcionaria. No tema claro esse contorno some: o preto já se destaca sozinho sobre fundo claro.

**Tux (cartão da seção 01).** `assets/tux.png`, 160×240 e 37 KB — o dobro do tamanho em que aparece. O cartão usa o modificador `.numero-tux`, que o transforma em flex para o pinguim encostar na direita.

A altura dele vai até 84px, menos que os ~70px de texto mais o padding do cartão. **Isso é proposital:** enquanto ele for mais baixo que o conteúdo de texto, os quatro cartões continuam do mesmo tamanho. Aumentar o `clamp` estica a linha inteira da grade.

A arte tem fundo preto opaco, não transparente, e o cartão do tema escuro é quase preto — sem uma borda a emenda apareceria. Por isso o `border: 1px solid var(--line)`, que resolve nos dois temas. No tema claro ele fica bem mais evidente, como uma miniatura de foto.

**Terminal (seção "sobre").** Fica ao lado do texto do "sobre", embaixo dos quatro números — é onde `whoami` faz sentido. O conteúdo é texto de verdade, não imagem: leitor de tela lê e busca indexa. As linhas entram em cascata (150ms entre cada) quando o bloco chega na tela; sem JavaScript nascem todas visíveis, porque a opacidade zero só existe dentro de `.js`.

**Formas.** Seis elementos em `.formas`, cada um com sua própria animação de flutuação (9s a 19s). Os tempos são propositalmente primos entre si para nunca sincronizarem — se sincronizassem, a composição inteira pulsaria junto e ficaria mecânica.

**Partículas.** Um `<canvas>` fixo cobrindo a viewport, com 42 pontinhos subindo devagar (20 no celular). Substituiu a poeira em SVG que existia antes — eram 24 círculos piscando, e ter três sistemas de fundo ao mesmo tempo (formas + poeira + partículas) era fundo demais disputando atenção.

Duas coisas nele valem atenção. A cor **não está no CSS**: o JS lê o token `--accent` e redesenha quando o tema muda, via `MutationObserver` no atributo `data-theme` do `<html>` — é assim que o bloco fica independente do bloco do tema. E o canvas é dimensionado pelo `devicePixelRatio` (limitado a 2), senão o ponto de 1px sai borrado em tela retina.

Pausa sozinho quando a aba sai de foco (`visibilitychange`), para não queimar bateria desenhando o que ninguém vê.

**Radar de topologia (seção 05).** SVG inline na coluna direita da trajetória: três anéis, três eixos, sete nós e uma varredura girando. Detalhado em ["Trajetória (seção 05)"](#trajetória-seção-05), na seção 2.

**Trama e brilho.** Duas camadas `position: fixed` com `z-index` negativo. A trama é uma grade de pontos feita com `radial-gradient` repetido, mascarada por um gradiente para sumir na direção do rodapé. O brilho são dois `radial-gradient` grandes atrás do hero.

**Faixas alternadas.** As seções com a classe `.faixa` usam `--bg-alt` e ganham uma linha degradê no topo e na base, para a página não ser um bloco só de preto.

### Efeitos (seção 14 do CSS)

Sete efeitos inspirados no portfólio da Lohane (<https://llohs.github.io/llohs-dev/>), adaptados para a identidade âmbar/Linux daqui. **Nenhum deles é necessário para ler a página**: todos dependem de JS e todos morrem na media query de movimento reduzido.

| efeito | onde | como funciona |
|---|---|---|
| **tela de boot** | `.boot`, logo depois do `<body>` | painel centralizado com log de 5 linhas, scanlines, varredura e barra de progresso. ~2.5s, uma vez por sessão |
| **scramble** | `.hero h1` | o título nasce embaralhado e assenta letra a letra, 800ms |
| **glitch RGB** | `.glitch` nos spans do h1 | três camadas: blocos opacos + cópias vermelha/ciano em faixas de `clip-path`, 500ms em `steps()`. Um pulso no fim do scramble e um a cada 9s |
| **partículas** | `<canvas class="particulas">` | ver acima |
| **CRT** | `.terminal::before` / `::after` | textura de scanlines + linha varrendo em 3.2s |
| **tilt 3D** | `.projeto` | inclina até 6° seguindo o cursor, com brilho no ponto do mouse |
| **ondulação + ímã** | `.btn` | círculo saindo do clique; o botão desliza na direção do cursor |

**A tela de boot é CSS, não JS — de propósito.** A animação de saída (`boot-sai`, atraso `var(--boot-espera)`) está declarada no próprio elemento. Se o script do rodapé nunca rodar (erro, bloqueador, rede caindo no meio), a tela sai sozinha e a página não fica trancada atrás de um overlay preto. O JS só grava o `sessionStorage`, tira o nó do DOM e chama o scramble.

Quem decide se o boot aparece é o script do `<head>`, não o do rodapé: lá embaixo a página já pintou, e a tela entraria por cima do conteúdo já visível. A classe `.sem-boot` nasce junto com o `<html>`, antes do primeiro paint. Pula quem já viu nesta aba e quem pediu menos movimento. Clique ou tecla cortam na hora.

**O boot é um painel centralizado, não a tela inteira.** O `.boot` é só o fundo (grade de pontos com vinheta, redesenhada ali porque o fundo opaco cobre a `.trama` de verdade, que vive em `z-index` negativo). O que aparece no meio é o `.boot-painel`:

| parte | o que é |
|---|---|
| `boot-liga` | o painel abre de uma linha para a caixa inteira, estourado de brilho, e assenta — CRT ligando |
| `.boot-cantos` | os quatro colchetes de HUD. Oito gradientes chapados num `<i>` vazio: cada canto é um traço deitado mais um em pé |
| `.boot-topo` | barra de título, `crinos@dev` / `sys/init · 0x1A` |
| `.boot-log` | as 5 linhas, com scanlines por cima |
| `.boot-painel::after` | a linha de varredura, mesmo `@keyframes varre` do terminal da seção 01, só que em 1.6s — o painel vive 2.5s, e uma passada de 3.2s não daria nem uma volta |
| `.boot-barra` | a barra de progresso do rodapé |

As scanlines ficam **só sobre o log**, não no painel inteiro. Passando por cima da barra de título e da de progresso, o efeito vira sujeira em vez de textura.

Os colchetes moram num `<i>` e não num pseudo do painel porque os dois pseudos do painel já têm dono (o fundo do `.boot::before` e a varredura do `::after`) — e uma borda comum não daria o recorte só nos cantos.

⚠️ **Os tempos do boot vivem em dois lugares.** No CSS há **um** só: os tokens `--boot-espera` (2.2s) e `--boot-passo` (300ms), declarados no `.boot`. A saída, a cascata das linhas e a barra de progresso derivam os três desses dois valores, então mexer ali move o conjunto junto. O outro lugar é o JS: `setTimeout(fimDoBoot, 3400)`, a rede de segurança para quando `animationend` não dispara (aba em segundo plano). **Se aumentar `--boot-espera`, aumente o 3400 junto** — senão o JS remove a tela no meio da animação.

A conta do ciclo: as linhas partem com 250ms de atraso (o tempo do painel abrir — linha entrando enquanto a caixa ainda cresce sai tremida), a última entra em `250ms + 4 × 300ms = 1450ms` e leva 250ms para aparecer, então o log está completo em 1.7s; a saída começa em 2.2s e dura 350ms. Total ~2.55s, com o log inteiro parado na tela por meio segundo. A versão anterior fechava em 1.65s e na prática piscava sem dar para ler nada.

A barra de progresso enche em `--boot-espera` exato: quando ela chega ao fim, a tela começa a sair. É por isso que as duas leem o mesmo token — barra que termina antes ou depois da saída denuncia que o número é decorativo.

O contrapeso de esticar mais: cada 100ms a mais é 100ms que um recrutador olha para uma tela preta antes de ver o portfólio. Como ela é pulável por clique ou tecla e só aparece uma vez por sessão, 2.5s passa sem culpa — mas não vá muito além disso.

**O glitch são três camadas empilhadas**, e é a soma delas que dá o estrago:

1. o próprio span, com blocos chapados de `--bg` piscando atrás do texto (`glitch-bloco`)
2. a cópia vermelha (`::before`), recortada em faixa, com fundo opaco
3. a cópia ciano (`::after`), em faixa complementar, também opaca

As faixas das duas cópias são complementares de propósito: quando a vermelha está no topo, a ciano está embaixo. Se coincidissem, a de cima taparia a de baixo e sobraria uma cor só piscando.

**Tudo anda em `steps(1, end)`.** Sem interpolação: cada quadro *salta* para o próximo. É essa ausência de transição que faz ler como defeito digital em vez de animação — glitch que desliza suave parece enfeite. São 10 quadros em 500ms, uns 20fps, que é o ponto de "cartucho com mau contato".

**O bloco opaco é o efeito, não um bug.** As cópias pintam `var(--bg)` atrás de si, então dentro da faixa o texto real some e sobra o retângulo com a cópia colorida por cima. Como o span é `display: block`, essa caixa tem a largura do `h1` inteiro — na linha curta ("STACK") o bloco sobra bem à direita da palavra, por cima do brilho do hero. Isso já foi motivo de eu **não** usar fundo aqui; é exatamente o artefato de vídeo pedido, então virou a regra.

⚠️ O último quadro de `glitch-a`/`glitch-b` fecha a faixa em zero **e** zera a opacidade. Os dois, não um só: `inset(0 0 0 0)` sozinho deixaria o bloco opaco parado por cima do título.

As cores `--glitch-1` e `--glitch-2` são a **única** exceção à regra de "nenhuma cor fora da identidade": o efeito depende de ler como vermelho e ciano. Não troque junto com o tema.

**Tilt: a perspectiva está na grade, não no cartão.** Se `perspective` ficasse em `.projeto`, cada cartão teria o próprio ponto de fuga e a fileira inteira pareceria torta. O tilt é ignorado se o cartão ainda não foi revelado (o `transform` naquele momento é o da animação de entrada) e se o botão do mouse está pressionado (a pessoa está selecionando texto).

**O deslocamento magnético é pequeno de propósito** — 12% na horizontal, 22% na vertical. Passar muito disso faz o botão fugir do ponteiro, e o efeito vira um alvo móvel em cima de um link de verdade.

Tilt e ímã só rodam em `pointer: fine`. No toque não existe "passar por cima": o dedo já é o clique.

**O glitch se repete a cada 9s, e o intervalo é o ponto.** O pulso está na função `pulsarGlitch()`, chamada em dois lugares: uma vez 850ms depois do scramble (para o glitch entrar só quando o texto já assentou) e depois num `setInterval` de 9s. O pulso dura 520ms, que é o tempo dos keyframes mais uma folga — tirar a classe antes disso cortaria o efeito no meio, e pior: o último quadro é o que zera a opacidade das cópias, então sair antes dele deixaria um bloco opaco parado por cima do título. O navegador só reinicia a animação depois que a classe sai, então esse número é o piso da repetição também.

Intervalo longo com pulso curto é o que separa "detalhe" de "distração": o título fica no canto do olho de quem está lendo o parágrafo logo abaixo do hero. **Não desça dos 9s.**

Com a aba escondida o pulso pula a rodada (`document.hidden`). O navegador estrangula timers em aba de fundo e as chamadas represadas sairiam todas juntas na volta — um surto de glitch no momento em que a pessoa volta para a página.

### Comportamento

**Temas.** O atributo `data-theme` fica no `<html>`. Um script no `<head>` aplica o tema salvo *antes* da primeira renderização, para não piscar ao carregar. Na primeira visita segue a preferência do sistema operacional. Todo acesso ao `localStorage` está dentro de `try/catch` — em aba anônima ou com cookies bloqueados a troca continua funcionando, só não sobrevive ao reload.

**Filtro.** Um `addEventListener` só, no container dos botões (delegação de evento). O estado ativo é `aria-pressed`, não uma classe — o CSS estiliza por `[aria-pressed="true"]` e o leitor de tela anuncia sozinho. Os cartões escondidos usam o atributo `hidden`, que tira o elemento do fluxo **e** da ordem de tabulação, então o link de um cartão filtrado não fica capturando o Tab.

**Rolagem.** Um `addEventListener` de scroll só, `passive`, com o trabalho dentro de um `requestAnimationFrame` que não empilha. Ele cuida de três coisas ao mesmo tempo: a barra de progresso, a borda que aparece na nav e o link da seção atual (`aria-current`).

**Revelação e contagem.** `IntersectionObserver`, sem listener de scroll. Cada elemento é revelado uma vez e sai da observação. Os números contam de zero ao chegar na tela; se `data-num` não for numérico, a contagem não roda e o texto fica intacto.

**Escalonamento.** Sem ele a página lê como se carregasse de uma vez: tudo que entra na tela no mesmo quadro sobe junto, num pop só. São três níveis de atraso, todos aplicados pelo JS como `transition-delay` inline:

| nível | passo | teto | onde aparece |
|---|---|---|---|
| blocos irmãos | 90ms | 450ms | os `.revelar` que o observer entrega na mesma leva |
| barras | 35ms | 700ms | as 18 barras da seção 04, que vivem num `.revelar` só |
| filhos de `.cascata` | 55ms | 650ms | os 12 logos e a lista de conceitos |

Os tetos existem para o último item de uma leva grande não ficar visivelmente atrasado do primeiro.

O atraso é inline, então valeria para **toda** transição do elemento — o hover do cartão ficaria lerdo pelo resto da visita. Por isso um `setTimeout` limpa o `transition-delay` depois que a revelação termina.

Para pôr um bloco novo em cascata, adicione a classe `cascata` no container (o mesmo elemento pode ser `revelar` e `cascata`, como a lista de conceitos). **Só faça isso onde o filho não tem `transform` próprio** — em `.numero` a cascata brigaria com o `translateY` do hover, e é por isso que os quatro cartões de número sobem juntos de propósito.

Nada disso roda com movimento reduzido: `atrasar()` sai antes de escrever qualquer coisa, e a media query zera `transition-delay` com `!important` caso a preferência do sistema mude no meio da visita.

**Sticky e a animação de revelar.** Na seção 04 o `.revelar` está nas duas colunas, e não no `.stack-duas` que as envolve. Não é estilo: a animação usa `transform`, e um ancestral com `transform` vira o bloco de contenção do `position: sticky`. Se você mover o `.revelar` para o container, a grade de logos para de grudar.

**Responsividade.** Quatro media queries de layout. Em 940px o hero vira uma coluna só (e a arte sobe para cima do texto, via `order: -1`); em 900px acontecem duas coisas — a stack deixa de ser duas colunas e os logos descem para baixo das barras com o sticky desligado, e a trajetória também vira uma coluna, com o radar saindo de cena; em 620px somem o selo de vaga e os links secundários da nav; em 400px a grade de logos aperta o espaçamento. Todo o resto se adapta por `clamp()` nos tamanhos e `repeat(auto-fill, minmax(...))` nas grades.

**Movimento reduzido.** A última media query zera animação, transição e rolagem suave para quem pediu menos movimento no sistema. Nesse modo o terminal aparece inteiro de uma vez, as barras já nascem preenchidas e os números vão direto ao valor final — nada fica preso invisível.

**Teclado.** Link "pular para o conteúdo" como primeiro item do Tab, `:focus-visible` com contorno de 2px em tudo que recebe foco, e `:focus:not(:focus-visible)` para não poluir o clique de mouse. As seções têm `scroll-margin-top` para a barra fixa não cobrir o título ao navegar por âncora.

---

## 6. Antes de publicar

- [ ] Nenhuma marca `FALTA:` sobrou sem resolver — busque por `FALTA:` no arquivo
- [ ] `SEU_ID_AQUI` trocado pelo ID real do Formspree
- [ ] Formulário testado com um envio de verdade
- [ ] Os três links de repositório abrem (domumERP, FluxaAI, UmbraForge)
- [ ] Nenhuma credencial (`.env`, string de conexão, chave de API) nos repositórios que você linkou
- [ ] `git status` conferido antes do commit — nada de interno na lista do que vai subir
- [ ] Testado nos dois temas — em especial a seção 04, onde as cores de marca mudam de valor, e o cartão do Tux
- [ ] Boot testado numa aba nova: ele só aparece uma vez por sessão, então recarregar não serve — use uma janela anônima
- [ ] Testado navegando só de Tab, sem mouse
- [ ] Aberto em um celular de verdade, não só no simulador do navegador
