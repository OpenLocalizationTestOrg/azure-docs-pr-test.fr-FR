---
title: "aaaCreate et télécharger un VM OpenBSD image tooAzure | Documents Microsoft"
description: "Découvrez comment toocreate et téléchargez un disque dur virtuel (VHD) qui contient hello toocreate du système d’exploitation OpenBSD une machine virtuelle Azure via l’interface CLI d’Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a><span data-ttu-id="b84b9-103">Créer et télécharger un tooAzure d’image de disque OpenBSD</span><span class="sxs-lookup"><span data-stu-id="b84b9-103">Create and Upload an OpenBSD disk image tooAzure</span></span>
<span data-ttu-id="b84b9-104">Cet article vous explique comment toocreate et téléchargez un disque dur virtuel (VHD) qui contient hello système d’exploitation de OpenBSD.</span><span class="sxs-lookup"><span data-stu-id="b84b9-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello OpenBSD operating system.</span></span> <span data-ttu-id="b84b9-105">Après que l’avoir téléchargée, vous pouvez l’utiliser en tant que vos propres toocreate image un ordinateur virtuel (VM) dans Azure via l’interface CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b84b9-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b84b9-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b84b9-106">Prerequisites</span></span>
<span data-ttu-id="b84b9-107">Cet article suppose que vous avez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b84b9-107">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="b84b9-108">**Abonnement Azure** : si vous ne possédez pas de compte, vous pouvez en créer un en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="b84b9-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="b84b9-109">Si vous disposez d’un abonnement MSDN, consultez [Crédit Azure mensuel pour les abonnés Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="b84b9-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="b84b9-110">Dans le cas contraire, découvrez comment trop[créer un compte d’évaluation gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b84b9-110">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="b84b9-111">**Azure CLI 2.0** -Assurez-vous que vous avez hello dernières [Azure CLI 2.0](/cli/azure/install-azure-cli) installé et connecté tooyour compte Azure avec [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b84b9-111">**Azure CLI 2.0** - Make sure you have hello latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in tooyour Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="b84b9-112">**Système d’exploitation OpenBSD dans un fichier .vhd** -un système d’exploitation pris en charge OpenBSD (6.1 version) doit être installé tooa un disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="b84b9-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="b84b9-113">Plusieurs outils existent toocreate les fichiers .vhd.</span><span class="sxs-lookup"><span data-stu-id="b84b9-113">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="b84b9-114">Par exemple, vous pouvez utiliser une solution de virtualisation tels que les fichiers de disque dur virtuel Hyper-V toocreate hello et installer le système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="b84b9-114">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="b84b9-115">Pour obtenir des instructions sur la façon dont tooinstall et l’utilisation de Hyper-V, consultez [installer Hyper-V et créer une machine virtuelle](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="b84b9-115">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="b84b9-116">Préparer l’image OpenBSD pour Azure</span><span class="sxs-lookup"><span data-stu-id="b84b9-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="b84b9-117">Sur hello VM où vous avez installé hello OpenBSD système d’exploitation 6.1, qui prend en charge Hyper-V, exécutez hello procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="b84b9-117">On hello VM where you installed hello OpenBSD operating system 6.1, which added Hyper-V support, complete hello following procedures:</span></span>

1. <span data-ttu-id="b84b9-118">Si DHCP n’est pas activée lors de l’installation, activez le service de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b84b9-118">If DHCP is not enabled during installation, enable hello service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="b84b9-119">Configurez une console série comme suit :</span><span class="sxs-lookup"><span data-stu-id="b84b9-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="b84b9-120">Configurez l’installation du package comme suit :</span><span class="sxs-lookup"><span data-stu-id="b84b9-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="b84b9-121">Par défaut, hello `root` utilisateur est désactivé sur les ordinateurs virtuels dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b84b9-121">By default, hello `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="b84b9-122">Les utilisateurs peuvent exécuter des commandes avec des privilèges élevés à l’aide de hello `doas` commande OpenBSD VM.</span><span class="sxs-lookup"><span data-stu-id="b84b9-122">Users can run commands with elevated privileges by using hello `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="b84b9-123">Doas est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="b84b9-123">Doas is enabled by default.</span></span> <span data-ttu-id="b84b9-124">Pour plus d’informations, voir [doas.conf](http://man.openbsd.org/doas.conf.5).</span><span class="sxs-lookup"><span data-stu-id="b84b9-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="b84b9-125">Installer et configurer les conditions préalables pour hello Azure Agent comme suit :</span><span class="sxs-lookup"><span data-stu-id="b84b9-125">Install and configure prerequisites for hello Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="b84b9-126">version la plus récente de hello agent Azure Hello se trouvent toujours sur [Github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="b84b9-126">hello latest release of hello Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="b84b9-127">Installez l’agent de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b84b9-127">Install hello agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b84b9-128">Après avoir installé l’Agent Azure, il est tooverify une bonne idée qu’elle s’exécute comme suit :</span><span class="sxs-lookup"><span data-stu-id="b84b9-128">After you install Azure Agent, it's a good idea tooverify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="b84b9-129">Annuler le déploiement hello système tooclean et elle est adaptée à la préparation.</span><span class="sxs-lookup"><span data-stu-id="b84b9-129">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="b84b9-130">Hello commande suivante supprime également dernier compte d’utilisateur configuré hello et les données de salutation associée :</span><span class="sxs-lookup"><span data-stu-id="b84b9-130">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="b84b9-131">Vous pouvez à présent arrêter votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b84b9-131">Now you can shut down your VM.</span></span>


## <a name="prepare-hello-vhd"></a><span data-ttu-id="b84b9-132">Préparer hello disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="b84b9-132">Prepare hello VHD</span></span>
<span data-ttu-id="b84b9-133">format VHDX Hello n'est pas pris en charge dans Azure, uniquement **disque dur virtuel fixe**.</span><span class="sxs-lookup"><span data-stu-id="b84b9-133">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="b84b9-134">Vous pouvez convertir le format de disque dur virtuel hello disque toofixed à l’aide du Gestionnaire Hyper-V ou hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b84b9-134">You can convert hello disk toofixed VHD format using Hyper-V Manager or hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="b84b9-135">Voici un exemple.</span><span class="sxs-lookup"><span data-stu-id="b84b9-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="b84b9-136">Créer des ressources de stockage et charger</span><span class="sxs-lookup"><span data-stu-id="b84b9-136">Create storage resources and upload</span></span>
<span data-ttu-id="b84b9-137">Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b84b9-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b84b9-138">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="b84b9-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="b84b9-139">tooupload votre disque dur virtuel, créez un compte de stockage avec [créer de compte de stockage az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="b84b9-139">tooupload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="b84b9-140">Le nom du compte de stockage devant être unique, entrez votre propre nom.</span><span class="sxs-lookup"><span data-stu-id="b84b9-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="b84b9-141">Hello exemple suivant crée un compte de stockage nommé *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="b84b9-141">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="b84b9-142">toocontrol accéder au compte de stockage toohello, d’obtenir la clé de stockage hello avec [liste de clés de compte de stockage az](/cli/azure/storage/account/keys#list) comme suit :</span><span class="sxs-lookup"><span data-stu-id="b84b9-142">toocontrol access toohello storage account, obtain hello storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="b84b9-143">hello distinct de toologically disques durs virtuels que vous téléchargez, créer un conteneur dans le compte de stockage hello avec [créer de conteneur de stockage az](/cli/azure/storage/container#create):</span><span class="sxs-lookup"><span data-stu-id="b84b9-143">toologically separate hello VHDs you upload, create a container within hello storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="b84b9-144">Enfin, chargez votre disque dur virtuel avec la commande [az storage blob upload](/cli/azure/storage/blob#upload) comme suit :</span><span class="sxs-lookup"><span data-stu-id="b84b9-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="b84b9-145">Créer la machine virtuelle à partir de votre disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="b84b9-145">Create VM from your VHD</span></span>
<span data-ttu-id="b84b9-146">Vous pouvez créer une machine virtuelle avec un [exemple de script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) ou directement avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b84b9-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b84b9-147">toospecify hello des VHD OpenBSD vous avez téléchargé, utilisez hello `--image` paramètre comme suit :</span><span class="sxs-lookup"><span data-stu-id="b84b9-147">toospecify hello OpenBSD VHD you uploaded, use hello `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="b84b9-148">Obtenir l’adresse IP de hello pour votre VM OpenBSD avec [az vm liste-ip-addresses](/cli/azure/vm#list-ip-addresses) comme suit :</span><span class="sxs-lookup"><span data-stu-id="b84b9-148">Obtain hello IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="b84b9-149">Vous pouvez désormais SSH tooyour OpenBSD VM normalement :</span><span class="sxs-lookup"><span data-stu-id="b84b9-149">Now you can SSH tooyour OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="b84b9-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b84b9-150">Next steps</span></span>
<span data-ttu-id="b84b9-151">Si vous souhaitez tooknow plus d’informations sur Hyper-V prend en charge sur OpenBSD6.1, lisez [OpenBSD 6.1](https://www.openbsd.org/61.html) et [hyperv.4](http://man.openbsd.org/hyperv.4).</span><span class="sxs-lookup"><span data-stu-id="b84b9-151">If you want tooknow more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="b84b9-152">Si vous souhaitez toocreate une machine virtuelle à partir de disque géré, lisez [disque de az](/cli/azure/disk).</span><span class="sxs-lookup"><span data-stu-id="b84b9-152">If you want toocreate a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 
