# O que ainda dá para melhorar

Escrito para o seu caso específico: 21 anos, 4º semestre de ADS, helpdesk júnior, querendo vaga em back-end / infra / segurança. Não é lista genérica de portfólio.

Ordem de prioridade no fim do arquivo.

---

## 1. Os quatro números do "sobre"

O erro clássico aqui é colocar número que não significa nada. "+1000 xícaras de café" e "∞ linhas de código" não são dados, são enfeite — e recrutador técnico desconta pontos por isso.

**O critério:** um bom número é (a) verdadeiro, (b) verificável ou pelo menos defensável numa conversa, e (c) diz algo que o resto da página não diz.

Testa assim: se te perguntarem "de onde saiu esse número?" na entrevista, você tem resposta em uma frase? Se não tem, troca.

### Opções que funcionam no seu caso

| Número | Por que é bom | Onde você acha |
|---|---|---|
| **Chamados resolvidos** | é o seu diferencial real sobre outros júniores. Quase todo júnior tem projeto de faculdade; poucos têm volume de atendimento | Movidesk — filtra por responsável e período. Use o número do último ano, não o histórico total |
| **Tempo médio de resolução** | mostra que você mede o próprio trabalho, não só executa | Movidesk, relatório de SLA |
| **Anos mexendo com T.I.** | contando de 2023 (quando virou estudo), dá 3. Honesto e simples | você já sabe |
| **Projetos publicados** | só coloca depois de ter os repositórios prontos | GitHub |
| **Sistemas/máquinas que você dá suporte** | dimensiona o ambiente onde você trabalha | pergunte ao seu líder o número aproximado de estações/usuários |
| **Linguagens que você usa em projeto real** | 3 ou 4, e bate com a seção de stack | conte só as que aparecem nos seus repos |

### Regras práticas

- **Arredonde para baixo, nunca para cima.** "+400 chamados" quando foram 470 é mais forte que "500" inflado, porque você consegue defender.
- **Ponha o recorte na legenda**, não só o número: "chamados resolvidos em 2025" vale mais que "chamados resolvidos".
- **Se o número for baixo, não é problema — o problema é ele ser vago.** "12 meses em helpdesk" é honesto e diz mais que "vários projetos".
- Não repita informação que já está no hero (idade, semestre).

Onde editar: `index.html`, procure por `<div class="numeros`. Cada bloco tem o número em `<b>` e a legenda em `<span>`.

---

## 2. Os projetos

Essa é a parte que mais pesa e é a que está vazia. Vale mais atrasar a publicação do site duas semanas e ter 3 projetos decentes do que publicar hoje com card vazio.

### Quantos

**Três.** Dois se forem muito bons. Cinco só se cada um mostrar coisa diferente. Ninguém abre o quarto card.

### Quais escolher

Você quer vaga em back-end/infra/segurança. Então o conjunto ideal cobre:

1. **Uma API de verdade** — C#/ASP.NET, com banco, autenticação (JWT) e alguma regra de negócio que não seja CRUD puro. É o seu tiro principal: bate com o que você já estuda e com a vaga que você quer.
2. **Uma ferramenta que resolve algo do seu trabalho** — script que lê log, automatiza tarefa repetitiva do helpdesk, gera relatório do Movidesk, checa se um serviço caiu. Esse é o mais valioso de todos e quase ninguém tem: prova que você viu um problema real e o eliminou. Python ou PowerShell serve.
3. **Uma coisa de segurança** — analisador de log procurando padrão suspeito, verificador de senha vazada consultando a API do Have I Been Pwned, script que audita permissão de pasta. Amarra o discurso do site inteiro.

Um projeto web/front-end é opcional para o seu objetivo. Se tiver um bom, entra; se não, não faz falta.

### Como escrever a descrição

O campo é uma frase sobre **o problema**, não sobre a tecnologia. A stack já aparece na linha de baixo — repetir é desperdiçar a única frase que a pessoa vai ler.

| ❌ Não | ✅ Sim |
|---|---|
| "API REST desenvolvida em C# com Entity Framework e PostgreSQL" | "Chamado repetido chegava sem histórico, e a gente refazia diagnóstico do zero toda vez" |
| "Aplicação web full stack com React e Node" | "Meu grupo da facul perdia prazo porque o cronograma vivia no WhatsApp" |
| "Script Python para automação" | "Levava 40 minutos por semana para montar o relatório de chamados na mão" |

Fórmula: **quem tinha o problema + o que doía + com que frequência.** Sem adjetivo.

### O que deixa cada projeto duas vezes melhor

- **README no repositório** com print ou GIF de 10 segundos. A maioria dos recrutadores não clona nada — olha o README e fecha.
- **Link do deploy**, se der. Render, Railway e Fly.io têm plano grátis para API; Vercel para front. Projeto que abre e funciona vale muito mais que projeto que só existe em código.
- **Commits com mensagem legível.** Alguém vai abrir seu histórico. `fix`, `fix2`, `agora vai` conta uma história ruim.
- **Não publique `.env`, string de conexão ou chave de API.** Você quer vaga em segurança — credencial commitada no repositório é o tipo de coisa que encerra a conversa. Antes de publicar, rode `git log -p | grep -i -E "senha|password|secret|api.?key|connectionstring"` e confira. Se já vazou alguma, **troque a credencial**, não basta apagar o arquivo — ela continua no histórico.

