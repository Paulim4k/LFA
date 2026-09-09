# Lista de Exercícios — Autômatos Finitos Determinísticos (AFD)

> **Disciplina:** Teoria das Linguagens e Autômatos  
> **Tema:** Autômatos Finitos Determinísticos  
> **Modalidade:** Atividade prática em grupo  
> **Objetivo:** identificar, interpretar, construir e testar AFDs.

---

## Identificação do grupo

| Campo | Preenchimento |
|---|---|
| Turma | |
| Data | |
| Integrante 1 | |
| Integrante 2 | |
| Integrante 3 | |
| Integrante 4 | |

## Orientações

- Registre o raciocínio utilizado em cada resposta.
- Nos exercícios com cadeias, apresente o caminho percorrido estado por estado.
- Nos exercícios de construção, entregue a quíntupla, a tabela de transição e o diagrama.
- Use `ε` para representar a cadeia vazia.
- Quando solicitado, implemente e teste o autômato no JFLAP.

---

# Parte 1 — Fundamentos

## Exercício 1 — Entendendo um autômato finito

Uma lâmpada controlada por um interruptor possui os estados `Desligado` e `Ligado`. Sempre que o botão é pressionado, ocorre a mudança:

```text
Desligado --pressionar--> Ligado
Ligado    --pressionar--> Desligado
```

Responda:

1. Quantos estados existem?
`R:2 estados (Desligado e Ligado).`

2. Qual é o estado inicial, considerando que a lâmpada começa apagada?
`R: 2 estados (Desligado e Ligado).`

3. Qual entrada provoca uma transição?
`R: Desligado.`

4. Partindo de `Desligado`, qual será o estado após um acionamento?
`R: A entrada "pressionar".`

5. Partindo de `Desligado`, qual será o estado após dois acionamentos?
`R: Ligado.`

6. Explique o funcionamento do sistema com suas palavras.
`R: Desligado.`

## Exercício 2 — Porta automática

Uma porta automática possui os estados `Fechado` e `Aberto`. O sensor identifica `pessoa_detectada` ou `nenhuma_pessoa`. Quando uma pessoa é detectada, a porta deve ficar aberta; quando ninguém é detectado, deve ficar fechada.

Complete a tabela:

| Estado atual | Entrada     | Próximo estado |
|---|---|---|
| Fechado | pessoa_detectada | `R: Aberto`    |
| Fechado | nenhuma_pessoa   | `R: Fechado`   |
| Aberto | pessoa_detectada  | `R: Aberto`    |
| Aberto | nenhuma_pessoa    | `R: Fechado `  |

Depois, desenhe o diagrama de estados correspondente e indique o estado inicial.
`R: O estado inicial é Fechado. O diagrama possui transições direcionadas entre Fechado e Aberto conforme as condições do sensor descritas na tabela acima.`

---

# Parte 2 — Anatomia e definição formal

## Exercício 3 — Identificando os elementos

Considere um AFD com `Σ = {0,1}`, `Q = {q0,q1}`, estado inicial `q0`, estado final `q1` e as transições abaixo:

| δ | 0 | 1 |
|---|---|---|
| q0 | q0 | q1 |
| q1 | q0 | q1 |

Identifique e explique:

1. o alfabeto `Σ`;
`R: Σ = {0,1}, conjunto de símbolos permitidos para leitura.`

2. o conjunto de estados `Q`;
`R: Q = {q0, q1}, conjunto finito de estados possíveis do autômato.`

3. o estado inicial;
`R: q0, o ponto de partida do processamento de qualquer cadeia.`
4. o conjunto de estados finais `F`;
`R: F = {q1}, estados que aceitam a cadeia ao final da leitura.`
5. os símbolos que podem ser lidos;
`R: Os símbolos 0 e 1 definidos no alfabeto.`

6. o significado do círculo duplo em um diagrama;
`R: Representa um estado de aceitação (final).`

7. o significado da seta sem origem apontando para um estado.
`R: Indica qual é o estado inicial do autômato.`

## Exercício 4 — A quíntupla do AFD

Um AFD é formalmente representado por:

```text
M = (Σ, Q, δ, q0, F)
```

Complete:

| Elemento | Significado |
|---|---|
| `Σ` | `R: Alfabeto de entrada (conjunto finito de símbolos).` |
| `Q` | `R: Conjunto finito de estados.`                   |
| `δ` | `R: Função de transição (mapeia Q × Σ para Q).`    |
| `q0` |`R: Estado inicial (pertencente a Q).`             |
| `F` |` R: Conjunto de estados de aceitação (subconjunto de Q).`|

