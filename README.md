# ☁️ Azure VMSS Autoscale
Praticando VMSS (virtual machine scale sets) com Azure.

[![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)](https://azure.microsoft.com)
[![Shell Script](https://img.shields.io/badge/Shell_Script-121011?style=for-the-badge&logo=gnu-bash&logoColor=white)](https://www.gnu.org/software/bash/)
[![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)](https://www.linux.org/)

> [!NOTE]
> O **Azure Virtual Machine Scale Sets (MVSS) Autoscale** (dimensionamento automático) é um recurso da nuvem Microsoft que **aumenta ou diminui automaticamente** o número de **máquinas virtuais** (VMs) que executam uma aplicação, respondendo a auma demandan real de tráfego.

> [!IMPORTANT]
> A **elasticidade** é a capacidade do Azure de **aumentar ou diminuir** recursos automaticamente conforme a demanda flutua. Já a **mensurabilidade** é toda ação **monitorada e cobrada** com base no consumo real.

## 📌 Passo a Passo

### Criar Grupo de Recursos
> [!NOTE]
> Um **grupo de recursos** é um contêiner lógico que agrupa recursos relacionados, como máquinas virtuais, bancos de dados, redes e entre outros, para uma solução específica.

```
az group create --name <rg-name> --location <location>
```
