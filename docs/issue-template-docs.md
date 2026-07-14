<img src="https://orbesoft.com.br/logo.svg" alt="Descrição" width="86" height="24" />

<p align="center">
 <a href="#objetivo">Objetivo</a> •
 <a href="#board">Board</a> •
 <a href="#hierarquia-do-board">Hierarquia</a> •
 <a href="#colunas-do-board">Colunas</a> •
 <a href="#regras-de-movimentacao">Regras de movimentação</a> •
 <a href="#tipos-de-template">Tipos de template</a> • 
 <a href="#task">Task</a> • 
 <a href="#macro">Macro</a> • 
 <a href="#module">Module</a> • 
 <a href="#componentes">Componentes</a> • 
 <a href="#boas-praticas">Boas práticas</a> • 
 <a href="#referencias">Referências</a>
</p>

<h2 id="objetivo">📝 Objetivo</h2>

Esta documentação tem como objetivo orientar novos usuários na utilização do board da empresa, apresentando a organização das issues, sua hierarquia, o significado de cada coluna e as regras de movimentação durante o fluxo de trabalho.

Também são apresentados os templates de issues disponíveis e um conjunto de componentes em Markdown que podem ser reutilizados para padronizar a criação, a documentação e o acompanhamento das demandas.

<h2 id="board">🗃️ Board</h2>

O board representa o fluxo de trabalho dos projetos e permite acompanhar o estado atual de cada demanda. Cada coluna possui uma finalidade específica e deve refletir a situação real da issue.

Manter o board atualizado é responsabilidade de todos os envolvidos no fluxo. Uma issue posicionada incorretamente pode prejudicar a priorização, a revisão, a homologação e o planejamento das entregas.

<h3 id="hierarquia-do-board">🌳 1. Hierarquia do board</h3>

As issues do board são organizadas em três níveis:

```text
Projeto
└── Módulo
    └── Tarefa
```

#### Projeto