Explique por que esses cinco elementos são suficientes para definir o funcionamento de um AFD.
`R: Eles determinam de forma unívoca o vocabulário suportado, a estrutura de controle por estados, as regras estritas de transição determinística, o ponto de partida e a condição de sucesso/aceitação.`
---

# Parte 3 — Tabela de transições e cadeias

## Exercício 5 — Interpretando uma tabela

Considere `Σ = {0,1}`, `Q = {q0,q1,q2}`, estado inicial `q0`, `F = {q1}` e:

| δ | 0 | 1 |
|---|---|---|
| q0 | q0 | q1 |
| q1 | q2 | q1 |
| q2 | q1 | q1 |

Responda:

1. Qual é o resultado de `δ(q0,0)`?
`R: q0`

2. Qual é o resultado de `δ(q0,1)`?
`R: q1`

3. Qual é o resultado de `δ(q1,0)`?
`R: q2`

4. Qual é o resultado de `δ(q2,1)`?
`R: q1`
5. Qual é o estado de aceitação?
`R: q1`
6. Desenhe o diagrama correspondente à tabela.
`R: q0 vai para q0 (com 0) e q1 (com 1); q1 vai para q2 (com 0) e q1 (com 1); q2 vai para q1 (com 0 e com 1)`

7. Justifique por que o autômato é determinístico.
`R: Porque para cada estado e para cada símbolo do alfabeto existe exatamente uma única transição de saída definida.`

## Exercício 6 — Aceita ou rejeita?

Utilize o AFD do Exercício 5. Determine se cada cadeia é aceita ou rejeitada:

```text
a) 1
b) 0011001
c) 010010
d) 1101
e) 000011010
```

Para cada cadeia, registre todas as transições. Exemplo:

```text
Cadeia: 01
q0 --0--> q0
q0 --1--> q1
Estado final: q1
Resultado: ACEITA
```

| Cadeia | Caminho percorrido | Estado final | Resultado |
|---|---|---|---|
| `1`    |`R: q0          `   |  `1`         |   `q1`    |
| `0011001` | | | |
| `010010` | | | |
| `1101` | | | |
| `000011010` | | | |

---

# Parte 4 — Construção de AFDs

## Exercício 7 — Cadeias que terminam em `1`

Construa um AFD sobre `Σ = {0,1}` que reconheça todas as cadeias que terminam em `1`.

- Devem ser aceitas: `1`, `01`, `101`, `0001`, `1101`.
- Devem ser rejeitadas: `ε`, `0`, `10`, `100`, `1110`.

Entregue: conjunto de estados, alfabeto, estado inicial, estados finais, tabela, diagrama e teste de pelo menos cinco cadeias.

## Exercício 8 — Número par de símbolos `1`

Construa um AFD sobre `Σ = {0,1}` que reconheça cadeias com quantidade par de símbolos `1`.

Analise: `ε`, `0`, `1`, `11`, `101`, `1100` e `10101`.

Apresente a definição formal `M = (Σ, Q, δ, q0, F)`, a tabela, o diagrama e o processamento das cadeias. Lembre-se de que basta controlar duas situações: quantidade par ou ímpar de símbolos `1`.

## Exercício 9 — Pelo menos dois zeros consecutivos

Construa um AFD para:

```text
L(M) = {w ∈ {0,1}* | w possui pelo menos dois 0s consecutivos}
```

- Devem ser aceitas: `00`, `001`, `100`, `1001`, `110011`, `0000`.
- Devem ser rejeitadas: `ε`, `0`, `1`, `01`, `10`, `10101`.

Responda antes de construir:

1. O que o estado inicial representa?
`R: Nenhum zero lido recentemente.`

2. O que ocorre quando aparece o primeiro `0`?
`R: O autômato transiciona para um estado intermediário que memoriza a leitura de um zero.`

3. O que ocorre quando outro `0` aparece imediatamente depois?
`R: O autômato transiciona para o estado de aceitação definitivo.`

4. Depois de encontrar `00`, a cadeia pode deixar de ser aceita?
`R: Não, pois o estado final absorve quaisquer símbolos subsequentes.`

5. Quantos estados são necessários?
`R: 3 estados.` 

Apresente a quíntupla, a tabela, o diagrama e os testes.

---

# Parte 5 — Desafios de modelagem

## Exercício 10 — Semáforo

Modele um semáforo com os estados `Verde`, `Amarelo` e `Vermelho`. Use a entrada `tempo` e represente o ciclo:

```text
Verde → Amarelo → Vermelho → Verde
```

Entregue o diagrama, a tabela de transições, a definição formal e uma explicação do funcionamento. Discuta se há sentido em definir estados de aceitação nesse modelo e justifique a escolha adotada.

## Exercício 11 — Sistema de login

Modele um sistema com as entradas `senha_correta` e `senha_incorreta`. Uma senha correta autentica o usuário; após três tentativas incorretas, o sistema fica bloqueado.

