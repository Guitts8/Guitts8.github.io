# Paletas para testar

Cinco opções, todas com contraste **verificado** pela fórmula da WCAG — nenhuma reprova em AA (mínimo 4.5:1 para texto).

## Como testar

No `index.html`, o topo do CSS tem dois blocos: `:root { ... }` (tema escuro) e `:root[data-theme="light"] { ... }` (tema claro). Substitua **as oito linhas de cor** de cada um pelo bloco correspondente abaixo e recarregue a página. Não mexa em mais nada — nenhum outro lugar do arquivo tem hexadecimal.

Guarde o bloco que estiver usando antes de trocar, para conseguir voltar.

---

## 1. Ciano sobre preto-azul — *a atual*

Rede, terminal, infra. É a mais neutra das cinco e a que menos disputa atenção com o avatar.

```css
/* escuro */
  --bg:       #070A0F;
  --bg-alt:   #0B1018;
  --surface:  #101822;
  --line:     #1E2A38;
  --text:     #E9EFF7;
  --muted:    #8B9AAD;
  --accent:   #4FD6FF;
  --accent-2: #1B6FA8;

/* claro */
  --bg:       #F2F5F8;
  --bg-alt:   #E5EBF2;
  --surface:  #FFFFFF;
  --line:     #CBD6E2;
  --text:     #0B1017;
  --muted:    #4E5A68;
  --accent:   #0A5E86;
  --accent-2: #1B6FA8;
```

Pior par: 5.86:1

---

## 2. Âmbar de terminal

Monitor âmbar de CRT antigo. A mais quente e a mais adulta do conjunto — combina com operação, log e plantão. Também é a mais distante da referência da Lohane.

Cuidado: âmbar é cor de alerta em ferramenta de monitoramento. Numa página inteira ela perde esse sentido, mas se você usar em cartão de projeto pode sugerir "atenção" sem querer.

```css
/* escuro */
  --bg:       #0A0908;
  --bg-alt:   #100E0B;
  --surface:  #16130F;
  --line:     #2E2820;
  --text:     #F2EDE4;
  --muted:    #A2978A;
  --accent:   #FFB13D;
  --accent-2: #A8541A;

/* claro */
  --bg:       #F8F5F0;
  --bg-alt:   #EFEAE0;
  --surface:  #FFFFFF;
  --line:     #DDD5C8;
  --text:     #14110C;
  --muted:    #5C5347;
  --accent:   #8A5200;
  --accent-2: #A8541A;
```

Pior par: 5.33:1

---

## 3. Vermelho Berserk

**A que mais conversa com o seu avatar.** O personagem tem botas vermelhas e o símbolo da Marca do Sacrifício no notebook — são os dois únicos pontos de cor saturada no desenho. Uma paleta vermelha faz o site inteiro parecer desenhado em volta dele, em vez de o avatar parecer colado depois.

O argumento contra: vermelho é a cor de erro em toda interface que existe. Numa página de segurança isso pode ler como tema, ou pode ler como alarme. Vale ver no monitor antes de decidir.

```css
/* escuro */
  --bg:       #0B0708;
  --bg-alt:   #120C0D;
  --surface:  #191111;
  --line:     #33201F;
  --text:     #F5EAEA;
  --muted:    #A89090;
  --accent:   #FF5A5A;
  --accent-2: #8C1C1C;

/* claro */
  --bg:       #F8F3F3;
  --bg-alt:   #EFE6E6;
  --surface:  #FFFFFF;
  --line:     #DCC9C9;
  --text:     #150E0E;
  --muted:    #5E4C4C;
  --accent:   #A81616;
  --accent-2: #8C1C1C;
```

Pior par: 6.07:1 — é a de melhor contraste das cinco.

---

## 4. Violeta cyber

A mais "cibersegurança" no sentido visual que o mercado adotou. Distinta, moderna, e nenhum outro portfólio júnior da sua região vai estar usando.

Contra: é a menos associada a back-end e infra. Comunica mais "hacker" que "quem sustenta o sistema".

```css
/* escuro */
  --bg:       #09070F;
  --bg-alt:   #0E0B18;
  --surface:  #150F22;
  --line:     #2A2140;
  --text:     #EDE9F7;
  --muted:    #9A90B5;
  --accent:   #B98CFF;
  --accent-2: #5B2FA8;

/* claro */
  --bg:       #F5F3FA;
  --bg-alt:   #EBE7F4;
  --surface:  #FFFFFF;
  --line:     #D3CCE6;
  --text:     #100C1A;
  --muted:    #554C6B;
  --accent:   #6A2CB8;
  --accent-2: #5B2FA8;
```

Pior par: 6.26:1

---

## 5. Verde de terminal

Verde de fósforo, console antigo. Direta, sem sutileza.

Contra, e é sério: é o clichê mais gasto de segurança da informação. Todo mundo que quer parecer hacker usa verde em fundo preto. Se você usar, o site precisa ser bom o bastante para a pessoa passar da primeira impressão — e o seu é, mas você começa devendo.

```css
/* escuro */
  --bg:       #050A07;
  --bg-alt:   #0A110C;
  --surface:  #0F1811;
  --line:     #1E3024;
  --text:     #E7F5EB;
  --muted:    #8CAD97;
  --accent:   #3DFF9E;
  --accent-2: #0F7A45;

/* claro */
  --bg:       #F1F7F3;
  --bg-alt:   #E4EEE8;
  --surface:  #FFFFFF;
  --line:     #C8DCD0;
  --text:     #08130C;
  --muted:    #47604F;
  --accent:   #0A6B3C;
  --accent-2: #0F7A45;
```

Pior par: 5.56:1

---

## Se você inventar a sua

Duas regras que as cinco acima seguem:

1. **O fundo nunca é preto puro.** Todos têm pigmento da cor do acento (`#070A0F` é preto com azul, `#0B0708` é preto com vermelho). Preto puro `#000000` com uma cor saturada em cima vibra e cansa a vista.

2. **O acento do tema claro não é o mesmo do escuro.** Cor neon existe para fundo escuro; sobre branco ela dá 1.5:1 e some. No tema claro o acento é sempre a mesma cor puxada para baixo até passar AA.

Depois de trocar, refaça a conta em <https://webaim.org/resources/contrastchecker/> — precisa dar no mínimo 4.5:1 para: texto/fundo, apagado/fundo, acento/fundo, e fundo sobre acento (que é o botão cheio).