O projeto é representado por uma issue do tipo [**Macro**](#macro).

* É a issue principal da hierarquia.
* Deve permanecer na coluna [`Macros`](#macros).
* Centraliza o contexto geral, a documentação e o design do projeto.
* Deve possuir um ou mais [módulos](#module) associados.

#### Módulo

O módulo é representado por uma issue do tipo [**Module**](#module).

* É uma sub-issue da [Macro](#macro) correspondente.
* Representa uma área, funcionalidade ou parte específica do projeto.
* Deve ser vinculado à Macro por meio do campo **Parent issue**.
* Entra inicialmente na coluna [`Backlog`](#backlog).
* Deve possuir uma ou mais [tarefas](#task) associadas.

#### Tarefa

A tarefa é representada por uma issue do tipo [**Task**](#task).

* É uma sub-issue do [módulo](#module) correspondente.
* Deve ser vinculada ao módulo por meio do campo **Parent issue**.
* Representa uma unidade de trabalho que será desenvolvida, revisada, homologada e entregue.
* É o tipo de issue que percorre as etapas operacionais do board.

> Todo projeto deve possuir [módulos](#module) e toda [tarefa](#task) que percorre o board deve pertencer a um módulo.

<h3 id="colunas-do-board">📊 2. Colunas do board</h3>

<h4 id="todo"><code>Todo</code></h4>

Contém as [tarefas](#task) que estão na fila para serem desenvolvidas.

Para que uma tarefa seja movida para esta coluna, ela deve possuir um contexto mínimo que permita o início do trabalho, incluindo:

* Descrição do que precisa ser feito.
* Requisitos ou regras de negócio.
* Critérios de aceitação.
* Referências necessárias.
* [Módulo](#module) pai corretamente vinculado.

O [template de Task](#task) possui os campos necessários para registrar essas informações.

Uma tarefa em `Todo` está disponível para ser iniciada, mas ainda não está sendo executada.

---

<h4 id="in-progress"><code>In Progress</code></h4>

Contém as [tarefas](#task) que estão em andamento.

Isso inclui tarefas que:

* Estão sendo desenvolvidas.
* Estão sendo investigadas.
* Estão sendo iteradas junto a um agente.

Antes de retirar uma tarefa desta coluna, é necessário:

1. Preencher o checklist de entrega.
2. Publicar o checklist preenchido no Google Drive.
3. Referenciar o documento do Google Drive no card da tarefa.
4. Garantir que os critérios de aceitação aplicáveis tenham sido atendidos.
5. Adicionar as referências ou evidências necessárias para a próxima etapa.

---

<h4 id="to-review"><code>To Review</code></h4>

Contém as [tarefas](#task) que estão prontas para serem revisadas.

Uma tarefa nesta coluna deve possuir todas as informações necessárias para que outra pessoa consiga validar a entrega sem depender de explicações adicionais.

Quando a tarefa exigir revisão direta:

* A implementação deve estar pronta para análise.
* As instruções necessárias para executar ou testar a entrega devem estar disponíveis.
* O checklist de entrega deve estar referenciado no card.

Quando a tarefa não exigir uma revisão direta:

* Deve existir, no mínimo, um vídeo de evidência vinculado à tarefa.
* O vídeo deve demonstrar claramente o resultado da implementação.
* A evidência deve contemplar os principais critérios de aceitação.

A movimentação para `To Review` indica que o responsável pelo desenvolvimento considera a tarefa concluída e pronta para validação.

---

<h4 id="in-review"><code>In Review</code></h4>

Contém as [tarefas](#task) que estão sendo revisadas.

A tarefa é movida de [`To Review`](#to-review) para `In Review` pelo responsável pela revisão, indicando que a análise foi iniciada.

Durante esta etapa, o responsável pela revisão deve verificar:

* Se os requisitos foram atendidos.
* Se os critérios de aceitação foram cumpridos.
* Se a solução apresenta o comportamento esperado.
* Se existem problemas, efeitos colaterais ou cenários não considerados.
* Se o checklist e as evidências estão disponíveis no card.

Após a aprovação, a tarefa pode seguir para a próxima etapa aplicável do fluxo.

---

<h4 id="homolog"><code>Homolog</code></h4>

Contém as [tarefas](#task) que estão em homologação e serão testadas pelo cliente.

Uma tarefa deve entrar nesta coluna quando:

* A revisão interna estiver concluída.
* A entrega estiver disponível no ambiente de homologação.
* O cliente precisar validar o comportamento ou o resultado da implementação.

As instruções de teste, acessos necessários, limitações conhecidas e demais informações relevantes devem estar registradas ou referenciadas no card.

---

<h4 id="ready"><code>Ready</code></h4>

Contém as [tarefas](#task) que estão prontas para serem publicadas em produção, mas que precisam aguardar alguma condição.

Exemplos:

* A entrega depende de outra tarefa que ainda está em [`Homolog`](#homolog).
* A publicação precisa acontecer em um horário específico.
* A publicação depende de uma autorização.
* A tarefa precisa ser publicada junto com outras entregas.
* Existe alguma dependência técnica ou operacional pendente.

O motivo da espera deve estar claramente registrado no card.

Quando a condição for atendida, a tarefa pode ser publicada em produção e movida para [`Done`](#done).

---

<h4 id="done"><code>Done</code></h4>

Contém as [tarefas](#task) que já estão em produção.

Uma tarefa somente deve ser movida para esta coluna quando:

* A entrega tiver sido efetivamente publicada em produção.
* A publicação tiver sido verificada.
* Não existirem ações obrigatórias pendentes relacionadas à entrega.

Mover uma tarefa para `Done` significa que seu fluxo de desenvolvimento e entrega foi concluído.

---

<h4 id="macros"><code>Macros</code></h4>

Contém as issues que representam os projetos.

As issues desta coluna:

* Devem utilizar o [template de **Macro**](#macro).
* São as issues principais da [hierarquia do board](#hierarquia-do-board).
* Centralizam a visão geral do projeto.
* Devem conter [módulos](#module) como sub-issues.
* Não percorrem o fluxo operacional das [tarefas](#task).

---

<h4 id="backlog"><code>Backlog</code></h4>

Contém [tarefas](#task) ou [módulos](#module) que podem ser desenvolvidos futuramente, mas que ainda não estão suficientemente definidos ou priorizados.

Esta coluna permite registrar demandas que:

* Ainda precisam de refinamento.
* Não possuem contexto suficiente para serem iniciadas.
* Ainda não foram priorizadas.
* Podem ser executadas em algum momento.
* Não devem ser perdidas de vista.

Uma tarefa deve sair do `Backlog` e ser movida para [`Todo`](#todo) quando possuir contexto mínimo e estiver disponível para desenvolvimento.

O `Backlog` não deve ser utilizado como destino para tarefas abandonadas. Caso uma demanda não seja mais necessária, essa decisão deve ser registrada claramente na issue.

<h3 id="regras-de-movimentacao">🚦 3. Regras de movimentação</h3>

| Origem                        | Destino                       | Condição esperada                                                                          |
| ----------------------------- | ----------------------------- | ------------------------------------------------------------------------------------------ |
| [`Backlog`](#backlog)         | [`Todo`](#todo)               | A tarefa possui contexto mínimo e está disponível para desenvolvimento.                    |
| [`Todo`](#todo)               | [`In Progress`](#in-progress) | O trabalho foi efetivamente iniciado.                                                      |
| [`In Progress`](#in-progress) | [`To Review`](#to-review)     | A implementação foi concluída, o checklist foi publicado e as evidências foram vinculadas. |
| [`To Review`](#to-review)     | [`In Review`](#in-review)     | O responsável pela revisão iniciou a análise.                                              |
| [`In Review`](#in-review)     | [`Homolog`](#homolog)         | A revisão interna foi aprovada e a entrega precisa ser validada pelo cliente.              |
| [`Homolog`](#homolog)         | [`In Progress`](#in-progress) | Foram solicitados ajustes durante a homologação.                                           |
| [`Homolog`](#homolog)         | [`Ready`](#ready)             | A homologação foi aprovada, mas existe uma condição que impede a publicação imediata.      |
| [`Homolog`](#homolog)         | [`Done`](#done)               | A homologação foi aprovada, a entrega foi publicada e verificada em produção.              |
| [`Ready`](#ready)             | [`Done`](#done)               | A condição de espera foi atendida e a entrega foi publicada e verificada em produção.      |

> As movimentações devem refletir acontecimentos reais. Não mova uma tarefa antecipadamente apenas para organizar visualmente o board.

Consulte também as [boas práticas](#boas-praticas) para criação e atualização das issues.

<h2 id="tipos-de-template">🔖 Tipos de template</h2>
Esta seção apresenta os diferentes templates de issues que suportaremos no [board](#board). Cada tipo de template é adaptado a um fluxo de trabalho específico.

<h3 id="task">📋 1. Task</h3>

O template de **task** é destinado a demandas de desenvolvimento e novas funcionalidades. Ele oferece campos claros para descrever o escopo da tarefa, requisitos funcionais e critérios de aceitação, garantindo que o time tenha tudo o que precisa para estimar, implementar e validar a entrega com eficiência.

As Tasks percorrem as colunas operacionais do [board](#board) e devem estar vinculadas a um [módulo](#module).

```markdown
<img src="https://orbesoft.com.br/logo.svg" alt="Descrição" width="86" height="24" />

## 📝 Descrição

<!-- Descreva claramente o que precisa ser feito ou qual é o problema/sugestão. -->

## 🎯 Requisitos

<!-- Liste os requisitos específicos desta solicitação (funcionalidades, restrições, regras de negócio). -->

## ✅ Critérios de Aceitação

<!-- Defina como saberemos se a solicitação foi corretamente implementada (testes, comportamento esperado, etc.). -->

## 🔗 Referências

<!-- Adicione links, documentos, ou prints que possam ajudar a entender o contexto. -->
```

<h3 id="macro">🗂️ 2. Macro</h3>

O template de **macro** é destinado à visão geral de um projeto. Agrupa [modules](#module) e centraliza documentação, design e contexto macro. Fica na coluna [`Macros`](#macros) do [board](#board).

```markdown
<img src="https://orbesoft.com.br/logo.svg" alt="Descrição" width="86" height="24" />

## 📝 Descrição

<!-- Visão geral do projeto: contexto, público-alvo e escopo. -->

## 📂 Docs

<!-- Links do Drive com documentação do projeto (briefing, requisitos, envs, credenciais, etc.). -->

## 🎨 Figma

<!-- Link do Figma do projeto. -->

## 🔗 Referências

<!-- Materiais complementares que não estão no Drive nem no Figma (issues relacionadas, APIs, threads, inspirações). -->
```

<h3 id="module">🧩 3. Module</h3>

O template de **module** é destinado a uma área específica dentro de uma [macro](#macro). Descreve escopo, docs e design do módulo. Entra em [`Backlog`](#backlog) e é vinculada à macro pai via Parent issue.

```markdown
<img src="https://orbesoft.com.br/logo.svg" alt="Descrição" width="86" height="24" />

## 📝 Descrição

<!-- Escopo específico deste módulo dentro do projeto. -->

## 📂 Docs

<!-- Links do Drive com documentação deste módulo (specs, envs, credenciais, etc.). -->

## 🎨 Figma

<!-- Link do Figma deste módulo. -->

## 🔗 Referências

<!-- Materiais complementares que não estão no Drive nem no Figma (issues relacionadas, APIs, threads, inspirações). -->
```

<h2 id="componentes">🧩 Componentes</h2>
Esta seção reune blocos de Markdown que podem ser copiados e colados em suas issues para padronizar a formatação, acelerar a criação e garantir consistência.

### 🔠 1. Títulos

Use títulos para estruturar suas issues em seções hierarquizadas, facilitando a leitura e o entendimento.

```markdown
# Título H1

## Título H2

### Título H3
```

### 📑 2. Listas

Liste itens de forma ordenada ou não ordenada para descrever etapas, requisitos ou agrupamentos.

```markdown
1. First item
2. Second item
3. Third item
```

```markdown
- First item
- Second item
- Third item
```

```markdown
- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media
```

### 📏 3. Tabela

Apresente informações tabulares de forma clara, comparando campos, tipos e descrições.

```markdown
| Coluna A | Coluna B |
| -------- | -------- |
| Dado 1   | Dado 2   |
```

<h2 id="boas-praticas">Boas práticas</h2>

1. **Forneça o máximo de detalhes possíveis**: inclua exemplos concretos, dados de entrada/saída, cenários de uso e contexto completo para que qualquer membro do time entenda sem precisar de esclarecimentos adicionais.
2. **Separe contexto e solução**: detalhe o “por quê” da demanda e o “como” da abordagem para facilitar priorização e execução.
3. **Matenha o status atualizado**: mova a issue no [board](#board) conforme avança ([To Do](#todo) → [In Progress](#in-progress) → [To Review](#to-review)).

<h2 id="referencias">🔗 Referências</h2>

**[The Markdown Guide](https://www.markdownguide.org/)**
