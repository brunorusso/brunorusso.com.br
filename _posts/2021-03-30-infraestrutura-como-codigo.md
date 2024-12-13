---
title: Infraestrutura como código
author: Bruno Russo
date: 2021-03-30 20:20 +03:00
categories: [Blogging, governança]
tags: [iac, infraestrutura, cloud]
---

## Infraestrutura como código

Qual ferramenta você utiliza para provisionar sua infraestrutura? Se a resposta for a criação de uma solicitação no sistema de atendimento, você está ultrapassado!

Neste momento você deve estar querendo se contradizer: "mas eu preciso ter controle".

Que controle? Um Ticket, o número de uma solicitação? Não é com um número que você terá o controle que deseja.

Atualmente a grande maioria das soluções permitem o seu uso através de API. E o uso de APIs, possibilita a criação de inúmeras automações. Por exemplo, você pode: criar uma regra em um firewall, configurar um load balancer, criar um repositório no Github ou no gitlab, entre muitas outras coisas.

Porém, com a grande adoção da computação em nuvem, a utilização de códigos para provisionar a infraestrutura, vem cada vez mais sendo popular. É isso é muito bom!

Atualmente, existem algumas ferramentas que podem ser usadas na automação da infraestrutura. São elas:

1. Ansible
2. Terraform
3. Chef
4. Puppet
5. AWS  Cloudformation
6. Azure Resource Manager
7. Google Cloud Deployment Manager

Nenhuma solução acima é mágica e vai atender 100% às suas necessidades. Porém, a junção de pelo menos duas pode te ajudar a resolver grande parte dos seus problemas.

Usar 3 soluções podem resolver 100% dos problemas? Não, pelo menos na minha opinião. Pois o uso de muitas soluções gera um outro "custo" que é a gestão das ferramentas.

As soluções 5, 6 e 7 são dedicadas aos seus provedores e acabam não sendo soluções agnosticas. Adoro essa palavra...

Atualmente a solução que tem mais se destacado no mercado é o terraform. A linguagem utilizada no terraform é muito intuitiva e declarativa, ou seja, com pequenas instruções você consegue criar seu recurso.

Além da facilidade no uso, o terraform possui integração com diversas soluções, como por exemplo:

- AWS
- Azure
- GCP
- VMware
- Kubernetes
- Oracle cloud
- Cisco ASA
- Github
- Datadog
- IBM Cloud
- e diversos outros
