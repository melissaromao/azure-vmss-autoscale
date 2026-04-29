# ☁️ Azure VMSS Autoscale
Praticando VMSS (virtual machine scale sets) com Azure.

[![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)](https://azure.microsoft.com)
[![Shell Script](https://img.shields.io/badge/Shell_Script-121011?style=for-the-badge&logo=gnu-bash&logoColor=white)](https://www.gnu.org/software/bash/)
[![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)](https://www.linux.org/)

> [!TIP]
> A **elasticidade** é a capacidade do Azure de **aumentar ou diminuir** recursos automaticamente conforme a demanda flutua. Já a **mensurabilidade** é toda ação **monitorada e cobrada** com base no consumo real.

## 📌 Passo a Passo

### Criar Grupo de Recursos
> [!NOTE]
> Um **grupo de recursos** é um contêiner lógico que agrupa recursos relacionados, como máquinas virtuais, bancos de dados, redes e entre outros, para uma solução específica.

```
az group create --name <rg-name> --location <location>
```

### Criar o VMSS
> [!NOTE]
> O **Azure Virtual Machine Scale Sets (MVSS)** é um serviço de computação do Azure que permite **criar** e **gerenciar** um **grupo de máquinas virtuais** (VMs) **idênticas e balanceadas**, com capacidade de **autoescala** (aumentar ou diminuir o número de instâncias) **automática** conforme a **demanda**, **otimizando custos e alta disponibilidade.**
```
# Iniciando com 2 instâncias
az vmss create \
  --resource-group rg-vmss \
  --name MeuVMSS \
  --image "Canonical:ubuntu-24_04-lts:server-arm64:latest" \
  --vm-sku Standard_B2pls_v2 \
  --location southcentralus \
  --admin-username azureuser \
  --admin-password 'Admin@123456' \
  --authentication-type password \
  --instance-count 2 \
  --upgrade-policy-mode automatic
```

### Criar a Configuração de Autoscale
```
az monitor autoscale create \
  --resource-group rg-vmss \
  --resource MeuVMSS \
  --resource-type Microsoft.Compute/virtualMachineScaleSets \
  --name escalaAutomatica \
  --min-count 2 \
  --max-count 5 \
  --count 2

az monitor autoscale rule create \
  --resource-group rg-vmss \
  --autoscale-name escalaAutomatica \
  --condition "Percentage CPU > 75 avg 5m" \
  --scale out 1

az monitor autoscale rule create \
  --resource-group rg-vmss \
  --autoscale-name escalaAutomatica \
  --condition "Percentage CPU < 25 avg 5m" \
  --scale in 1
```

### LoadBalancer
```
# Pegando o IP
az network public-ip list --resource-group rg-vmss --query "[].ipAddress" --output table

# Conectando via SSH
ssh azureuser@IP_DO_LOAD_BALANCER -p 50001

# Instalando e rodando o stress
sudo apt-get update
sudo apt-get install stress -y
sudo stress --cpu 1 --timeout 600
```

