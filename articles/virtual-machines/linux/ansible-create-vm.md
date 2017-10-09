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
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a>Créer une machine virtuelle Linux de base dans Azure avec Ansible
Ansible vous permet de déploiement de hello tooautomate et configuration des ressources dans votre environnement. Vous pouvez utiliser Ansible toomanage vos machines virtuelles (VM) dans Azure, même hello comme vous le feriez pour toute autre ressource. Cet article vous montre comment toocreate une base pour machine virtuelle avec Ansible. Vous pouvez également apprendre comment trop[créer un environnement de machine virtuelle complète avec Ansible](ansible-create-complete-vm.md).


## <a name="prerequisites"></a>Composants requis
toomanage Azure ressources avec Ansible, vous devez hello suivant :

- Ansible et hello modules Azure Python SDK installés sur votre système hôte.
    - Installez Ansible sur [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) et [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)
- Informations d’identification Azure et Ansible configuré toouse les.
    - [Créer des informations d’identification Azure et configurer Ansible](ansible-install-configure.md#create-azure-credentials)
- Azure CLI version 2.0.4 ou ultérieure. Exécutez `az --version` version de hello toofind. 
    - Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). Vous pouvez également utiliser [Cloud Shell](/azure/cloud-shell/quickstart) à partir de votre navigateur.


## <a name="create-supporting-azure-resources"></a>Créer des ressources Azure de support
Dans cet exemple, nous créons un runbook qui déploie une machine virtuelle dans une infrastructure existante. Créez d’abord un groupe de ressources avec [az group create](/cli/azure/vm#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :

```azurecli
az group create --name myResourceGroup --location eastus
```

Créez un réseau virtuel pour votre machine virtuelle avec [az network vnet create](/cli/azure/network/vnet#create). Hello exemple suivant crée un réseau virtuel nommé *myVnet* et un sous-réseau nommé *mySubnet*:

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a>Créer et exécuter un playbook Ansible
Créer un scénario Ansible nommé **azure_create_vm.yml** et coller hello suivant le contenu. Cet exemple crée une seule machine virtuelle et configure les informations d’identification SSH. Entrez vos propres données de clé publique Bonjour *key_data* paire comme suit :

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

hello toocreate machine virtuelle avec Ansible, exécutez manuel de hello comme suit :

```bash
ansible-playbook azure_create_vm.yml
```

sortie de Hello ressemble toohello similaire qui affiche hello que machine virtuelle a été créé avec succès l’exemple suivant :

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a>Étapes suivantes
Cet exemple crée une machine virtuelle dans un groupe de ressources existant avec un réseau virtuel déjà déployé. Pour obtenir un exemple plus détaillé sur la façon de toouse Ansible toocreate prise en charge des ressources telles que d’un réseau virtuel et les règles du groupe de sécurité réseau, consultez [créer un environnement de machine virtuelle complète avec Ansible](ansible-create-complete-vm.md).
