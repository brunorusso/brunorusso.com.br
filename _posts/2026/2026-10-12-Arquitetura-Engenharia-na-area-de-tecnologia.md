---
title: "Migrating from elilo to Grub on Slackware current (16) with UEFI/EFIBoot"
author: "Bruno Russo"
date: 2026-10-12 22:50 +0300
categories: ["Arquitetura"]
tags: ["arquitetura", "governança", "Grub"]
ping: true
math: true
mermaid: true
image: 
    path: https://www.brunorusso.com.br/assets/2026/arquitetura_engenharia.jpeg
    alt: "The image shows the GRUB screen, customized for Slackware."
---


## Arquitetura & Engenharia na área de tecnologia

O que vou relatar nesse post é simplesmente uma opinão pessoal, baseada em artigos, conversas com líderes de várias empresas, outros arquitetos, amigos e etc.

Arquitetura e Engenharia, dois times atuando em conjunto para construir as melhores soluções para os clientes. Esse é o modelo que muitas empresas adotam para desenvolver e evoluir suas aplicações, sejam elas para uso interno ou para uso externo pelos seus clientes, por exemplo.

Antes de iniciar qualquer discussão, pois o assunto pode ser polêmico sob determinados pontos de vista, é importante termos as definições dessas duas áreas.

### Definição de Arquitetura e Engenharia

**Arquitetura**

A área de Arquitetura de Tecnologia é a disciplina responsável por projetar, estruturar e alinhar os componentes de tecnologia da informação (software, infraestrutura, dados e redes) aos objetivos estratégicos de um negócio. Ela define os padrões técnicos, regras de integração, diretrizes de segurança e a topologia de sistemas para garantir que os ambientes de TI sejam escaláveis, resilientes, seguros e eficientes do ponto de vista operacional e financeiro.

Martin Fowler, em seu artigo “Quem Precisa de um Arquiteto” (Fowler, 2003), compartilhou as ideias de Ralph Johnson sobre arquitetura. Na qual ressaltou: “ A arquitetura trata das coisas importantes. Sejam elas quais forem”.

