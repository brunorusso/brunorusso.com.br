---
title: "Testando o kubevirt no minikube"
author: "Bruno Russo"
date: 2026-04-05 01:00 +0300
categories: ["k8s"]
tags: ["OpenSource", "Kubernetes", "Transformação Digital"]
ping: true
math: true
mermaid: true
image: 
    path: https://www.brunorusso.com.br/assets/2026/Minukube+kubevirt.png
    alt: "MINIKUBE KUBERNETES + KUBEVIRT LOCAL LAB. Dividi-a em seções: 'CONTAINERS (PODS)' com ícones de contêineres, 'VIRTUAL MACHINES (VMs)' com um bloco de detalhes da VM apresentando o logotipo do Fedora e uma barra de status indicando 'KUBEVIRT OPERATOR ACTIVE'. Além disso, destaco os gráficos holográficos flutuantes acima do laptop, incluindo o logotipo do Kubernetes."
---

A virtualização de servidores é uma tecnologia que permite criar múltiplas máquinas virtuais (VMs) independentes dentro de um único servidor físico. Porém, é necessário ter um software que faça a orquestração de todas essas múltiplas máquinas virtuais.

Em um ambiente enterprise, existem soluções bem maduras e estremamente robustas, é claro que tudo tem o seu preço. Com a evolução e do aumento da maturidade da soluções opensource, uma solução que vem ganhado espaço no mundo corporativo é a solução [kubevirt](https://kubevirt.io/) que é baseada no [kubernetes](https://kubernetes.io/).

Para testar essa solução, fiz um laboratório em meu próprio [notebook](https://brunorusso.com.br/posts/Maria/), usando o [minikube](https://minikube.sigs.k8s.io/docs/).


> **Minikube** - permiter subir rapidamente um cluster Kubernetes local no macOS, Linux e Windows. Compatível com a versão mais recente do kubernetes, Suporta GPU, vários runtimes de contêiner e inúmeras outras funcionalidades.


> **Kubevirt** - é uma tecnologia que atende às necessidades de equipes de desenvolvimento que adotaram ou desejam adotar o Kubernetes , mas possuem cargas de trabalho existentes baseadas em máquinas virtuais que não podem ser facilmente conteinerizadas. Mais especificamente, a tecnologia fornece uma plataforma de desenvolvimento unificada onde os desenvolvedores podem criar, modificar e implantar aplicativos que residem tanto em contêineres de aplicativos quanto em máquinas virtuais em um ambiente comum e compartilhado. 


### Roteiro usado para teste


O passo a passo que usei para preparar o ambiente e subir uma máquina virtual está descrito abaixo:

1- O Minikube precisa estar instalado.
2- A inicialização do minikube foi realizada com o seguinte parâmetro.

```
minikube start --driver=docker --cpus=4 --memory=8192 --cni=flannel
```

3- Habilitei o addon de storage e habilitei, com o comando:

```
minikube addons enable storage-provisioner

minikube addons enable default-storageclass
```

4- Habilitei o kubevirt, com o comando:

```
minikube addons enable kubevirt
```

5- Habilitei alguns itens específicos, pois o objetivo era subir um servidor com Fedora Linux, e para isso foi necessário fazer o upload da imagem etc

```
export TAG=$(curl -s https://api.github.com/repos/kubevirt/containerized-data-importer/releases/latest | grep '"tag_name":' | sed -E 's/.*"([^"]+)".*/\1/')
kubectl create -f https://github.com/kubevirt/containerized-data-importer/releases/download/$TAG/cdi-operator.yaml
kubectl create -f https://github.com/kubevirt/containerized-data-importer/releases/download/$TAG/cdi-cr.yaml
kubectl port-forward -n cdi svc/cdi-uploadproxy 8443:443
```

6- A imagem do fedora que usei para o laboratório foi

```
cd /tmp 
wget https://br.mirrors.cicku.me/fedora/linux/releases/43/Cloud/x86_64/images/Fedora-Cloud-Base-Generic-43-1.6.x86_64.qcow2
```

7- Agora que as dependências foram sanadas, o próximo passo é fazer o upload da imagem para o cluster com o comando

```
./virtctl image-upload pvc fedora-pvc \
  --size=10Gi \
  --image-path=/tmp/Fedora-Cloud-Base-Generic-43-1.6.x86_64.qcow2 \
  --default-instancetype=n1.medium \
  --default-preference=fedora \
  --access-mode=ReadWriteOnce \
  --uploadproxy-url=https://127.0.0.1:8443 \
  --insecure
```

8- O próximo passo é criar um arquivo com o conteúdo abaixo, salvei ele com o nome de vm.yaml

```
apiVersion: kubevirt.io/v1
kind: VirtualMachine
metadata:
  name: fedora
spec:
  runStrategy: Always
  template:
    spec:
      domain:
        resources:
          requests:
            memory: 2048M # 2GB de RAM para o Fedora
        devices:
          disks:
          # O disco principal com o sistema que fizemos upload
          - name: os-disk
            disk:
              bus: virtio
          # O disco virtual temporário que injeta a senha
          - name: cloudinitdisk
            disk:
              bus: virtio
      volumes:
      # Apontando para o seu PVC recém-criado
      - name: os-disk
        persistentVolumeClaim:
          claimName: fedora-pvc
      # Configuração do usuário e senha
      - name: cloudinitdisk
        cloudInitNoCloud:
          userData: |-
            #cloud-config
            user: fedora
            password: fedorapassword
            chpasswd: { expire: False }
            ssh_pwauth: True
```


9- O próximo passo é criar a VM, com o comando

```
kubectl apply -f vm.yaml
```

10- Como o parâmetro **runStrategy** está definido com o valor **Always** a máquina virtual será inicializada automaticamente. Para visualizar, instalei o dashboard com o comando

```
minikube dashboard
```

11- Uma outra forma de visualizar é através do comando 

```
kubectl get vmis
```

12- Para acessar a console gráfica do ambiente, usa-se o comando

```
virtctl vnc fedora
```

13- Para acessar a console texto, usa-se o comando

```
virtctl console fedora
```



### Considerações sobre o laboratório

A execução deste laboratório surpreendeu pela agilidade e simplicidade.

Configurar o KubeVirt, que em um passado recente poderia parecer uma tarefa complexa, tornou-se quase trivial graças aos addons do Minikube e operadores como o CDI. Além disso, o ambiente se mostrou extremamente leve, permitindo rodar uma VM Fedora completa encapsulada em um cluster local sem exigir um hardware robusto. 

Isso comprova o quão acessível está se tornando testar arquiteturas modernas, permitindo que engenheiros validem a união do mundo de contêineres com máquinas virtuais em um único painel de controle, diretamente de seus notebooks.



### Conclusão

Em resumo, testar o KubeVirt via Minikube provou que explorar tecnologias avançadas de orquestração está ao alcance de qualquer notebook. O futuro da infraestrutura aponta para plataformas cada vez mais unificadas, onde a barreira entre o tradicional e o cloud-native se torna invisível para as esteiras de deploy. Dominar essas ferramentas é um passo fundamental para quem atua na linha de frente da tecnologia.