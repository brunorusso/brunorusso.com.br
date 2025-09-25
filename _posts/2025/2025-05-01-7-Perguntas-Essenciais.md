---
title: "Como Entender Demandas de Negócio sob o olhar da Tecnologia com 7 Perguntas Essenciais"
author: "Bruno Russo"
date: 2025-05-01 21:30 +0300
categories: ["Cloud", "Gestão", "Arquitetura"]
tags: ["Transformação Digital", "Arquitetura", "Conhecimento", "dicas"]
ping: true
math: true
mermaid: true
image: 
    path: https://www.brunorusso.com.br/assets/2025/7-Perguntas-Essenciais.jpg
    alt: "A imagem é uma ilustração digital vibrante com um tema tecnológico, projetada para promover um artigo sobre 7 perguntas para alinhar tecnologia e negócios. O fundo apresenta um gradiente de azul e roxo, criando uma estética futurista e high-tech. Há linhas finas e curvas suaves ao fundo, que lembram fluxos de dados ou circuitos digitais, adicionando um toque de dinamismo.
No centro da imagem, há um homem de pele clara, quase careca (com cabelo muito curto), usando óculos de armação preta. Ele está sorrindo e parece confiante. Sua roupa é casual: uma camisa polo azul, calça jeans azul e tênis brancos. Ele está em pé sobre uma plataforma circular que tem um leve brilho, sugerindo um ambiente tecnológico avançado. Suas mãos estão nos bolsos, transmitindo uma postura relaxada. Ao redor do homem, flutuam sete caixas de diálogo retangulares com bordas arredondadas e um leve brilho translúcido, como se fossem hologramas. Cada caixa contém um ícone e uma palavra que representam as sete perguntas mencionadas no artigo. As caixas estão posicionadas em um círculo ao redor do homem, algumas mais à esquerda, outras à direita, e algumas acima ou abaixo dele."
---

## Introdução

Quando se trata de alinhar tecnologia às necessidades de um negócio, a **clareza é tudo**. Muitas vezes, projetos falham porque as expectativas não foram bem definidas ou os requisitos técnicos não foram mapeados corretamente.

Para evitar isso, desenvolvi uma abordagem com 7 perguntas-chave que ajudam a compreender qualquer demanda sob a ótica da tecnologia. Essas perguntas não só identificam o problema e os requisitos, mas também garantem que aspectos como disponibilidade, segurança, escalabilidade e custo sejam considerados. Neste post, compartilho essa metodologia e explico como aplicá-la para transformar demandas em soluções eficazes.


## 7 Perguntas
 
**1. Qual problema você está tentando resolver?**

Toda solução tecnológica começa com um problema (que pode ser de negócio, de produto ou mesmo algo novo que está sendo criado) claro. Essa pergunta é o ponto de partida para entender o que o negócio precisa. Por exemplo, é uma questão de lentidão no sistema? Perda de clientes por falhas? Ou a necessidade de lançar um novo produto?

> Dica prática: Vá além e pergunte: “Quais são os principais gargalos ou pontos de dor que você enfrenta hoje?” Isso ajuda a capturar nuances que podem não ser mencionadas inicialmente e que são extremamentes importantes.


**2. Quais aspectos específicos da aplicação requerem níveis de disponibilidade específicos?**

Nem todas as partes de uma aplicação precisam de 100% de uptime. Identificar quais funcionalidades são críticas (ex.: checkout de um e-commerce) e quais podem tolerar pequenas interrupções é essencial para dimensionar a infraestrutura.

> Dica prática: Considere sazonalidades e pergunte: “Existem picos de uso, como Black Friday ou fins de mês, que exigem maior disponibilidade?” Isso antecipa cenários de alta demanda.


**3. Qual a indisponibilidade total que a aplicação pode acumular durante um ano?**

Essa pergunta traduz a tolerância do negócio em métricas técnicas, como 99,9% de uptime (é cerca de 8,76 horas de indisponibilidade por ano). Ela é crucial para definir SLAs (Service Level Agreements) e planejar redundâncias.

> Dica prática: Complemente questionando: “Qual é o tempo máximo aceitável para recuperação após uma falha (RTO) e quanta perda de dados é tolerável (RPO)?” Isso orienta estratégias de backup e recuperação.


**4. Qual o impacto atual da indisponibilidade?**

Entender o impacto — financeiro, operacional ou reputacional — ajuda a justificar investimentos em tecnologia. Por exemplo, uma hora de downtime em um sistema de vendas pode custar milhares de reais ou afastar clientes.

> Dica prática: Pergunte: “Como a indisponibilidade afeta os usuários finais ou a percepção da marca?” Isso captura impactos indiretos, como churn ou perda de confiança.


**5. Quais são os riscos de segurança associados à aplicação?**

**Segurança é inegociável**. Identificar riscos, como vazamento de dados, ataques DDoS ou falhas de compliance, é essencial para proteger o negócio e seus clientes.

> Dica prática: Mapeie os dados sensíveis envolvidos (ex.: informações de pagamento) e pergunte: “Quais regulamentações, como LGPD ou GDPR, a aplicação precisa atender?” Isso garante conformidade desde o início.


**6. Qual é o crescimento esperado de usuários ou transações nos próximos anos?**

Escalabilidade é sobre "prever" o futuro. Uma solução que funciona hoje pode colapsar com o crescimento do negócio. Entender as projeções de uso ajuda a escolher tecnologias que acompanhem a expansão.

> Dica prática: Pergunte: “Você planeja expandir para novos mercados ou lançar novos produtos?” Isso revela necessidades de escalabilidade horizontal ou vertical.


**7. Qual é o orçamento disponível para atingir os níveis de disponibilidade desejados?**

Tecnologia de ponta tem um custo, e o equilíbrio entre custo e benefício é crucial. Essa pergunta alinha expectativas financeiras com os requisitos técnicos, evitando soluções inviáveis.

> Dica prática: Explore opções de custo variável, como computação em nuvem, e pergunte: “Você prefere investir mais agora para reduzir custos operacionais no futuro?” Isso ajuda a balancear CapEx e OpEx.


## Aplicando essas perguntas na prática

- **Reúna os stakeholders:** Inclua representantes do negócio, TI e usuários finais para capturar diferentes perspectivas; 
- **Documente as respostas:** Use um template ou ferramenta de gestão (ex.: Notion, Jira) para organizar as informações;
- **Traduza para requisitos técnicos:** Converta as respostas em especificações, como arquitetura, SLAs e planos de mitigação de riscos;
- **Valide com o cliente:** Apresente um resumo para garantir alinhamento antes de iniciar o projeto.


## Por que essa abordagem funciona?

Essas 7 perguntas cobrem os pilares de um projeto tecnológico bem-sucedido: clareza do problema, disponibilidade, impacto, segurança, escalabilidade e viabilidade financeira. Elas são inspiradas em frameworks como o Well-Architected da AWS, mas simplificadas para serem práticas e universais. Ao usá-las, você não apenas entende a demanda, mas também constrói uma base sólida para entregar valor ao negócio.


## Conclusão

Compreender uma demanda tecnológica é como montar um quebra-cabeça: cada pergunta revela uma peça essencial. Ao usar essa abordagem de 7 perguntas, você garante que a solução seja alinhada, segura, escalável e financeiramente viável.
