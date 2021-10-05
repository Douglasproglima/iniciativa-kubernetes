### Kubernets: 
	É formado por um cluster(São um conjunto de máquina) e cada
	um dessas máquina irá exercer um dos dois papeis possíveis

### Papeis:
1 - Kubernetes Nodes
	Node é responsável por executar os container das app's.
	responsável por executar toda a carga.

#### Componentes do Node:
	1.1 Kulelet:
		Atua como agente de inspeção do node
		Responsável por garantir a execução dos containers e interagir com o 
		Kube Api Server para reportar o STATUS. 
			
	1.2 Kube Proxy:
		Responsável pelas comunicações de redes com o Cluster 
			
	1.3 Container Runtime ou CRI:
		São as especificações necessárias para que um container runtime
		seja utilizado dentro do Kubernete para executar os containers.
			
		Obs: 
		1 - É possível executar vários containers em runtime ao mesmo.
		2 - O Docker nunca implementou o Container Runtime Interface ou CRI.
		O Docker usa Docker Shim com adaptador como Interface do CRI e a interface do Docker.
		3 - Versão 1.20 Kubernet descontinuado o uso do Docker como container runtime
		4 - Alternativas que podem ser usados ao inves do Docker no caso de um container runtime:
				Container Shim
				Container RKT
				Container Frakti
				Container CRI-O
			
	2 - Kubernetes Control Plane:
	Responsável por iniciar os nodes e orquestrar todo o cluster.
	Observação: Para garantir alta disponibilidade do cluster é necessário
				ter pelo ao menos dois Control Plane disponíveis, pois caso
				ocorra algum problema o outro assume o papel
	
	Componentes do Control Plane:
		2.1 Kube Api Server:
			Responsável por receber toda comunicação com o cluster.
			Qualquer comunicação(Comando) feita através da Api Server ou KubeCTL
			será com o Kube Api Server que essa comunicação irá ocorrer.
			
		2.2 ETCD:
			É um banco de chave e valor que armazena todos os dados do Kubernete.
			Obs: Os dados dsse BD deve ser acessado pelo componente Kube Api Server.
			
		2.3 Kube Scheduler:
			Responsável por organizar onde cada processo será executado.
			Ele analisa as especificações e verifica quais nodes podem atender a demanda
			e define a onde ele será executado.
			
		2.4 Kube Controller Manager:
			Responsável por executar/gerenciar todos os controladores do Kubernete.
			Resumindo, o cara que administra as tomadas de decisões do Kubernete.
			Exemplo:
				*Autenticações;
				*Autorizações;
				*Admissões.
		
#### FORMAS DE TER UM CLUSTER KUBERNETES
---
	On-Premisse:
		Geralmente usa máquinas fisicas/Virtuais(EC2, Azure, etc...) e a 
		instalação e configurações são feitas do zero.
		
		Ferramentas para criar o cluster kubernete on-premisse
			> Kubeadm
			> Kubespray
			> RKE
			> K3S
			> MicroK8S
		
		Não recomendável quando se tem uma equipe pequena ou equipe com pouca experiência com
		o kubernete.
		
		Vantagem:
			*Controle Total sobre o cluster kubernete
		Desvantagem
			*Responsabilidade total do cluster kubernete.
			*Atualização dos S.O's
			*Atualização do Kubernete
			*Atualização das máquinas
			*Equipe capacitada
	
	KaaS(Kubernet as a Service)
		Vantagem:
			Delegação das responsabilidade do cluster para o provedor cloud
		
		Desvantagem
			Preço
		
		Pode ser usados vários serviços dos provedores de cloud como:
			AWS.........: EKS
			Azure.......: AKS
			Google Cloud: GKE
			Oracle......: OKE
	
	Local
		Vantagem
			Economia de recurso para o Datacenter produção ou ambiente de Nuvem
			Antecipa uma etapa antes do deploy no ambiente de homologação/produção
		
		Ferramentas:
			Minikube
			Kind (Kubernete in Docker)
			K3D
			MicroK8S
			K3S
			
#### USANDO O KIND LOCAL - https://kind.sigs.k8s.io/
---
Instalar o KubeCTL parecido como se fosse o Docker CLI
	https://kubernetes.io/docs/tasks/tools/

Instalar o Kind:
	https://kind.sigs.k8s.io/docs/user/quick-start/#installation
	sudo mv ./kind /usr/local/bin
	
	
#### CRIANDO O CLUSTER COM O KIND
---
```sh
$ sudo service docker start
$ kind create cluster
```