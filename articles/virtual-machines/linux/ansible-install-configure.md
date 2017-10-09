---
title: aaaInstall et configurer Ansible pour une utilisation avec des machines virtuelles | Documents Microsoft
description: "Découvrez comment tooinstall et configurer Ansible pour la gestion des ressources Azure sur Ubuntu, CentOS et SLES"
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
ms.openlocfilehash: b33d1893909b6134a5474617c9af2d6e4f627c05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a>Installer et configurer des machines virtuelles de toomanage Ansible dans Azure
Cet article décrit en détail comment tooinstall Ansible et les modules Azure Python SDK requis pour certaines des hello distributions de Linux prises les plus courantes. Vous pouvez installer Ansible sur d’autres versions en ajustant hello installé packages toofit votre plateforme spécifique. toocreate Azure des ressources de manière sécurisée, vous apprendrez également comment toocreate et définir les informations d’identification pour Ansible toouse. 

Pour plus d’options d’installation de plates-formes supplémentaires, consultez hello [Ansible guide d’installation](https://docs.ansible.com/ansible/intro_installation.html).


## <a name="install-ansible"></a>Installer Ansible
Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupAnsible* Bonjour *eastus* emplacement :

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

Maintenant, créez une machine virtuelle et installer Ansible pour l’une des hello suivant les versions de :

- [Ubuntu 16.04 LTS](#ubuntu1604-lts)
- [CentOS 7.3](#centos-73)
- [SLES 12.2 SP2](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS
Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create). Hello exemple suivant crée un ordinateur virtuel nommé *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH à l’aide de machine virtuelle tooyour hello `publicIpAddress` hello figurant à l’opération de création de sortie à partir de la machine virtuelle de hello :

```bash
ssh azureuser@<publicIpAddress>
```

Sur votre machine virtuelle, installez les packages hello requis pour les modules du Kit de développement logiciel Azure Python hello et Ansible comme suit :

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Azure SDKs via pip
pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via apt
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update && sudo apt-get install -y ansible
```

À présent passer trop[informations d’identification Azure de créer](#create-azure-credentials).


### <a name="centos-73"></a>CentOS 7.3
Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create). Hello exemple suivant crée un ordinateur virtuel nommé *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH à l’aide de machine virtuelle tooyour hello `publicIpAddress` hello figurant à l’opération de création de sortie à partir de la machine virtuelle de hello :

```bash
ssh azureuser@<publicIpAddress>
```

Sur votre machine virtuelle, installez les packages hello requis pour les modules du Kit de développement logiciel Azure Python hello et Ansible comme suit :

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

À présent passer trop[informations d’identification Azure de créer](#create-azure-credentials).


### <a name="sles-122-sp2"></a>SLES 12.2 SP2
Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create). Hello exemple suivant crée un ordinateur virtuel nommé *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH à l’aide de machine virtuelle tooyour hello `publicIpAddress` hello figurant à l’opération de création de sortie à partir de la machine virtuelle de hello :

```bash
ssh azureuser@<publicIpAddress>
```

Sur votre machine virtuelle, installez les packages hello requis pour les modules du Kit de développement logiciel Azure Python hello et Ansible comme suit :

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

À présent passer trop[informations d’identification Azure de créer](#create-azure-credentials).


## <a name="create-azure-credentials"></a>Créer des informations d’identification Azure
Ansible communique avec Azure en utilisant un nom d’utilisateur et un mot de passe, ou un principal de service. Un principal de service Azure est une identité de sécurité que vous pouvez utiliser avec des applications, des services et des outils d’automatisation comme Ansible. Contrôler et de définir des autorisations de hello comme principal du service hello toowhat opérations réalisables dans Azure. sécurité tooimprove simplement en fournissant un nom d’utilisateur et un mot de passe, cet exemple crée un service de base principale.

Créer un service principal avec [az ad sp créer-de-rbac](/cli/azure/ad/sp#create-for-rbac) et informations d’identification de hello sortie Ansible doit :

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Voici un exemple de sortie de hello de hello précédant les commandes :

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

tooauthenticate tooAzure, vous devez également tooobtain avec l’ID de votre abonnement Azure [afficher de compte az](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Vous utilisez la sortie hello à partir de ces deux commandes à l’étape suivante de hello.


## <a name="create-ansible-credentials-file"></a>Créer un fichier d’informations d’identification Ansible
tooprovide tooAnsible les informations d’identification, vous définissez les variables d’environnement ou créez un fichier d’informations d’identification locales. Pour plus d’informations sur la façon de voir des informations d’identification de toodefine Ansible, [fournissant les informations d’identification tooAzure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules). 

Pour un environnement de développement, créez un fichier *d’informations d’identification* pour Ansible sur votre machine virtuelle hôte comme suit :

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

Hello *informations d’identification* fichier lui-même associe des ID d’abonnement hello sortie hello de création d’un principal de service. La sortie à partir de hello précédente [az ad sp créer-de-rbac](/cli/azure/ad/sp#create-for-rbac) commande est la même hello classer en fonction des besoins pour *client_id*, *secret*, et *client* . Hello selon exemple *informations d’identification* fichier affiche ces valeurs correspondant à la sortie précédente hello. Saisissez vos propres valeurs, comme suit :

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a>Utiliser des variables d’environnement Ansible
Si vous vous apprêtez toouse des outils tels que Ansible tour ou Jenkins, vous pouvez définir des variables d’environnement comme suit. Ces variables associent des ID d’abonnement hello sortie hello à partir de la création d’un service principal. Sortie de hello précédente [az ad sp créer-de-rbac](/cli/azure/ad/sp#create-for-rbac) commande est la même hello classer en fonction des besoins pour *AZURE_CLIENT_ID*, *AZURE_SECRET*, et *AZURE_ CLIENT*. 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a>Étapes suivantes
Vous avez maintenant Ansible et hello nécessaire modules Azure Python SDK installés et les informations d’identification définies pour Ansible toouse. Découvrez comment trop[créer une machine virtuelle avec Ansible](ansible-create-vm.md). Vous pouvez également apprendre comment trop[créer une machine virtuelle de Azure complète et la prise en charge des ressources avec Ansible](ansible-create-complete-vm.md).