### Enquanto não tiver os três

Deixe a seção com dois, ou remova os cards vazios e escreva uma linha só: "Estou selecionando os projetos que valem a pena mostrar." É melhor que `[NOME_DO_PROJETO_1]` no ar.

Se sobrar filtro sem projeto nenhum, apague o botão — filtro que não filtra nada parece bug.

---

## 3. A stack está grande

Você me mandou 20 itens com nível. Eu agrupei por área (back-end, dados, front-end, infra e redes, operação e segurança) porque 20 barras em lista corrida viram parede e ninguém lê.

Mesmo agrupado, vale pensar em cortar. **Argumento a favor de manter:** mostra amplitude, e para quem vem de suporte a amplitude é real. **Argumento a favor de cortar:** oito itens entre 45 e 55 comunicam "vi por cima" mais do que "sei fazer", e diluem os quatro números altos, que são os que te vendem.

Sugestão intermediária: mantenha os grupos, mas tire o que está em 45 (Spring Boot, Docker) das barras e passe para os chips de "já usei em projeto ou estudo". Um chip não promete nível; uma barra promete.

Os quatro que te vendem — e que estão bem posicionados no topo dos grupos — são **Suporte/troubleshooting 80, SQL/PostgreSQL 75, Documentação técnica 75 e Testes de API 70**. Note que três deles não são linguagem de programação. Isso não é fraqueza: é exatamente o perfil que falta em time júnior.

---

## 4. O currículo em PDF

Está comentado no HTML porque você ainda não tem. Faça — é a primeira coisa que pedem depois de gostar do site.

- Uma página. Duas só com experiência que justifique.
- Ao subir no Drive: botão direito → Compartilhar → **"Qualquer pessoa com o link"** → Leitor. Se esquecer disso, quem clicar vê tela de pedir permissão, e ninguém pede.
- Nome do arquivo com o seu nome: `raul-guilherme-curriculo.pdf`, não `cv_final_v3.pdf`.
- Quando tiver o link, descomente o bloco `CURRÍCULO EM PDF` no `index.html`, na seção de contato.

---

## 5. Coisas pequenas que mudam a impressão

- **Teste o formulário de verdade** depois de configurar o Formspree. Formulário quebrado em página de contato é pior que não ter formulário.
- **Abra no celular de verdade**, não só no simulador do navegador. Metade dos recrutadores abre link no celular.
- **Foto sua**: não tem no layout e não faz falta. Se quiser adicionar, ela cabe ao lado do texto do "sobre" — mas não é obrigatório e o site funciona melhor sem.
- **Google Analytics / contador de visita**: não coloque. Não vale o script externo, e você fez questão de zero dependência.

---

## 6. O que eu preciso que você confirme

Duas coisas na trajetória eu inferi e podem estar erradas:

1. **2024 = entrada em ADS.** Deduzi de "4º semestre": se o 4º semestre é agora (2026.1), o curso começou no segundo semestre de 2024. Se você entrou em outro ano, me diz.
2. **2026 = entrada na Supermídia.** Você só disse "situação atual". Se começou em 2025, o marco muda de ano.

E uma decisão de conteúdo, mais importante:

3. **2025 e 2026 estão escritos de forma sóbria.** Você escreveu em caixa alta: *"NINGUÉM JAMAIS NOVAMENTE TERÁ MEUS DADOS"* e *"NEM OS DA MINHA FAMÍLIA"*. Eu não coloquei essas frases literalmente e não inventei o que aconteceu, porque você não contou e eu não ia supor.

   O que está lá agora descreve o interesse por segurança sem afirmar nenhum episódio. Se houve um caso concreto — e a força do que você escreveu sugere que sim — ele pode virar a parte mais forte do site, porque explica de onde vem a sua motivação de um jeito que ninguém copia. Mas isso é decisão sua, e tem dois lados:

   - **A favor:** motivação verdadeira e específica é o que separa você de outro júnior. Entrevistador lembra.
   - **Contra:** é informação pessoal, num site público, indexado pelo Google, para sempre. E dependendo de como for escrito, pode expor sua família ou soar como desabafo em vez de trajetória profissional.

   Se quiser incluir, me conta o que aconteceu e eu escrevo em duas frases sóbrias, sem dramatizar e sem detalhe identificável. Se preferir deixar como está, também está resolvido — o site já comunica que segurança é o seu eixo.

---

## Ordem de prioridade

1. **Os três projetos** — sem isso o site não cumpre a função. É 90% do trabalho que falta.
2. **ID do Formspree** — 5 minutos, e sem isso o formulário não envia nada.
3. **Os quatro números** — 20 minutos com o Movidesk aberto.
4. **Currículo em PDF** e descomentar o link.
5. Decidir sobre a trajetória de 2025/2026.
6. Enxugar a stack, se concordar com o argumento da seção 3.
