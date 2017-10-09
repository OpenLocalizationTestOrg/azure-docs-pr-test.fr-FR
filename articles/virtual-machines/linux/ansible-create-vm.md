---
title: aaaUse Ansible toocreate une VM Linux base dans Azure | Documents Microsoft
description: "Découvrez comment toouse Ansible toocreate et de gérer un ordinateur de virtuel Linux base dans Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: ffe278b3f846924ff9c4d026120565146f951152
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="c0dfa-103">Créer une machine virtuelle Linux de base dans Azure avec Ansible</span><span class="sxs-lookup"><span data-stu-id="c0dfa-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="c0dfa-104">Ansible vous permet de déploiement de hello tooautomate et configuration des ressources dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="c0dfa-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="c0dfa-105">Vous pouvez utiliser Ansible toomanage vos machines virtuelles (VM) dans Azure, même hello comme vous le feriez pour toute autre ressource.</span><span class="sxs-lookup"><span data-stu-id="c0dfa-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="c0dfa-106">Cet article vous montre comment toocreate une base pour machine virtuelle avec Ansible.</span><span class="sxs-lookup"><span data-stu-id="c0dfa-106">This article shows you how toocreate a basic VM with Ansible.</span></span> <span data-ttu-id="c0dfa-107">Vous pouvez également apprendre comment trop[créer un environnement de machine virtuelle complète avec Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="c0dfa-107">You can also learn how too[Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c0dfa-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c0dfa-108">Prerequisites</span></span>
<span data-ttu-id="c0dfa-109">toomanage Azure ressources avec Ansible, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="c0dfa-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="c0dfa-110">Ansible et hello modules Azure Python SDK installés sur votre système hôte.</span><span class="sxs-lookup"><span data-stu-id="c0dfa-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="c0dfa-111">Installez Ansible sur [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) et [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="c0dfa-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="c0dfa-112">Informations d’identification Azure et Ansible configuré toouse les.</span><span class="sxs-lookup"><span data-stu-id="c0dfa-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="c0dfa-113">Créer des informations d’identification Azure et configurer Ansible</span><span class="sxs-lookup"><span data-stu-id="c0dfa-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="c0dfa-114">Azure CLI version 2.0.4 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c0dfa-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c0dfa-115">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="c0dfa-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="c0dfa-116">Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c0dfa-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="c0dfa-117">Vous pouvez également utiliser [Cloud Shell](/azure/cloud-shell/quickstart) à partir de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="c0dfa-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="c0dfa-118">Créer des ressources Azure de support</span><span class="sxs-lookup"><span data-stu-id="c0dfa-118">Create supporting Azure resources</span></span>
<span data-ttu-id="c0dfa-119">Dans cet exemple, nous créons un runbook qui déploie une machine virtuelle dans une infrastructure existante.</span><span class="sxs-lookup"><span data-stu-id="c0dfa-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="c0dfa-120">Créez d’abord un groupe de ressources avec [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="c0dfa-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="c0dfa-121">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="c0dfa-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="c0dfa-122">Créez un réseau virtuel pour votre machine virtuelle avec [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="c0dfa-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="c0dfa-123">Hello exemple suivant crée un réseau virtuel nommé *myVnet* et un sous-réseau nommé *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="c0dfa-123">hello following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="c0dfa-124">Créer et exécuter un playbook Ansible</span><span class="sxs-lookup"><span data-stu-id="c0dfa-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="c0dfa-125">Créer un scénario Ansible nommé **azure_create_vm.yml** et coller hello suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="c0dfa-125">Create an Ansible playbook named **azure_create_vm.yml** and paste hello following contents.</span></span> <span data-ttu-id="c0dfa-126">Cet exemple crée une seule machine virtuelle et configure les informations d’identification SSH.</span><span class="sxs-lookup"><span data-stu-id="c0dfa-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="c0dfa-127">Entrez vos propres données de clé publique Bonjour *key_data* paire comme suit :</span><span class="sxs-lookup"><span data-stu-id="c0dfa-127">Enter your own public key data in hello *key_data* pair as follows:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create VM
    azure_rm_virtualmachine:
      resource_group: myResourceGroup
      name: myVM
      vm_size: Standard_DS1_v2
      admin_username: azureuser
      ssh_password_enabled: false
      ssh_public_keys: 
        - path: /home/azureuser/.ssh/authorized_keys
          key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="c0dfa-128">hello toocreate machine virtuelle avec Ansible, exécutez manuel de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c0dfa-128">toocreate hello VM with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="c0dfa-129">sortie de Hello ressemble toohello similaire qui affiche hello que machine virtuelle a été créé avec succès l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c0dfa-129">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="c0dfa-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c0dfa-130">Next steps</span></span>
<span data-ttu-id="c0dfa-131">Cet exemple crée une machine virtuelle dans un groupe de ressources existant avec un réseau virtuel déjà déployé.</span><span class="sxs-lookup"><span data-stu-id="c0dfa-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="c0dfa-132">Pour obtenir un exemple plus détaillé sur la façon de toouse Ansible toocreate prise en charge des ressources telles que d’un réseau virtuel et les règles du groupe de sécurité réseau, consultez [créer un environnement de machine virtuelle complète avec Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="c0dfa-132">For a more detailed example on how toouse Ansible toocreate supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>
