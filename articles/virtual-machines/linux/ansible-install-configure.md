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
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a><span data-ttu-id="bf13e-103">Installer et configurer des machines virtuelles de toomanage Ansible dans Azure</span><span class="sxs-lookup"><span data-stu-id="bf13e-103">Install and configure Ansible toomanage virtual machines in Azure</span></span>
<span data-ttu-id="bf13e-104">Cet article décrit en détail comment tooinstall Ansible et les modules Azure Python SDK requis pour certaines des hello distributions de Linux prises les plus courantes.</span><span class="sxs-lookup"><span data-stu-id="bf13e-104">This article details how tooinstall Ansible and required Azure Python SDK modules for some of hello most common Linux distros.</span></span> <span data-ttu-id="bf13e-105">Vous pouvez installer Ansible sur d’autres versions en ajustant hello installé packages toofit votre plateforme spécifique.</span><span class="sxs-lookup"><span data-stu-id="bf13e-105">You can install Ansible on other distros by adjusting hello installed packages toofit your particular platform.</span></span> <span data-ttu-id="bf13e-106">toocreate Azure des ressources de manière sécurisée, vous apprendrez également comment toocreate et définir les informations d’identification pour Ansible toouse.</span><span class="sxs-lookup"><span data-stu-id="bf13e-106">toocreate Azure resources in a secure manner, you also learn how toocreate and define credentials for Ansible toouse.</span></span> 