Determine:

1. todos os estados necessários para contar as tentativas;
`R: Aguardando, Erro1, Erro2, Autenticado, Bloqueado.`

2. o alfabeto de entrada;
`R: Σ = {senha_correta, senha_incorreta}`

3. o estado inicial;
`R: Aguardando`

4. os estados finais;
`R: F = {Autenticado}`

5. todas as transições;
`R: Transições direcionadas controlando falhas sequenciais até o bloqueio ou sucesso imediato.`

6. o comportamento após a autenticação e após o bloqueio.
`R: Estados absorventes onde novas tentativas não alteram o estado final atingido.`

Responda: apenas os estados `Aguardando`, `Autenticado` e `Bloqueado` são suficientes para controlar três tentativas? Justifique e construa o AFD completo.
`R: Não, pois são necessários estados intermediários para registrar o histórico e a contagem exata das falhas antes de atingir o limite de três tentativas.`

---

# Parte 6 — Prática no JFLAP

## Exercício 12 — Implementação e testes

Escolha um dos AFDs dos exercícios 7, 8 ou 9 e implemente-o no JFLAP.

1. Crie os estados.
2. Defina o estado inicial e os estados finais.
3. Crie todas as transições.
4. Teste três cadeias que devem ser aceitas.
5. Teste três cadeias que devem ser rejeitadas.
6. Compare os resultados esperados e obtidos.

Inclua um print do AFD, a tabela de testes e uma breve explicação.

| Cadeia | Resultado esperado | Resultado no JFLAP | Conferência |
|---|---|---|---|
|`1`    |`Aceita`  | `Aceita`  | |
|`01`   | `Aceita` | `Aceita`  | |
|`101`  |`Aceita`  | `Aceita`  | |
|`0`    |`Rejeita` |`Rejeita`  | |
|`10`   | `Rejeita`| `Rejeita` | |
| `1110`| `Rejeita`|  `Rejeita`| |

---

# Desafio final

## Exercício 13 — Crie seu próprio problema

Escolha uma situação real representável por estados, como elevador, máquina de vendas, controle de acesso, estacionamento, pedido de delivery, semáforo, porta eletrônica ou protocolo de comunicação.

O grupo deverá:

1. descrever o problema e suas regras;
`R: Sistema de catraca de acesso que libera a passagem mediante cartão válido e trava após o usuário passar.`

2. identificar as entradas e os estados;
`R: Entradas: {cartao_valido, passagem_catraca}. Estados: {Bloqueada, Liberada}`

3. definir o estado inicial e os estados finais;
`R: Estado inicial: Bloqueada. Estado final: F = {Bloqueada}`

4. criar a tabela de transições;


5. desenhar o AFD;
`R: Diagrama com setas direcionadas entre os estados Bloqueada e Liberada conforme a tabela.`

6. apresentar `M = (Σ, Q, δ, q0, F)`;
`R: M = ({cartao_valido, passagem_catraca}, {Bloqueada, Liberada}, δ, Bloqueada, {Bloqueada}).`

7. testar pelo menos cinco sequências de entrada;
`R: 1) cartao_valido (Rejeita) | 2) cartao_valido, passagem_catraca (Aceita) | 3) passagem_catraca (Aceita) | 4) cartao_valido, cartao_valido, passagem_catraca (Aceita) | 5) cartao_valido, passagem_catraca, passagem_catraca (Aceita).`

8. explicar por que o modelo é determinístico;
`R: Porque cada estado possui exatamente uma única transição definida para cada símbolo de entrada, sem ambiguidades.`

9. apresentar uma conclusão sobre o que foi aprendido.
`R: O exercício consolidou a aplicação prática de AFDs na modelagem de sistemas de controle físico.`

---

# Entregável

O grupo deverá entregar um único arquivo `README.md`, contendo:

- identificação do grupo;
- respostas dos exercícios indicados pela professora;
- diagramas e tabelas de transição;
- processamento estado por estado das cadeias;
- evidência dos testes no JFLAP;
- conclusão do grupo.

## Modelo para o desafio final

```markdown
## Desafio final

### Problema escolhido

### Estados e significado

### Alfabeto

### Estado inicial e estados finais

### Tabela de transições

### Diagrama

### Definição formal
M = (Σ, Q, δ, q0, F)

### Testes realizados
| Entrada | Resultado esperado | Resultado obtido |
|---|---|---|
| | | |

### Evidência no JFLAP

### Conclusão
```

> **Importante:** não basta apresentar o diagrama. Demonstre como o AFD processa cada cadeia, estado por estado, até decidir pela aceitação ou rejeição.

---

**Profa. Kadidja Valéria**
