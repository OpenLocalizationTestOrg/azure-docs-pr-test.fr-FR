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
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a>Création d’un environnement de machine virtuelle Linux complète dans Azure avec Ansible
Ansible vous permet de déploiement de hello tooautomate et configuration des ressources dans votre environnement. Vous pouvez utiliser Ansible toomanage vos machines virtuelles (VM) dans Azure, même hello comme vous le feriez pour toute autre ressource. Cet article vous explique comment toocreate un environnement Linux complet et prise en charge des ressources avec Ansible. Vous pouvez également apprendre comment trop[créer une base pour machine virtuelle avec Ansible](ansible-create-vm.md).


## <a name="prerequisites"></a>Composants requis
toomanage Azure ressources avec Ansible, vous devez hello suivant :

- Ansible et hello modules Azure Python SDK installés sur votre système hôte.
    - Installez Ansible sur [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) et [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)
- Informations d’identification Azure et Ansible configuré toouse les.
    - [Créer des informations d’identification Azure et configurer Ansible](ansible-install-configure.md#create-azure-credentials)
- Azure CLI version 2.0.4 ou ultérieure. Exécutez `az --version` version de hello toofind. 
    - Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). Vous pouvez également utiliser [Cloud Shell](/azure/cloud-shell/quickstart) à partir de votre navigateur.


## <a name="create-virtual-network"></a>Création d’un réseau virtuel
la section suivante dans un scénario Ansible Hello crée un réseau virtuel nommé *myVnet* Bonjour *10.0.0.0/16* l’espace d’adressage :

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

tooadd un sous-réseau, hello après section crée un sous-réseau nommé *mySubnet* Bonjour *myVnet* réseau virtuel :

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a>Création d’une adresse IP publique
ressources tooaccess entre hello Internet, créer et affecter un tooyour d’adresse IP publique machine virtuelle. la section suivante dans un scénario Ansible Hello crée une adresse IP publique nommée *myPublicIP*:

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a>Créer un groupe de sécurité réseau
Flux de hello du contrôle des groupes de sécurité réseau du trafic réseau vers et depuis votre machine virtuelle. la section suivante dans un scénario Ansible Hello crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup* et définit un trafic SSH tooallow règle sur le port TCP 22 :

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


## <a name="create-virtual-network-interface-card"></a>Créer une carte réseau virtuelle
Une carte d’interface réseau virtuelle (NIC) connecte à votre tooa de machine virtuelle donné de réseau virtuel, adresse IP publique et un groupe de sécurité réseau. la section suivante dans un scénario Ansible Hello crée une carte de réseau virtuel nommé *myNIC* connecté toohello des ressources réseau virtuel que vous avez créé :

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


## <a name="create-virtual-machine"></a>Create virtual machine
étape finale de Hello est toocreate une machine virtuelle et utiliser toutes les ressources hello créés. la section suivante dans un scénario Ansible Hello crée un ordinateur virtuel nommé *myVM* et attache hello carte réseau virtuelle nommée *myNIC*. Entrez vos propres données de clé publique Bonjour *key_data* paire comme suit :

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

## <a name="complete-ansible-playbook"></a>Terminer le playbook Ansible
toobring toutes ces sections, forment un manuel Ansible nommé *azure_create_complete_vm.yml* et coller hello suivant contenu :

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

Ansible a besoin d’un toodeploy de groupe de ressources toutes vos ressources dans. Créez un groupe de ressources avec la commande [az group create](/cli/azure/vm#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :

```azurecli
az group create --name myResourceGroup --location eastus
```

toocreate hello complète environnement de machine virtuelle avec Ansible, exécutez manuel de hello comme suit :

```bash
ansible-playbook azure_create_complete_vm.yml
```

sortie de Hello ressemble toohello similaire qui affiche hello que machine virtuelle a été créé avec succès l’exemple suivant :

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

## <a name="next-steps"></a>Étapes suivantes
Cet exemple crée un environnement de machine virtuelle complet, y compris des ressources de mise en réseau virtuel hello requis. Pour un exemple plus directe toocreate une machine virtuelle dans les ressources réseau avec des options par défaut, consultez [créer une machine virtuelle](ansible-create-vm.md).
