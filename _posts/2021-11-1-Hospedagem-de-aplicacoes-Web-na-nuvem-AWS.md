---
title: Hospedagem de aplicacoes Web na nuvem AWS
author: Bruno Russo
date: 2021-11-01 15:00 0300
categories: [Cloud, AWS, Governança, Gestão]
tags: [AWS, Cloud, Web, Arquitetura]
layout: post
type: post
---

## Introdução

Para muitas empresas, o primeiro workload é uma aplicação web, composta por uma camada de segurança, balanceadores de carga, servidores de front-end e back-end, banco de dados e por fim uma camada de segurança e governança em relação aos dados, como backup por exemplo.

Este workload é bem simples e muito comum. Porém, quando tudo isso precisa ser feito em um ambiente on premisse, alguns itens podem ser bem mais difíceis de serem implementados, seja por custos, conhecimento ou até mesmo prazo de entrega da solução.

Um outro ponto que torna manter um ambiente desse em um ambiente on premise são os custos operacionais e o de hardware ocioso. Na grande maioria das vezes o hardware é subutilizado, e isso é investimento perdido.

Ao utlizar AWS, há uma eficiência entre custos (investimentos) e a disponibilidade da aplicação, com maior resiliência, disponibilidade, confiabildade e segurança.

Assim que a decisão do uso da Cloud AWS é entendida como a melhor escolha, a primeira atividade que precisa ser feita é a definição de uma arquitetura adequada.

![Move to Cloud](https://brunorusso.com.br/assets/2021/move-to-cloud.png "Imagem oficial: https://www.cloudflare.com/pt-br/learning/cloud/what-is-cloud-migration/")

## Como definir a arquitetura adequada?

Esta pergunta não é tão simples de ser respondida. 

Atualmente, com inúmeras tecnologias e com a alta demanda de negócios por evolução de seus serviços, uma aplicação sofre inúmeras alterações durante o seu ciclo de vida. O mesmo acontece com sua arquitetura (aplicação e infraestrutura).

Dessa forma, afirmar que a arquitetura adequada está criada, é verdadeiro por apenas um período de tempo. Assim que um novo requisito de negócio ou técnico foi inserido ou alterado, a arquitetura adequada pode não ser mais válida e com isso uma nova precisa ser desenvolvida.

Além dos requisitos técnicos, de negócio e funcionais existem alguns pontos que precisam ser levados em consideração para definir a arquitetura mais adequada. Vejamos alguns deles:

1. Qual problema você está tentando resolver?
2. Quais aspectos específicos da aplicação requerem níveis de disponibilidades específicos?
3. Qual a Indisponibilidade total que a aplicação pode acumular durante um ano?
4. Qual o atual impacto da Indisponibilidade?

Em posse dessas informações e dos requisitos é possível começar a criar a arquitetura. 

As arquiteturas podem ser complexas ou mesmo simples. Tudo vai depender das respostas para as perguntas certas.

Com a alta demanda pelo consumo das aplicações, algumas arquiteturas precisam contemplar uma solução escalonável para lidar com picos de tráfego inesperados e até mesmo uma solução sob demanda para ambientes de desenvolvimento, teste de carga, homologação e produção.

## Importantes considerações para hospedagem de uma aplicação

Existem muitas diferenças entre uma hospedagem tradicional (on premise) e uma hospedagem em cloud pública. Vejamos algumas:

- Sem dispositivos de rede (Firewall, balanceadores, switches etc)
- Firewalls em todas as camadas (sendo componentes lógicos, o seu uso se torna mais fácil)
- A arquitetura deve considerar a utilização de vários data centers (Zonas de disponibilidade)
- Os servidores precisam ser considerados dinâmicos e efêmeros (servidoes não são um ativo. As informações precisam estar armazenadas em locais corretos e não dentro de servidores)
- Considere o uso de serviços serverless e contêineres
- Crie esteiras automatizadas para deploy de aplicação


## Notas finais

Este post, foi escrito com base no Whitepaper **Web Application Hosting in the AWS Cloud** que pode ser lido na íntegra em: https://docs.aws.amazon.com/whitepapers/latest/web-application-hosting-best-practices/welcome.html
