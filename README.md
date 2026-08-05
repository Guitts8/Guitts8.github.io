# Portfólio — Raul Guilherme

Página única, um arquivo só (`index.html`), com CSS e JS embutidos. Sem framework, sem build, sem `node_modules`. Abre direto no navegador com dois cliques.

Única dependência externa: as fontes do Google Fonts, carregadas por `<link>`. Sem internet a página continua funcionando — só cai para a fonte do sistema.

**Arquivos:**

| arquivo | o que é |
|---|---|
| `index.html` | o site inteiro. É o único que vai para o GitHub Pages |
| `README.md` | este arquivo: o que falta e como publicar |
| `MELHORIAS.md` | dicas detalhadas de como escolher os números, os projetos e o que melhorar |
| `DADOS.md` | o formulário que você preencheu. Pode apagar quando quiser |

---

## 1. O que ainda falta preencher

O texto do site já está escrito. Sobrou só o que depende de dado que você ainda não tem. Procure por `[` no `index.html` — tudo entre colchetes é placeholder.

### a) Os quatro números do "sobre"

```html
<div class="numero"><b>[N]</b><span>[chamados resolvidos]</span></div>
```

Troque `[N]` pelo número e `[legenda]` pela descrição. **Como escolher números que valem alguma coisa: `MELHORIAS.md`, seção 1.**

### b) Os três cartões de projeto

Em cada `<article class="projeto">`:

- `[NOME_DO_PROJETO_N]` — aparece **duas vezes** no mesmo cartão: no `<h3>` e dentro do `<span class="so-leitor">`. Troque nos dois.
- `[O PROBLEMA que ele resolve]` — uma frase sobre o problema, não sobre a tecnologia
- `<p class="stack">` — as tecnologias, separadas por `·`
- `[URL_REPOSITORIO_N]` — o link do repositório

**Como escolher e descrever os projetos: `MELHORIAS.md`, seção 2.**

Para adicionar um projeto, copie um `<article>` inteiro. Para criar uma categoria nova (ex: `dados`):

1. Adicione o botão dentro de `<div class="filtros">`:
   ```html
   <button class="filtro" type="button" data-filtro="dados" aria-pressed="false">dados</button>
   ```
2. No cartão, use a mesma string em dois lugares: `data-tag="dados"` no `<article>` e o texto do `<p class="tag">`.

As strings precisam bater exatamente — o JS compara texto puro. Se um filtro ficar sem nenhum projeto, apague o botão.

### c) O ID do Formspree

Procure por `SEU_ID_AQUI`. Instruções na seção 2 abaixo.

### d) O currículo em PDF (quando tiver)

O bloco está comentado no HTML, na lista de contato. Quando tiver o link do Drive, descomente e troque `[URL_CURRICULO_PDF]`.

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
   git init
   git add index.html README.md MELHORIAS.md
   git commit -m "portfólio"
   git branch -M main
   git remote add origin https://github.com/Guitts8/Guitts8.github.io.git
   git push -u origin main
   ```

   Se não quiser publicar as anotações junto, suba só o `index.html`.

2. No GitHub: **Settings** → **Pages** → em *Source* escolha **Deploy from a branch** → branch `main`, pasta `/ (root)` → **Save**.

3. Espere um ou dois minutos e recarregue a página de Settings — o link aparece no topo.

Cada `git push` novo republica o site sozinho. A propagação leva até um minuto.

---

## 4. Notas técnicas

**Cores.** Só existem 6 cores nomeadas, todas no bloco `:root` do topo do CSS. Não há nenhum hexadecimal no resto do arquivo — hovers e transparências saem de `color-mix()` sobre os tokens. Para trocar a identidade visual inteira, mexa só nesses 12 valores (6 do tema escuro + 6 do claro).

**Contraste.** Verificado com a fórmula de luminância relativa da WCAG, não estimado. Todos os pares de texto passam AA (mínimo 4.5:1):

| par | escuro | claro |
|---|---|---|
| texto / fundo | 16.09:1 | 16.93:1 |
| texto / superfície | 14.72:1 | 17.99:1 |
| apagado / fundo | 7.75:1 | 5.90:1 |
| acento / fundo | 9.94:1 | 5.13:1 |
| fundo sobre acento (botão cheio) | 9.94:1 | 5.13:1 |

Se você trocar as cores, **refaça a conta** antes de publicar: <https://webaim.org/resources/contrastchecker/>.

O acento do tema claro (`#0A6FA8`) é bem mais escuro que o do escuro (`#5CC8F5`) de propósito: o ciano claro dá 1.8:1 sobre fundo branco, seria ilegível.

**`--line` vs `--muted` nas bordas.** As bordas de campo de formulário usam `--muted`, não `--line`. A WCAG 1.4.11 exige 3:1 em bordas que carregam significado, e `--line` (1.5:1) é decorativa — serve para divisórias e bordas de cartão, onde não há essa exigência.

**Temas.** O atributo `data-theme` fica no `<html>`. Um script no `<head>` aplica o tema salvo *antes* da primeira renderização, para não piscar branco ao carregar. Na primeira visita segue a preferência do sistema operacional. Todo acesso ao `localStorage` está dentro de `try/catch` — em aba anônima ou com cookies bloqueados a troca continua funcionando, só não sobrevive ao reload.

**Filtro.** Um `addEventListener` só, no container dos botões (delegação de evento). O estado ativo é `aria-pressed`, não uma classe — o CSS estiliza por `[aria-pressed="true"]` e o leitor de tela anuncia sozinho. Os cartões escondidos usam o atributo `hidden`, que tira o elemento do fluxo **e** da ordem de tabulação, então o link de um cartão filtrado não fica capturando o Tab.

**Stack agrupada.** São 20 itens com nível. Em lista corrida viravam uma parede de barras, então estão divididos em cinco grupos (back-end, dados, front-end, infra e redes, operação e segurança), cada um ordenado do maior nível para o menor. Cada grupo é um `<div class="grupo">`; para mover um item, é só recortar o `<div class="nivel">` inteiro.

**Responsividade.** Uma media query só para layout (nav abaixo de 620px). Todo o resto se adapta por `clamp()` nos tamanhos e `repeat(auto-fill, minmax(...))` nas grades. A segunda media query é a de `prefers-reduced-motion`.

**Movimento.** A revelação ao rolar usa `IntersectionObserver`, sem listener de scroll. Cada elemento é revelado uma vez e sai da observação. As classes de opacidade só se aplicam dentro de `.js`, adicionada pelo script do `<head>` — com JavaScript desligado a página nasce inteira visível em vez de invisível.

**Teclado.** Link "pular para o conteúdo" como primeiro item do Tab, `:focus-visible` com contorno de 2px em tudo que recebe foco, e `:focus:not(:focus-visible)` para não poluir o clique de mouse. As seções têm `scroll-margin-top` para a barra fixa não cobrir o título ao navegar por âncora.

---

## 5. Antes de publicar

- [ ] Nenhum `[COLCHETE]` sobrou — busque por `[` no arquivo
- [ ] `SEU_ID_AQUI` trocado pelo ID real do Formspree
- [ ] Formulário testado com um envio de verdade
- [ ] Todos os links de repositório abrem
- [ ] Nenhuma credencial (`.env`, string de conexão, chave de API) nos repositórios que você linkou
- [ ] Testado nos dois temas
- [ ] Testado navegando só de Tab, sem mouse
- [ ] Aberto em um celular de verdade, não só no simulador do navegador