<span data-ttu-id="bf13e-107">Pour plus d’options d’installation de plates-formes supplémentaires, consultez hello [Ansible guide d’installation](https://docs.ansible.com/ansible/intro_installation.html).</span><span class="sxs-lookup"><span data-stu-id="bf13e-107">For more installation options and steps for additional platforms, see hello [Ansible install guide](https://docs.ansible.com/ansible/intro_installation.html).</span></span>


## <a name="install-ansible"></a><span data-ttu-id="bf13e-108">Installer Ansible</span><span class="sxs-lookup"><span data-stu-id="bf13e-108">Install Ansible</span></span>
<span data-ttu-id="bf13e-109">Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="bf13e-109">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="bf13e-110">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupAnsible* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="bf13e-110">hello following example creates a resource group named *myResourceGroupAnsible* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

<span data-ttu-id="bf13e-111">Maintenant, créez une machine virtuelle et installer Ansible pour l’une des hello suivant les versions de :</span><span class="sxs-lookup"><span data-stu-id="bf13e-111">Now create a VM and install Ansible for one of hello following distros:</span></span>

- [<span data-ttu-id="bf13e-112">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="bf13e-112">Ubuntu 16.04 LTS</span></span>](#ubuntu1604-lts)
- [<span data-ttu-id="bf13e-113">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="bf13e-113">CentOS 7.3</span></span>](#centos-73)
- [<span data-ttu-id="bf13e-114">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="bf13e-114">SLES 12.2 SP2</span></span>](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="bf13e-115">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="bf13e-115">Ubuntu 16.04 LTS</span></span>
<span data-ttu-id="bf13e-116">Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="bf13e-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="bf13e-117">Hello exemple suivant crée un ordinateur virtuel nommé *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="bf13e-117">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="bf13e-118">SSH à l’aide de machine virtuelle tooyour hello `publicIpAddress` hello figurant à l’opération de création de sortie à partir de la machine virtuelle de hello :</span><span class="sxs-lookup"><span data-stu-id="bf13e-118">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="bf13e-119">Sur votre machine virtuelle, installez les packages hello requis pour les modules du Kit de développement logiciel Azure Python hello et Ansible comme suit :</span><span class="sxs-lookup"><span data-stu-id="bf13e-119">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

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

<span data-ttu-id="bf13e-120">À présent passer trop[informations d’identification Azure de créer](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="bf13e-120">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="centos-73"></a><span data-ttu-id="bf13e-121">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="bf13e-121">CentOS 7.3</span></span>
<span data-ttu-id="bf13e-122">Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="bf13e-122">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="bf13e-123">Hello exemple suivant crée un ordinateur virtuel nommé *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="bf13e-123">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="bf13e-124">SSH à l’aide de machine virtuelle tooyour hello `publicIpAddress` hello figurant à l’opération de création de sortie à partir de la machine virtuelle de hello :</span><span class="sxs-lookup"><span data-stu-id="bf13e-124">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="bf13e-125">Sur votre machine virtuelle, installez les packages hello requis pour les modules du Kit de développement logiciel Azure Python hello et Ansible comme suit :</span><span class="sxs-lookup"><span data-stu-id="bf13e-125">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

<span data-ttu-id="bf13e-126">À présent passer trop[informations d’identification Azure de créer](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="bf13e-126">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="sles-122-sp2"></a><span data-ttu-id="bf13e-127">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="bf13e-127">SLES 12.2 SP2</span></span>
<span data-ttu-id="bf13e-128">Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="bf13e-128">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="bf13e-129">Hello exemple suivant crée un ordinateur virtuel nommé *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="bf13e-129">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="bf13e-130">SSH à l’aide de machine virtuelle tooyour hello `publicIpAddress` hello figurant à l’opération de création de sortie à partir de la machine virtuelle de hello :</span><span class="sxs-lookup"><span data-stu-id="bf13e-130">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="bf13e-131">Sur votre machine virtuelle, installez les packages hello requis pour les modules du Kit de développement logiciel Azure Python hello et Ansible comme suit :</span><span class="sxs-lookup"><span data-stu-id="bf13e-131">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

<span data-ttu-id="bf13e-132">À présent passer trop[informations d’identification Azure de créer](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="bf13e-132">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


## <a name="create-azure-credentials"></a><span data-ttu-id="bf13e-133">Créer des informations d’identification Azure</span><span class="sxs-lookup"><span data-stu-id="bf13e-133">Create Azure credentials</span></span>
<span data-ttu-id="bf13e-134">Ansible communique avec Azure en utilisant un nom d’utilisateur et un mot de passe, ou un principal de service.</span><span class="sxs-lookup"><span data-stu-id="bf13e-134">Ansible communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="bf13e-135">Un principal de service Azure est une identité de sécurité que vous pouvez utiliser avec des applications, des services et des outils d’automatisation comme Ansible.</span><span class="sxs-lookup"><span data-stu-id="bf13e-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Ansible.</span></span> <span data-ttu-id="bf13e-136">Contrôler et de définir des autorisations de hello comme principal du service hello toowhat opérations réalisables dans Azure.</span><span class="sxs-lookup"><span data-stu-id="bf13e-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="bf13e-137">sécurité tooimprove simplement en fournissant un nom d’utilisateur et un mot de passe, cet exemple crée un service de base principale.</span><span class="sxs-lookup"><span data-stu-id="bf13e-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="bf13e-138">Créer un service principal avec [az ad sp créer-de-rbac](/cli/azure/ad/sp#create-for-rbac) et informations d’identification de hello sortie Ansible doit :</span><span class="sxs-lookup"><span data-stu-id="bf13e-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Ansible needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="bf13e-139">Voici un exemple de sortie de hello de hello précédant les commandes :</span><span class="sxs-lookup"><span data-stu-id="bf13e-139">An example of hello output from hello preceding commands is as follows:</span></span>

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

<span data-ttu-id="bf13e-140">tooauthenticate tooAzure, vous devez également tooobtain avec l’ID de votre abonnement Azure [afficher de compte az](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="bf13e-140">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="bf13e-141">Vous utilisez la sortie hello à partir de ces deux commandes à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="bf13e-141">You use hello output from these two commands in hello next step.</span></span>


## <a name="create-ansible-credentials-file"></a><span data-ttu-id="bf13e-142">Créer un fichier d’informations d’identification Ansible</span><span class="sxs-lookup"><span data-stu-id="bf13e-142">Create Ansible credentials file</span></span>
<span data-ttu-id="bf13e-143">tooprovide tooAnsible les informations d’identification, vous définissez les variables d’environnement ou créez un fichier d’informations d’identification locales.</span><span class="sxs-lookup"><span data-stu-id="bf13e-143">tooprovide credentials tooAnsible, you define environment variables or create a local credentials file.</span></span> <span data-ttu-id="bf13e-144">Pour plus d’informations sur la façon de voir des informations d’identification de toodefine Ansible, [fournissant les informations d’identification tooAzure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span><span class="sxs-lookup"><span data-stu-id="bf13e-144">For more information about how toodefine Ansible credentials, see [Providing Credentials tooAzure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span></span> 

<span data-ttu-id="bf13e-145">Pour un environnement de développement, créez un fichier *d’informations d’identification* pour Ansible sur votre machine virtuelle hôte comme suit :</span><span class="sxs-lookup"><span data-stu-id="bf13e-145">For a development environment, create a *credentials* file for Ansible on your host VM as follows:</span></span>

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

<span data-ttu-id="bf13e-146">Hello *informations d’identification* fichier lui-même associe des ID d’abonnement hello sortie hello de création d’un principal de service.</span><span class="sxs-lookup"><span data-stu-id="bf13e-146">hello *credentials* file itself combines hello subscription ID with hello output of creating a service principal.</span></span> <span data-ttu-id="bf13e-147">La sortie à partir de hello précédente [az ad sp créer-de-rbac](/cli/azure/ad/sp#create-for-rbac) commande est la même hello classer en fonction des besoins pour *client_id*, *secret*, et *client* .</span><span class="sxs-lookup"><span data-stu-id="bf13e-147">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *client_id*, *secret*, and *tenant*.</span></span> <span data-ttu-id="bf13e-148">Hello selon exemple *informations d’identification* fichier affiche ces valeurs correspondant à la sortie précédente hello.</span><span class="sxs-lookup"><span data-stu-id="bf13e-148">hello following example *credentials* file shows these values matching hello previous output.</span></span> <span data-ttu-id="bf13e-149">Saisissez vos propres valeurs, comme suit :</span><span class="sxs-lookup"><span data-stu-id="bf13e-149">Enter your own values as follows:</span></span>

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a><span data-ttu-id="bf13e-150">Utiliser des variables d’environnement Ansible</span><span class="sxs-lookup"><span data-stu-id="bf13e-150">Use Ansible environment variables</span></span>
<span data-ttu-id="bf13e-151">Si vous vous apprêtez toouse des outils tels que Ansible tour ou Jenkins, vous pouvez définir des variables d’environnement comme suit.</span><span class="sxs-lookup"><span data-stu-id="bf13e-151">If you are going toouse tools such as Ansible Tower or Jenkins, you can define environment variables as follows.</span></span> <span data-ttu-id="bf13e-152">Ces variables associent des ID d’abonnement hello sortie hello à partir de la création d’un service principal.</span><span class="sxs-lookup"><span data-stu-id="bf13e-152">These variables combine hello subscription ID with hello output from creating a service principal.</span></span> <span data-ttu-id="bf13e-153">Sortie de hello précédente [az ad sp créer-de-rbac](/cli/azure/ad/sp#create-for-rbac) commande est la même hello classer en fonction des besoins pour *AZURE_CLIENT_ID*, *AZURE_SECRET*, et *AZURE_ CLIENT*.</span><span class="sxs-lookup"><span data-stu-id="bf13e-153">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *AZURE_CLIENT_ID*, *AZURE_SECRET*, and *AZURE_TENANT*.</span></span> 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a><span data-ttu-id="bf13e-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bf13e-154">Next steps</span></span>
<span data-ttu-id="bf13e-155">Vous avez maintenant Ansible et hello nécessaire modules Azure Python SDK installés et les informations d’identification définies pour Ansible toouse.</span><span class="sxs-lookup"><span data-stu-id="bf13e-155">You now have Ansible and hello required Azure Python SDK modules installed, and credentials defined for Ansible toouse.</span></span> <span data-ttu-id="bf13e-156">Découvrez comment trop[créer une machine virtuelle avec Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="bf13e-156">Learn how too[create a VM with Ansible](ansible-create-vm.md).</span></span> <span data-ttu-id="bf13e-157">Vous pouvez également apprendre comment trop[créer une machine virtuelle de Azure complète et la prise en charge des ressources avec Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="bf13e-157">You can also learn how too[create a complete Azure VM and supporting resources with Ansible](ansible-create-complete-vm.md).</span></span>