Além desses pontos, acredito que tudo isso é cercado por uma palavra fundamental: **comunicação**, que abordo no fim do artigo. Em um excelente artigo [Ana Brenes](https://www.betterask.erni.ch/the-triple-a-saga-architecture-architects-and-agile-part-i/#:~:text=%E2%80%9C(1)%20A%20formal%20description%20of%20a%20system%2C,design%20and%20evolution%20over%20time%E2%80%9D%20(TOG%2C%202018)) aborda essa questão da comunicação, onde descreve a importância de "comunicar ...  às pessoas relevantes."

**Engenharia**

Engenharia de Software (ou a área de Engenharia de TI) é a aplicação de uma abordagem sistemática, disciplinada e quantificável ao desenvolvimento, operação e manutenção de sistemas de software.

O termo passou a ser amplamente adotado no mercado porque criar software em escala corporativa exige práticas muito semelhantes às da engenharia tradicional (civil, mecânica ou elétrica). Algumas práticas adotadas pela engenharia são:

1. **Ciclo de Vida Completo (SDLC):** Desde a concepção, levantamento de requisitos e análise de viabilidade, até a automação de testes, implantação (CI/CD), monitoramento em produção e eventual desativação (decommissioning);

2. **Garantia de Qualidade e Testes:** Definição de estratégias de testes automatizados (unitários, integração, regressão, carga e segurança) para evitar regressões e garantir previsibilidade;

3. **Manutenção e Evolução:** Preocupação contínua com a redução de débito técnico, refatoração e facilidade de sustentação por outros times.

4. **Métricas e Processos:** Uso de dados para medir eficiência e confiabilidade — como tempo de ciclo (lead time), frequência de implantação, taxa de falhas e tempo médio de recuperação (MTTR).


## Arquitetura & Engenharia: Como atuam na prática?

A distinção entre as duas áreas costuma ser entendida pela relação entre **o projeto (o que construir)** e **a construção (como construir e manter)**. Na tabela a seguir, podemos comparar, em alto nível, algumas diferenças entre as duas.

| Aspecto | Arquitetura de Tecnologia | Engenharia de Software / TI |
| --- | --- | --- |
| **Foco Principal** | Estrutura, padrões, viabilidade e alinhamento estratégico. | Implementação, construção, automação e operação eficiente. |
| **Escopo de Visão** | Visão macro/sistêmica (como os blocos e plataformas se conectam). | Visão micro/operacional (como os componentes internos são codificados e testados). |
| **Entregáveis Típicos** | Blueprints, diagramas C4, padrões técnicos, análises de trade-offs. | Código-fonte, pipelines de CI/CD, suítes de testes, artefatos implantáveis. |
| **Pergunta Fundamental** | *"Como esta solução deve ser desenhada para atender aos requisitos?"* | *"Como construímos, testamos e mantemos essa solução com máxima qualidade?"* |

Nas empresas modernas, as duas áreas atuam em cooperação contínua: os arquitetos definem as diretrizes e limites, enquanto a engenharia constrói e valida as soluções dentro dessas fronteiras. Pelo menos isso é o esperado.


### Bife no prato Vs Massa de pão

Ao analisar a tabela anterior, especificamente na primeira linha temos o **Foco Principal**. Observe que arquitetura tem como função definir: _estrutura_, _padrões_ etc etc. Já engenharia foca em _Implementação_.

> Entendo e concordo que quanto mais se analisa a necessidade de negócio e estrutura um plano, melhor será o resultado da construção de uma aplicação. Porém, convenhamos que no atual momento e com o uso massivo da inteligência artificial a tarefa da "codificação" em si, se tornou mais "rápida" para ser entregue, quando comparada à duas décadas atrás.

O que quero chamar a atenção sob esse aspecto é que a engenharia coloca "bife no prato", ou seja, disponibiliza o software para ser usado de forma rápida e prática. Já a arquitetura, faz o que eu defini como "massa de pão", onde a massa precisa ser sovada, precisa descansar para aí então ser modelada e ir para o forno. Logo, engenharia entrega algo pronto de forma rápida enquanto arquitetura demora demasiadamente para fazer uma entrega.

> Importante ressaltar que em nenhum momento estou julgando a qualidade do que é entregue. Estou apenas apresentando fatos.

Para ilustrar de uma outra maneira, o que quero dizer em relação a essa diferença, imagine o seguinte cenário.

**Cenário do cálculo simples**

Em um mesmo ambiente, analisando uma demanda estão um engenheiro e um arquiteto. Então, o seguinte problema é apresentado aos dois:

Considere a variável Valor-A com o valor de 1 e a variável Valor-B com valor de 1. Qual será o resultado da soma dessas duas variáveis?

O Engenheiro responde prontamente: **2**

O Arquiteto responde: **Depende**. E questiona se os valores de cada variável são números inteiros?

Pequena explicação sobre esse contexto:

**A resposta do Engenheiro é a estritamente correta** e a do Arquiteto é um excesso de **zelo**.

A explicação dividida pelas duas áreas:

Por que a resposta do Engenheiro está matematicamente correta?

Na matemática pura e na teoria dos números:

* O símbolo **1** representa a unidade dentro de um corpo numérico (seja nos números Naturais $\mathbb{N}$, Inteiros $\mathbb{Z}$, Racionais $\mathbb{Q}$ ou Reais $\mathbb{R}$).
* A operação de adição $+$ é uma função binária universalmente definida nesses conjuntos.
* Pela própria definição axiomática dos números (Axiomas de Peano), a soma de $1 + 1$ é **invariavelmente 2**, independentemente de o número ser classificado como inteiro, float ou complexo. $1.0 + 1.0$ continua sendo $2.0$.

**De onde vem a provocação da pergunta do Arquiteto?**

A dúvida do Arquiteto só faria sentido se estivéssemos lidando com **tipagem de dados em programação** ou **contexto do domínio do problema**, e não com matemática pura:

1. **Tipagem e Representação na Memória:**
* Se forem números inteiros: `1 + 1 = 2`.
* Se forem *strings* (texto): `"1" + "1"` resulta em `"11"` (concatenação).
* Se forem booleanos: `true + true` em C/C++ resulta em `2`, mas em lógica booleana ($1 \lor 1$) o resultado é $1$.
* Se for aritmética de ponto flutuante com precisão limitada, $1.0 + 1.0$ resulta em $2.0$, mas em casos de *overflow* ou conversões de tipo, o resultado armazenado pode mudar.


**A "Deformação Profissional" do Arquiteto:**

A piada retrata com precisão a mentalidade do Arquiteto: antes de aceitar uma premissa ou executar um cálculo, ele questiona as **fronteiras, o contexto, o tipo de dado e as restrições do sistema** (os requisitos não-funcionais).


**Resumo**

Matematicamente, **1 + 1 é 2** e não há ambiguidade. O Arquiteto tentou tratar um problema de **aritmética básica** como se fosse um problema de **modelagem de sistemas**, onde premissas não declaradas podem quebrar uma aplicação em produção.

> Obrigado ao Google Gemini, por me ajudar com a resposta acima.

Mas brincadeiras a parte, note que a preocupação do engenheiro é a de entrega e a do arquiteto é a de identificar pontos que não precisam ser discutidos. Logo, o arquiteto fica fazendo a "massa de pão" e o engenheiro coloca o "bife no prato".

Sob o aspecto de negócio, que sempre está com fome e precisa se saciar, é claro que o bife no prato é o que ele prefere, já que resolve o seu problema de forma imediata.


### O real valor entregue

Em um cenário ideal, esses dois papéis funcionam como um contrapeso necessário. Porém, quando mal calibrado (e esse é o grande problema), o comportamento de ambos traz riscos bem definidos para o negócio:

**A visão de entrega rápida (Foco na Engenharia)**

O motor da empresa é a execução/entrega de valor. Focar em resolver o problema imediato e colocar o valor na mão do cliente rapidamente traz retorno financeiro, valida hipóteses e mantém a empresa competitiva.

* **O valor:** Entregas rápidas (Time-to-Market), resolução prática de problemas e foco no resultado imediato.
* **O risco do excesso:** Se a engenharia focar *apenas* no curto prazo ignorando o contexto, constrói-se o que o mercado chama de "castelo de cartas". O sistema acumula **débito técnico** tão rápido que, em 1 ou 2 anos, qualquer nova alteração simples passa a demorar meses ou causa quedas em produção.

**A visão de sustentabilidade (Foco na Arquitetura)**

O papel da arquitetura é evitar que as decisões de hoje inviabilizem a empresa amanhã. No entanto, questionamentos sem pragmatismo e desconectados do momento do negócio geram o fenômeno conhecido como **Paralisia por Análise** (*Over-engineering*).

* **O valor:** Visão de médio/longo prazo, escalabilidade, segurança e garantia de que o custo de manutenção não vai explodir no futuro.
* **O risco do excesso:** Questionamentos desconectados da realidade imediata que travam entregas, gastam horas em reuniões conceituais e não geram valor real para o negócio no tempo necessário.

> É necessário ter um ponto de equilíbrio corporativo

Essa provocação que trouxe expõe uma falha comum em arquiteturas que atuam como "torre de marfim": **o arquiteto que questiona por questionar, sem pragmatismo**.

No contexto corporativo moderno, um bom arquiteto **não é aquele que impede a entrega rápida**, mas sim aquele que ajuda a engenharia a entregar rápido **com o menor risco possível**, deixando explícitos os *trade-offs* e para isso a comunicação é fundamental.

> A entrega de valor da Engenharia é **frequente e imediata**; o valor da Arquitetura é **cumulativo**, garantindo que a empresa continue conseguindo entregar rápido daqui a 2 ou 5 anos.


### Novo mindset da arquitetura

Vejo que uma das grandes dores que existem em tecnologia moderna é o descompasso entre a **velocidade da inovação na ponta** (engenharia) e a **capacidade de governança no centro** (arquitetura).

> Em meu ponto de vista, o grande problema está em querer governar depois que algo está pronto e entregue. Em muitos casos, quando tenta governar de forma antecipadamente, peca pelo excesso de ações burocráticas.

E a sensação é de que a arquitetura está "sempre um passo atrás" acontece principalmente quando a empresa adota um modelo arquitetural tradicional e principalmente reativo.

**Por que a Engenharia costuma trazer as novidades primeiro?**

1. **Proximidade com o problema real:** Os times de engenharia sentem a dor do dia a dia no código, na infraestrutura e na esteira de CI/CD. Quando uma ferramenta, framework ou serviço de nuvem novo surge para resolver exatamente essa dor, a engenharia é a primeira a testar e adotar.
2. **Pressão por velocidade:** Pressionada para entregar mais rápido, a engenharia busca atalhos tecnológicos.
3. **Volume e especialização:** É matematicamente impossível para um time central de arquitetura acompanhar cada biblioteca, ferramenta ou tendência que surge em dezenas de ecossistemas diferentes na mesma velocidade que centenas de engenheiros.

Se a arquitetura tenta atuar como um **"Pedágio"** (onde nada passa sem a aprovação prévia do arquiteto), ela vira um gargalo. A engenharia passa por cima, adota a novidade por fora (gerando em alguns casos o famoso e perigoso *Shadow IT*), e a arquitetura só descobre quando o problema já está em produção.


### O Papel da Arquitetura: Estar à frente não significa saber tudo antes

Estar "à frente" da engenharia não significa que o arquiteto precisa descobrir todas as ferramentas do mercado antes da engenharia. O papel da arquitetura para liderar o processo envolve mudar a forma como os padrões são criados:

1. Definir Guardrails (Trilhos), não Guardrails de Concreto (Paredes)

Em vez de ditar a ferramenta exata (*"vocês só podem usar o banco X na versão Y"*), a arquitetura define os **critérios de elegibilidade**:

* *"Qualquer tecnologia nova trazida pela engenharia precisa ter suporte a observabilidade, autenticação via SSO corporativo, ser compatível com a esteira de CI/CD e possuir análise de custo de execução."*
* Com isso, a engenharia tem autonomia para inovar, mas dentro de limites seguros preestabelecidos.

2. Arquitetura Evolutiva e "Paved Roads" (Estradas Pavimentadas)

A arquitetura cria o caminho padrão ("a estrada pavimentada") onde tudo é automatizado, documentado e fácil de usar.

3. Habilitadora, não Fiscalizadora (*Enablement*)

A arquitetura atua antecipadamente identificando **tendências estruturais do negócio** (ex: migração de nuvem, estratégia de dados, resiliência regulatória, controle de custos/FinOps) enquanto a engenharia foca na **inovação tática do produto**.

**A diferença entre Arquitetura Reativa e Proativa**

| Modelo | Arquitetura Reativa (Um passo atrás) | Arquitetura Proativa (À frente do negócio) |
| --- | --- | --- |
| **Atuação** | Descobre a novidade quando o problema estoura em produção. | Cria critérios e políticas claras de adoção antes da escolha. |
| **Posição** | Atua como fiscal de normas e "aprovador de requisição". | Atua como consultora técnica e curadora de padrões. |
| **Relacionamento** | Vista pela Engenharia como burocracia que atrasa entregas. | Vista pela Engenharia como parceira que destrava e protege o sistema. |
| **Foco** | Tentar controlar cada linha de código ou ferramenta. | Desenhar a estratégia macro de longo prazo da plataforma. |


Quando a arquitetura foca em **definir direcionadores estratégicos, arquitetura de referência e limites de segurança**, ela deixa de ser atropelada pelas novidades técnicas da engenharia e passa a guiá-las de forma sustentável.

A arquitetura proativa não passa a "fazer o bife" (pois a construção do software/feature continua sendo a entrega fim da Engenharia), mas sim **prepara a cozinha industrial, automatiza a grelha e deixa os cortes prontos** para que a Engenharia sirva o bife 10 vezes mais rápido e sem risco de contaminação. Isso reforça a ideia de que Arquitetura habilita a Engenharia a entregar valor imediato.


Porém, mesmo a arquitetura atuando de forma proativa ela não pode ter atuação passiva, ou seja, o padrão está definido e pronto! Isso continuará não trazendo nenhum benefício ao negócio.



### Mudando de patamar

Para dar um salto de maturidade e sair de modelos genéricos ou meramente operacionais, a **Arquitetura de Tecnologia Proativa** pode ser estruturada sobre alguns pilares e um deles que, quero abordar é o de **Gerenciamento de Riscos e Resiliência Técnica**



**Arquitetura Evolutiva e Gestão de Débito Técnico**

Sistemas corporativos sofrem degradação natural com o passar do tempo se não houver mecanismos para medir e controlar a obsolescência tecnológica.

* **Funções de Aptidão (*Fitness Functions*):** Testes automatizados executados na esteira de integração contínua para validar requisitos não-funcionais e regras arquiteturais. Se um módulo tentar acessar diretamente o banco de dados de outro serviço ou se uma dependência violar um acoplamento proibido, o build é interrompido.
* **Matriz de Obsolescência e Risco:** Mapeamento contínuo dos componentes de software, bibliotecas e serviços de infraestrutura em relação ao ciclo de vida (LTS, descontinuação de suporte pela comunidade ou provedor, vulnerabilidades CVEs).
* **Quota de Refatoração:** Pactuação institucional entre Arquitetura, Engenharia e Gestão de Produtos para alocar um percentual fixo da capacidade de desenvolvimento (ex: 15% a 20% das sprints) prioritariamente para redução de débito técnico e atualização de componentes estruturais.

---

## Comparativo de Maturidade da Arquitetura

| Dimensão | Nível 1: Passivo / Reativo | Nível 2: Padronizador / Normativo | Nível 3: Proativo / Habilitador |
| --- | --- | --- | --- |
| **Padrões Técnicos** | Documentados em arquivos PDF ou wikis isoladas. | Validados manualmente em comitês de arquitetura. | Embutidos automaticamente em templates e pipelines de CI/CD. |
| **Gargalo de Aprovação** | Exige revisão humana para qualquer alteração técnica. | Exige aprovação para novos componentes de infraestrutura. | *Guardrails* automatizados dão autonomia total dentro dos limites. |
| **Gestão de Custos** | Análise pontual da fatura de nuvem após o vencimento. | Ações reativas para cortes de gastos quando o orçamento estoura. | *Cost-Driven Architecture* com visibilidade de custos em tempo de código. |
| **Relação com a Engenharia** | Vista como área fiscalizadora que atrasa entregas. | Vista como área consultiva acionada esporadicamente. | Provedora de plataforma que acelera a produtividade dos times. |


### E a Comunicação?

A comunicação na arquitetura não é sobre preencher formulários, planilhas de excel e/ou fazer apresentações bonitas. Trata-se de traduzir a complexidade técnica para diferentes contextos e linguagens.

> Se você atua com arquitetura e apenas faz apresentações bonitas, cuidado! Isso não é um bom sinal.

O arquiteto que não se comunica bem acaba caindo em um dos dois extremos: ou vira o "arquiteto de marfim" incompreendido e que todos ignoram, ou vira o "fiscal burocrata" que todos tentam desviar.

Por isso saber se comunicar com todos os níveis que existem na empresa é fundamental. Veja os seguintes exemplos de comunicação:

- **Com a Engenharia**: Falar a linguagem de quem está no código. Não adianta ditar regras em um PDF de 50 páginas; a comunicação aqui precisa ser pragmática, pautada em trade-offs transparentes, ouvindo as dores do time e transformando diretrizes em automação (a "cozinha pronta" que mencionamos).

- **Com a Gestão de Produto (POs/PMs)**: Explicar o impacto de um débito técnico em termos de velocidade futura. O produto quer colocar o "bife no prato" hoje, mas o arquiteto precisa comunicar com clareza: "Se não dedicarmos 15% da sprint para refatoração agora, no próximo trimestre a entrega de novas funcionalidades vai demorar o dobro do tempo". - Para esse item, virou algo muito comum criar [ADR](https://brunorusso.com.br/posts/ADR-a-chave-para-documentacoes-ageis-e-eficientes-de-arquitetura/). O problema é que o ADR se transformou em mais um "formulário" para ser preenchido, perdendo o seu real valor.

- **Com a Liderança e Negócio (C-Level/Diretoria)**: Traduzir decisões técnicas em linguagem financeira e de risco. O executivo não quer saber se o banco de dados é NoSQL ou Relacional; ele precisa entender se a solução escala em períodos críticos como Black Friday, por exemplo, se atende às exigências regulatórias (como LGPD) e qual será o impacto financeiro para o negócio.


### Pequena conclusão

Em última análise, tecnologia é feita por e para pessoas. Padrões, paved roads e matrizes de risco só geram impacto real quando acompanhados de escuta ativa e pragmatismo. Quando a arquitetura deixa de ser um pedágio burocrático e passa a atuar como habilitadora da engenharia, o negócio ganha o melhor dos dois mundos: a velocidade imediata que o mercado exige com a sustentabilidade técnica que o futuro precisa.
