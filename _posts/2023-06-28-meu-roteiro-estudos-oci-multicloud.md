---
title: Meu roteiro de estudos para Oracle Cloud Foundation e MultiCloud Architect Certified Associate
author: Bruno Russo
date: 2023-06-28 14:00 0300
categories: [Aprendizado, OCI, Cloud, treinamento, Arquitetura ]
tags: [Aprendizado, Conhecimento, Oracle, OCI, Arquitetura, Certificação, Cloud]
layout: post
type: post
---

## Desafio 

Se você trabalha com tecnologia, aprender algo novo é sempre bom!

E pensando dessa forma, me desafiei em aprender um pouco mais de Oracle Cloud (OCI). O desafio era conseguir pelo menos uma certificação OCI em 2 meses, pois entraria de férias e não queria parar os estudos no meio para curtir às férias e depois voltar a estudar. Além disso, também precisava ganhar conhecimento o mais rápido possível em OCI.

## Treinamentos 

Dessa forma, analisei os treinamentos que a Oracle havia disponibilizado ano passado e eu ainda não tinha realizado.

Revendo os treinamentos que tenho disponíveis, realizei os seguintes treinamentos:

- **Oracle Cloud Overview** - [https://mylearn.oracle.com/ou/learning-path/oracle-cloud-overview/115954](https://mylearn.oracle.com/ou/learning-path/oracle-cloud-overview/115954): This Learning Path introduces you to Cloud Computing and Oracle's Cloud Solutions which include Oracle Cloud Infrastructure and Oracle Cloud Applications;
- **Oracle Cloud Infrastructure 2023 Certified Foundations Associate** - [https://mylearn.oracle.com/ou/learning-path/become-an-oci-foundations-associate-2023/122043](https://mylearn.oracle.com/ou/learning-path/become-an-oci-foundations-associate-2023/122043): This Learning Path provides the foundational knowledge of Oracle Cloud Infrastructure Cloud Services, and prepares you for the Oracle Cloud Infrastructure Foundations Associate Certification;
- **Oracle Cloud Infrastructure 2023 Multicloud Architect Certified Associate** - [https://mylearn.oracle.com/ou/learning-path/become-an-oci-multicloud-architect-associate/120606](https://mylearn.oracle.com/ou/learning-path/become-an-oci-multicloud-architect-associate/120606): This Learning Path provides strong foundational knowledge in architecting infrastructure using Oracle Cloud Infrastructure services and prepares you for the Oracle Cloud Infrastructure Multicloud Architect Associate Certification.

O primeiro treinamento é introdutório ao universo Oracle Cloud, além de conhecer alguns itens básicos também compreenderá como Oracle Cloud Infraestrutura funciona e quais as ofertas de serviços Oracle Cloud Applications. Ao término do estudo você pode responder um questionário para avaliar o conhecimento.

Já com o segundo treinamento, é possível conhecer um pouco mais os serviços que Oracle Cloud Infrastructure oferece e quais são os cenários para uso dos principais recursos. É um treinamento de Foundations.

O terceiro treinamento, é um pouco mais avançado que o treinamento de foundations, porém é extremamente focado em MultiCloud. É preciso ter um conhecimento básico de Cloud para realizar este treinamento, caso contrário terá dificuldade em alguns termos e serviços que são apresentados.

Ao todo o investimendo foi cerca de 30 horas de estudos, entre vídeos do treinamento, testes, simulados, anotações e leitura da documentação oficial do OCI - [https://docs.oracle.com/en-us/iaas/Content/home.htm](https://docs.oracle.com/en-us/iaas/Content/home.htm)
 
Além dos treinamentos oficiais, também realizei os simulados Oracle Cloud Infrastructure 2023 Multicloud Architect Associate disponibilizados pela Maitreyee - [https://www.udemy.com/user/maitreyee-panda-2/](https://www.udemy.com/user/maitreyee-panda-2/)

Com a dedicação e o tempo investido, consegui obter às certificações:
- Certificação - Oracle Cloud Infrastructure 2023 Foundations Associate
- Certificação - Oracle Cloud Infrastructure 2023 Multicloud Architect Associate

## O que aprendi?

- Os treinamentos me propirciaram conhecimento em:
- Compreensão dos conceitos básicos de nuvem; 
- Familiaridade com os principais serviços OCI: Computação, Armazenamento, Redes, Base de Dados;
- Capacidade de explicar o modelo de identidade e segurança OCI e a estrutura de conformidade; 
- Compreensão sobre o faturamento OCI;
- Gestão de custos e governança e administração;
- Entendimento de multicloud e seus benefícios;
- Descrever as opções de conectividade OCI Multicloud;
- Implementar Interconexão OCI-Azure;
- Implementar o Oracle Database Service para Azure.

Para saber mais sobre Oracle Cloud MultiCloud, visite esse link: [https://docs.oracle.com/en-us/iaas/Content/multicloud/intro.htm](https://docs.oracle.com/en-us/iaas/Content/multicloud/intro.htm)


## Badges

![OCI Associate Multicloud](https://www.brunorusso.com.br/assets/OCI-associate-multicloud.png)

![OCI Associate Foundation](https://www.brunorusso.com.br/assets/OCI-associate-foundation.png)


## Guia dos meus estudos

Abaixo compartilho o conteúdo das minhas anotações que fiz durante o período de estudos.

**Benefícios de Multi Cloud**
- redundância
- redução de custos
- Integração com Azure
- < 2ms de latência

**Conexão é feita entre Azure express route com OCI fast connect**
- não há custo de data transfer (in/out)
- Casos de Uso
    - Banco no OCI, APP no Azure - Conexão via Fast Connect e Express Route
    - Banco no OCI, APP na AWS - Conexão via Fast Connect + fast connect de parceiros + AWS Direct Connect
    - Banco no OCI, APP no Google - Conexão via Fast Connect + fast connect de parceiros + Google Interconnect
- SaaS - onde existe uma aplicação SaaS, banco de dados Oracle OCI e uma outra aplicação consumindo esse - banco de dados em outro provedor (Azure, AWS, Google)
- Benefícios desse modelo são:
- baixa latência
- alta performance
- alto throughput
- Arquitetura split stack

**IAM**
- controle de acessos é granular
- Autenticação e autorização
- Conceitos do Identity
- Identity Domain: contêm a relação dos usuários e grupos
- Users: usuários
- Groups: conjunto de usuários que possuem mesmo  tipo de acesso
- Principals: pode ser usuários e recursos do principal
- Dynamic Groups
- Policies: autorização para algo
- Compartment: coleção  de recursos relacionados
- Resource: recurso/objeto da cloud
- Federation: provedor de identidade
- Network resources: grupo de IP usado em policy para permitir ou não o acesso a partir de determinadas redes
- Policy, sempre permite algo, nunca nega.
- O padrão de segurança adotado é sempre o de menor privilégio
- Se não permitir, então está negado!

**Policy**
- Permite (allow)
- Quem (subject)
- recurso (verb)
- local (compartment)
- where
- condição

**Tipos de Identity Domain**
- Padrão que é gratuito
- Oracle Apps, usado para Oracle PaaS, SaaS e GBU App
- Oracle Apps Premium, usado em uma mescla dois modelos acima
- Premium, fornece full control e um suporte mais amplo
- External User, para usuários externos e com suporte a uma escala de milhões de usuários

**Federação**
- Identity Provider (gestão dos usuários)
- Service Provider, que usa o IdP para autenticar
- Suporte SAML 2.0
- Conceitos:
    - Federation trust
    - SAML
    - Metadata URL

**Federado**
- A autenticação ocorre em 5 etapas
- Usuário acessa recurso no Service Provider
- Service Provider retorna o pedido de autenticação
- Usuário faz a autenticação no AD (Identity Provider)
- ID valida a autenticação
- Usuário acessa a aplicação/recurso

**VCN**
- VCN é por região
- Conexão  entre VCN é realizado por Peering
- Cada VCN pode ter mais de um CIDR
- Não usar o mesmo CIDR em mais de uma VCN, pode ter problemas com peering
- Range da VCN deve fazer parte da RFC 1918, range permitido entre /16 e /30
- VCN reserva 3 IPs
- IPV4 é mandatório
- pode ter até 5 prefixos de IPV6
- A diferença da subnet pública e privada é uma flag

**VCN subnet**
- máximo de 300 subnets por VCN
- subnet pública:
    - é internet-facing
    - tem conexão com a Internet
Subnet:
    - é regional
    - disponível em specific domain (AZs) o que é bom para HA e DR
    - A subnet pode ser alterada
- vNIC (Virtual Network Interface Card), determina como a instância se conecta com endpoint interno/externo da VCN.

**VCN Security**
- Security list
    - é um firewall
    - quando cria uma VCN, automaticamente é criada uma security list
    - as regras são aplicadas em ordem
    - as regras são associadas com subnets, com isso afetam recursos criados dentro destas subnets
    - Padrão é negar tudo
    - limite de 5 security list por subnet
    - statefull security rules é configurada no momento da regra, ou seja, você define se a regra é ou não stateful. Desta forma, o tráfego Ingress terá um egress habilitando o mesmo
    - Stateless, precisa criar uma regra de egress para o retorno da requisição.
    - bom para ser usado com Load Balancer, Big Data
    - ICMP, precisa de regras de egress criada para funcionar

**Network Security Groups**
- regras aplicadas para cada recurso de forma individual
- máximo de 5 NSG por vNIC
- pode ser usado em mais  de um recurso

**VCN Peering**
- local peering
- na mesma região
- não pode ter overlap de IP
- Em cada VCN é preciso ter um Local Peering Gateway
- A conexão é feita no Local Peering Gateway
- Precisa estabelecer as rotas
- precisa estabelecer regras de firewall liberando acesso
- remote peering
- entre regiões
- usa o Dynamic Routing Gateway em cada região para estabelecer as conexões
- Usa o backbone da Oracle para estabelecer a conexão entre as regiões 

**VCN Gateway**
- Internet Gateway - entrada/saída para Internet
- Nat Gateway - saída para internet
- Service Gateway  - permite conexão com outros serviços OCI via rede privada
- Local peering gateway - conecta com outra VNC na mesma região
- Dynamic Routing Gateway:
    - Conecta com outra VNC em outra região
    - Conecta com ambiente on-premise via Fast-Connect
    - é standalone da VNC, não fica atrelado a VNC, diferente dos outros gateways
- Service Gateway
    - é regional
    - permite acesso a outros recursos da OCI
    - pode ser usado para acessar recursos na OCI a partir do ambiente on premise, via Fast Connect ou VPN
- Nat Gateway
    - Permite acesso à Internet para recursos que estiverem na subnet privada.
    - Suporta TCP/UDP/ICMP
    - Suporta até 20000 conexões concorrentes para o mesmo  destino
    - IP público pode ser reservada ou dinâmico
    - 1 NAT por VCN. Se for necessário mais pode solicitar
    - não pode ser usado para acessar Internet via peering
- Internet Gateway
    - Roteador para acessar à Internet
    - Suporta Ingress/Egress
    - Usado para fornecer IP público aos recursos
    - Para proteção, precisa de regras de segurança
    - não pode ser usado em zonas seguras
- VCN Routing
    - semelhante a uma tabela de rotas
    - atua como roteador entre subnets
    - se tiver rotas com overlapping, vai usar a regra mais específica
    - sem rota para a Internet, o resultado é  DROP
    - Suporta IPV6
- Dynamic Routing Gateway
    - usado em diversos cenários
    - Gateway dinâmico usado em  diversos tipos de conexões remotas
- Peering entre VCN entre regiões
    - Conectar mais  de uma VCN para fazer conexão inter VCN
    - Usado para estabelecer políticas de roteamento entre VCN
    - Usado nas conexões via Fast Connect, VPN site-to-site (IPSEC)
    - pode ser usado em  até 300 conexões
    - A configuração  é simplificada, por exemplo: ao estabelecer uma conexão VPN,a tabela de roteamento  já é criada de forma  automática
    - HA é padrão, você configura 1, porém um outro já fica em standby para ser usado caso uma falha  aconteça
    - suporta transitive routing
    - On-premise -> Conta A
    - Conta A -> Conta B
    - On-premise  acessar conta  B

**MULTICLOUD CONNECTIVITY**
- Site-to-site VPS
- Internet Pública
- múltiplos túneis IPsec
- Banda e latência podem variar
- Fast Connect
- conexão dedicada
- banda e latência fixa
- Suporte peering privada e pública (quando ter parceiros)
- Site to site VPN
    - serviço gratuíto
    - Casos de uso:
        - PoC
        - Conexão de escritórios  remotos
        - Conexão com outra cloud
        - Redundância do fast connect
    - Para conectar usa:
        - IKEV1/v2
        - Dynamic Routing Gateway
        - No cliente, gateway do cliente
        - IPsec conexão
        - Suporte BGP
    - Suporta roteamento dinâmico
    - Padrão de VPN é IPSec
    - Alguns vendors são suportados

**MultiCloud Site to site VPN**
- Existem documentações prontas para cada provider de nuvem
- Fast Connect
- conexão são de 1Gb/10Gb/100Gb
- Suporta link aggregation
- Virtual Circuit
- é uma camada de rede isolada
- roda uma ou mais redes físicas fornecendo local único de conexão entre o DRG e o CPE composto por e partes
    - Cliente
    - OCI
- Provider
    - O cliente pode ter vários circuitos para:
    - isolar tráfegos entre serviços
    - ter redundância
- Usa BGP para roteamento
- Suporta IPV6
- BGP para IPV6
    - prefixos suportados: /64, /96, /126, /127

**OCI-Azure**
- Conexão cross-cloud
- A conexão é direta, não tem provedor de telecom
- Aplicações multicloud
- conexão privada com latência inferior a 2ms
- fornece SSO único para recursos criados no OCI e no Azure
- OCI-Azure Setup
- Usa BGP
- como é uma conexão redundante, precisa de e BGPs
- dois blocos de rede são necessários, com subnet /28 e /31
- Etapas para conexão:
    - OCI - DataBases
- Oracle Base Database Service
- Single VM ou 2-node RAC
- Cloud automation under customer control, fornece:
    - provisionamento
    - patch
    - backup
    - DR
    - 4 tipos de licenças
        - Standard edition
            - Multi tenant databases
            - suporta até 3 databases
        - Enterprise edition extreme performance
            - DB in memory
            - Data Guard
            - RAC
            - Application Continuity
        - Enterprise edition high performance
            - Partition e Multi Tenant
            - Compressão avançada
            - Segurança avançada
            - ciclo de vida e pack cloud management
        - Enterprise edition
            - Data guard
            - RAC
            - Masking e subset Data
            - Tunning Pack e digest Pack
        - Standard Edition 2
            - TDE (Transparent Data Encryption)
            - Multi tenant 3PDB
            - Machine Learning
            - Spatial e Graph
    - Roda todas as versões do Oracle suportadas
    - Benefícios
        - rápido provisionamento
        - HA com 2 nodes
            - domain
            - fault domain

**Arquitetura de Storage para DB**
- LVM e Block Storage
- ASM usa Data e Recovering disk group
- Block fornece tríplice armazenamento de dados
- ASM a redundância é definida para externa
- Suporta clone do SystemDB

**Automação e ciclo de vida**
- ferramentas que podem ser usadas: Interface WEB, API, SDK, CLI e terraform
- Ações
    - Scale OCPU
    - Scale storage
    - Habilitação DataGuard
    - updateDB e systemDB
    - Backup e restore

**HA e DR**
- RAC
    - Isola contra falha
    - mesma região
    - usa 2 fault domain
- Data Guard
    - usa vários domínios
    - pode ser usado entre regiões
    - usado para DR

**Autonomous Database**
- Usa Linux customizado
- otimizado
- patchs automáticos
- sem down time
- Suporta vários tipos  de bancos de dados
    - data warehouse
    - transacional
    - documentos
- todo o provisionamento é automatizado
- configuração automatizada
- criptografia automática
- Tipos de bancos de dados
    - Autonomous transaction processing
        - modelo transacional
    - Autonomous data warehouse
        - Analítico
        - transformação de dados
    - Autonomous Json Database
        - NoSQL
    - Autonomous Database with APEX
        - para aplicações low  code
- Tipos de deploy
    - Shared
        - Oracle suporta a infraestrutura
        - Cliente gerencia o banc de dados
    - Dedicado
        - hardware do exadata é exclusivo
        - permite maior customização, por  exemplo update de versão, tempo  de retenção dos dados  de backup, etc

**Exadata Database Service**
- Solução  Exatada na OCI
- Oferece
    - RAC
    - In-memory
    - Oracle multi-tunnel
- Dedicado
    - Oracle gerencia a infra
    - cliente gerencia VM e DB
- Autonomous
    - 100% gerenciado pela Oracle
- Pode rodar no OCI ou Cloud@Customer
- Possibilidade de scalling OCPU
    - up/down
    - online
    - OCPU (paga somente a infraestrutura)
    - scalling vertical
- Para usar precisa de subscription
- License Included pricing
    - workload
    - paga pelo uso
- BYOL
    - bom para quem já tem licença
    - Inclui: TDE, data safe, oracle ML e packs de gerenciamento

**MySQL Database Service**
- 100% gerenciado
- service  native
- mais seguro
- maior confiabilidade
- automático: patch,  backup, segurança e HA
- Para provisionar:
    - escolhe  o shape (OCPU e memória)
    - Versão 8.0 ou acima
    - VCN
    - tipo de storage
- O acesso é através de um endpoint criado
- read réplicas pode ser usado com LB
- Backup é full ou incremental (point in time)
- Para migrar precisa usar uma ferramenta da oracle
    - dumpX
    - loadDump

**MySQL HA**
- Suportado nas versões 8.0.24 ou superiores
- pode  ser configurado no setup ou posteriormente
- Node primário é R/W
- node secundário (cópia assíncrona)
- usa múltiplos AV ou FD
- usa o grupo de réplica nativa MySQL
- toda a replicação ocorre via rede interna da Oracle
- Requisito: todas as tabelas precisam ter Primary Key
- Fail over automático
- RPO = 0
- RTO = minutos
- Poder ter um Preferred Placement, porém no fail over o Connect Placement é alterado automáticamente. Pode ser revertido

**MySQL HeatWave**
- MySQL é bom para dados transacionais
- MySQL não é bom para dados analiticos
- Problema:
    - precisa de dois bancos de dados
    - Processo de ETL do MySQL para OLAP
    - análise dos dados não é em tempo real
    - compliance e segurança para duas bases de dados
    - custos com licenciamento de  ETL
- Solução: MySQL Heatwave
- Transacional + analítico
- não precisa mudar nada na aplicação
- mesma arquitetura para processamento de consulta massivas e paralelas
- Excelente custo x benefício
- Integrado com outras soluções OCI
- Arquitetura
    - nodes dedicados  e distribuídos
    - processamento de dados em memória
    - scalling em tempo real
    - In-memory, usa engine específico para consultas colunares
    - usa object storage para a camada de dados persistentes (tráfego em trânsito é criptgrafado)
    - fail over automátco
    - tempo de falha de até 60 segundos, caso identificado outro node é criado
- Features
    - a gestão do banco de dados é a mesma (independente se é transacional ou analítico)
    - Syntaxe SQL é a mesma
    - O próprio banco detecta que a consulta é analítica, envia para os nodes específicos e retorno o resultado para o cliente
    - feature para ML nativa
    - rotinas de ML podem ser pré criadas para serem executadas através de uma query SL
    - ML pode ser treinado

**Oracle Database Service for Azure**
- Permite usar bancos de dados Oracle, na nuvem OCI, a partir da Azure
- Para o usuário, a experiência é como usar Azure 3 passos necessários
    1. estabelecer conexão entre as contas/clouds
    2. provisionar o banco de dados, via portal Azure
    3. Utilizar os serviços, gerenciar logs/métricas a partir do Azure
- Serviços suportados
- Autonomous Database on Shared Exadata Infrastructure
- Exadata Database  Service
- Base Database Service
- MySQL HeatWave

**Como funciona**
- usuário tem o portal Azure para criar e gerenciar os recursos na OCI conexão é automática, basta ter subscription no Azure
- Usar o AzureAD para autenticar os usuários que forem utilizar os serviços OCI
- Acesso ao banco é direto
- conectividade é de baixa latência
- Logs gerados na OCI são enviados para Azure
- Suporte é colaborativo entre Azure e Oracle
-  5 passos para usar
    1. definir os pré-requisitos
    2. estabelecer conexão
    3. Criar grupos de usuários no Azure para criar e gerenciar recursos na OCI
    4. Provisionar bancos de dados
    5. usar. Gerenciar o serviço