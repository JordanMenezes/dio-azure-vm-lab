# dio-azure-vm-lab

# Desafio DIO: Criando e Documentando uma VM no Azure

## 🚀 Objetivo
Este repositório reúne resumo, passo-a-passo, dicas e scripts para criação de uma máquina virtual Windows no Azure, conforme o laboratório da DIO.

## 📝 Sumário
1. Pré-requisitos  
2. Criando recursos no Portal  
3. Usando Azure CLI  
4. Conexão RDP e testes  
5. Cleanup  
6. Referências

## 1. Pré-requisitos
- Conta Microsoft/Azure ativa  
- Permissões de Owner ou Contributor no Subscription  
- Azure CLI (opcional se for usar portal)

## 2. Criando recursos no Portal
2.1. Criar Resource Group  
    - Abra o Portal → Resource Groups → Create  
    - Nome: `rg-dio-vm` / Região: `southcentralus`  
    - ![rg](images/01-create-rg.png)  
2.2. Criar máquina virtual  
    - Compute → Virtual Machines → Create  
    - Nome: `vm-dio-lab`  
    - Imagem: `Windows Server 2019 Datacenter`  
    - Tamanho: `Standard_B1s`  
    - Autenticação: Password / Usuário: `adminDIO`  
    - Rede virtual: `vnet-dio` / Subnet: `default`  
    - Network Security Group: permitir RDP porta 3389  
    - Review + Create  
    - ![vm-create](images/02-create-vm.png)

## 3. Usando Azure CLI  
```bash
# login
az login

# criar RG
az group create \
  --name rg-dio-vm \
  --location eastus

# criar VM
az vm create \
  --resource-group rg-dio-vm \
  --name vm-dio-lab \
  --image Win2019Datacenter \
  --admin-username adminDIO \
  --admin-password 'SenhaForte123!' \
  --size Standard_B1s \
  --public-ip-sku Standard \
  --generate-ssh-keys
