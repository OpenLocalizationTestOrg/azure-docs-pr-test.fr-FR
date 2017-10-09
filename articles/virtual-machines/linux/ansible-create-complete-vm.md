---
title: "aaaUse Ansible toocreate une VM Linux complète dans Azure | Documents Microsoft"
description: "Découvrez comment toouse Ansible toocreate et gérer un environnement de machine virtuelle Linux complet dans Azure"
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
ms.openlocfilehash: 970b0427f39fc23240f9faab868196ca4f444e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a><span data-ttu-id="27518-103">Création d’un environnement de machine virtuelle Linux complète dans Azure avec Ansible</span><span class="sxs-lookup"><span data-stu-id="27518-103">Create a complete Linux virtual machine environment in Azure with Ansible</span></span>
<span data-ttu-id="27518-104">Ansible vous permet de déploiement de hello tooautomate et configuration des ressources dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="27518-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="27518-105">Vous pouvez utiliser Ansible toomanage vos machines virtuelles (VM) dans Azure, même hello comme vous le feriez pour toute autre ressource.</span><span class="sxs-lookup"><span data-stu-id="27518-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="27518-106">Cet article vous explique comment toocreate un environnement Linux complet et prise en charge des ressources avec Ansible.</span><span class="sxs-lookup"><span data-stu-id="27518-106">This article shows you how toocreate a complete Linux environment and supporting resources with Ansible.</span></span> <span data-ttu-id="27518-107">Vous pouvez également apprendre comment trop[créer une base pour machine virtuelle avec Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="27518-107">You can also learn how too[Create a basic VM with Ansible](ansible-create-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="27518-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="27518-108">Prerequisites</span></span>
<span data-ttu-id="27518-109">toomanage Azure ressources avec Ansible, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="27518-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="27518-110">Ansible et hello modules Azure Python SDK installés sur votre système hôte.</span><span class="sxs-lookup"><span data-stu-id="27518-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="27518-111">Installez Ansible sur [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) et [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="27518-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="27518-112">Informations d’identification Azure et Ansible configuré toouse les.</span><span class="sxs-lookup"><span data-stu-id="27518-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="27518-113">Créer des informations d’identification Azure et configurer Ansible</span><span class="sxs-lookup"><span data-stu-id="27518-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="27518-114">Azure CLI version 2.0.4 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="27518-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="27518-115">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="27518-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="27518-116">Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="27518-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="27518-117">Vous pouvez également utiliser [Cloud Shell](/azure/cloud-shell/quickstart) à partir de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="27518-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-virtual-network"></a><span data-ttu-id="27518-118">Création d’un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="27518-118">Create virtual network</span></span>
<span data-ttu-id="27518-119">la section suivante dans un scénario Ansible Hello crée un réseau virtuel nommé *myVnet* Bonjour *10.0.0.0/16* l’espace d’adressage :</span><span class="sxs-lookup"><span data-stu-id="27518-119">hello following section in an Ansible playbook creates a virtual network named *myVnet* in hello *10.0.0.0/16* address space:</span></span>

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

<span data-ttu-id="27518-120">tooadd un sous-réseau, hello après section crée un sous-réseau nommé *mySubnet* Bonjour *myVnet* réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="27518-120">tooadd a subnet, hello following section creates a subnet named *mySubnet* in hello *myVnet* virtual network:</span></span>

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a><span data-ttu-id="27518-121">Création d’une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="27518-121">Create public IP address</span></span>
<span data-ttu-id="27518-122">ressources tooaccess entre hello Internet, créer et affecter un tooyour d’adresse IP publique machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="27518-122">tooaccess resources across hello Internet, create and assign a public IP address tooyour VM.</span></span> <span data-ttu-id="27518-123">la section suivante dans un scénario Ansible Hello crée une adresse IP publique nommée *myPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="27518-123">hello following section in an Ansible playbook creates a public IP address named *myPublicIP*:</span></span>

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a><span data-ttu-id="27518-124">Créer un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="27518-124">Create Network Security Group</span></span>
<span data-ttu-id="27518-125">Flux de hello du contrôle des groupes de sécurité réseau du trafic réseau vers et depuis votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="27518-125">Network Security Groups control hello flow of network traffic in and out of your VM.</span></span> <span data-ttu-id="27518-126">la section suivante dans un scénario Ansible Hello crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup* et définit un trafic SSH tooallow règle sur le port TCP 22 :</span><span class="sxs-lookup"><span data-stu-id="27518-126">hello following section in an Ansible playbook creates a network security group named *myNetworkSecurityGroup* and defines a rule tooallow SSH traffic on TCP port 22:</span></span>

```yaml
- name: Create Network Security Group that allows SSH
  azure_rm_securitygroup:
    resource_group: myResourceGroup
    name: myNetworkSecurityGroup
    rules:
      - name: SSH
        protocol: TCP
        destination_port_range: 22
        access: Allow
        priority: 1001
        direction: Inbound
```


## <a name="create-virtual-network-interface-card"></a><span data-ttu-id="27518-127">Créer une carte réseau virtuelle</span><span class="sxs-lookup"><span data-stu-id="27518-127">Create virtual network interface card</span></span>
<span data-ttu-id="27518-128">Une carte d’interface réseau virtuelle (NIC) connecte à votre tooa de machine virtuelle donné de réseau virtuel, adresse IP publique et un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="27518-128">A virtual network interface card (NIC) connects your VM tooa given virtual network, public IP address, and network security group.</span></span> <span data-ttu-id="27518-129">la section suivante dans un scénario Ansible Hello crée une carte de réseau virtuel nommé *myNIC* connecté toohello des ressources réseau virtuel que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="27518-129">hello following section in an Ansible playbook creates a virtual NIC named *myNIC* connected toohello virtual networking resources you have created:</span></span>

```yaml
- name: Create virtual network inteface card
  azure_rm_networkinterface:
    resource_group: myResourceGroup
    name: myNIC
    virtual_network: myVnet
    subnet: mySubnet
    public_ip_name: myPublicIP
    security_group: myNetworkSecurityGroup
```


## <a name="create-virtual-machine"></a><span data-ttu-id="27518-130">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="27518-130">Create virtual machine</span></span>
<span data-ttu-id="27518-131">étape finale de Hello est toocreate une machine virtuelle et utiliser toutes les ressources hello créés.</span><span class="sxs-lookup"><span data-stu-id="27518-131">hello final step is toocreate a VM and use all hello resources created.</span></span> <span data-ttu-id="27518-132">la section suivante dans un scénario Ansible Hello crée un ordinateur virtuel nommé *myVM* et attache hello carte réseau virtuelle nommée *myNIC*.</span><span class="sxs-lookup"><span data-stu-id="27518-132">hello following section in an Ansible playbook creates a VM named *myVM* and attaches hello virtual NIC named *myNIC*.</span></span> <span data-ttu-id="27518-133">Entrez vos propres données de clé publique Bonjour *key_data* paire comme suit :</span><span class="sxs-lookup"><span data-stu-id="27518-133">Enter your own public key data in hello *key_data* pair as follows:</span></span>

```yaml
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
    network_interfaces: myNIC
    image:
      offer: CentOS
      publisher: OpenLogic
      sku: '7.3'
      version: latest
```

## <a name="complete-ansible-playbook"></a><span data-ttu-id="27518-134">Terminer le playbook Ansible</span><span class="sxs-lookup"><span data-stu-id="27518-134">Complete Ansible playbook</span></span>
<span data-ttu-id="27518-135">toobring toutes ces sections, forment un manuel Ansible nommé *azure_create_complete_vm.yml* et coller hello suivant contenu :</span><span class="sxs-lookup"><span data-stu-id="27518-135">toobring all these sections together, create an Ansible playbook named *azure_create_complete_vm.yml* and paste hello following contents:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create virtual network
    azure_rm_virtualnetwork:
      resource_group: myResourceGroup
      name: myVnet
      address_prefixes: "10.0.0.0/16"
  - name: Add subnet
    azure_rm_subnet:
      resource_group: myResourceGroup
      name: mySubnet
      address_prefix: "10.0.1.0/24"
      virtual_network: myVnet
  - name: Create public IP address
    azure_rm_publicipaddress:
      resource_group: myResourceGroup
      allocation_method: Static
      name: myPublicIP
  - name: Create Network Security Group that allows SSH
    azure_rm_securitygroup:
      resource_group: myResourceGroup
      name: myNetworkSecurityGroup
      rules:
        - name: SSH
          protocol: Tcp
          destination_port_range: 22
          access: Allow
          priority: 1001
          direction: Inbound
  - name: Create virtual network inteface card
    azure_rm_networkinterface:
      resource_group: myResourceGroup
      name: myNIC
      virtual_network: myVnet
      subnet: mySubnet
      public_ip_name: myPublicIP
      security_group: myNetworkSecurityGroup
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
      network_interfaces: myNIC
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="27518-136">Ansible a besoin d’un toodeploy de groupe de ressources toutes vos ressources dans.</span><span class="sxs-lookup"><span data-stu-id="27518-136">Ansible needs a resource group toodeploy all your resources into.</span></span> <span data-ttu-id="27518-137">Créez un groupe de ressources avec la commande [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="27518-137">Create a resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="27518-138">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="27518-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="27518-139">toocreate hello complète environnement de machine virtuelle avec Ansible, exécutez manuel de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="27518-139">toocreate hello complete VM environment with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_complete_vm.yml
```

<span data-ttu-id="27518-140">sortie de Hello ressemble toohello similaire qui affiche hello que machine virtuelle a été créé avec succès l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="27518-140">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create virtual network] *********************************************
changed: [localhost]

TASK [Add subnet] *********************************************************
changed: [localhost]

TASK [Create public IP address] *******************************************
changed: [localhost]

TASK [Create Network Security Group that allows SSH] **********************
changed: [localhost]

TASK [Create virtual network inteface card] *******************************
changed: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=7    changed=6    unreachable=0    failed=0
```

## <a name="next-steps"></a><span data-ttu-id="27518-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="27518-141">Next steps</span></span>
<span data-ttu-id="27518-142">Cet exemple crée un environnement de machine virtuelle complet, y compris des ressources de mise en réseau virtuel hello requis.</span><span class="sxs-lookup"><span data-stu-id="27518-142">This example creates a complete VM environment including hello required virtual networking resources.</span></span> <span data-ttu-id="27518-143">Pour un exemple plus directe toocreate une machine virtuelle dans les ressources réseau avec des options par défaut, consultez [créer une machine virtuelle](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="27518-143">For a more direct example toocreate a VM into existing network resources with default options, see [Create a VM](ansible-create-vm.md).</span></span>
