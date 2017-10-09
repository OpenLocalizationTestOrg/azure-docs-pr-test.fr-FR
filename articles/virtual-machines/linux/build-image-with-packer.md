---
title: aaaHow toocreate Images de machine virtuelle Azure Linux avec compression | Documents Microsoft
description: "Découvrez comment les images toocreate toouse GARNITURE d’ordinateurs virtuels Linux dans Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="b50b3-103">Comment une machine virtuelle Linux toouse GARNITURE toocreate images dans Azure</span><span class="sxs-lookup"><span data-stu-id="b50b3-103">How toouse Packer toocreate Linux virtual machine images in Azure</span></span>
<span data-ttu-id="b50b3-104">Chaque ordinateur virtuel (VM) dans Azure est créé à partir d’une image qui définit hello distribution Linux et la version du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="b50b3-104">Each virtual machine (VM) in Azure is created from an image that defines hello Linux distribution and OS version.</span></span> <span data-ttu-id="b50b3-105">Les images peuvent inclure des configurations et des applications pré-installées.</span><span class="sxs-lookup"><span data-stu-id="b50b3-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="b50b3-106">Hello Azure Marketplace fournit des images de premier et le tiers pour distributions courantes et les environnements de l’application, ou vous pouvez créer vos propres besoins de tooyour adaptés des images personnalisées.</span><span class="sxs-lookup"><span data-stu-id="b50b3-106">hello Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="b50b3-107">Cet article décrit en détail comment toouse hello ouvrir outil source [GARNITURE](https://www.packer.io/) toodefine et créer des images personnalisées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b50b3-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="b50b3-108">Créer un groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="b50b3-108">Create Azure resource group</span></span>
<span data-ttu-id="b50b3-109">Pendant le processus de génération hello, GARNITURE crée des ressources Azure temporaires lorsqu’il crée l’ordinateur virtuel source de hello.</span><span class="sxs-lookup"><span data-stu-id="b50b3-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="b50b3-110">toocapture qui de source pour une utilisation en tant qu’image de machine virtuelle, vous devez définir un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b50b3-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="b50b3-111">Hello sortie à partir de processus de génération du programme de compression hello est stockée dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b50b3-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="b50b3-112">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b50b3-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b50b3-113">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="b50b3-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="b50b3-114">Créer des informations d’identification Azure</span><span class="sxs-lookup"><span data-stu-id="b50b3-114">Create Azure credentials</span></span>
<span data-ttu-id="b50b3-115">Packer s’authentifie auprès d’Azure à l’aide d’un principal de service.</span><span class="sxs-lookup"><span data-stu-id="b50b3-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="b50b3-116">Un principal de service Azure est une identité de sécurité que vous pouvez utiliser avec des applications, des services et des outils d’automatisation comme Packer.</span><span class="sxs-lookup"><span data-stu-id="b50b3-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="b50b3-117">Contrôler et de définir des autorisations de hello comme principal du service hello toowhat opérations réalisables dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b50b3-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="b50b3-118">Créer un service principal avec [az ad sp créer-de-rbac](/cli/azure/ad/sp#create-for-rbac) et informations d’identification de hello sortie GARNITURE doit :</span><span class="sxs-lookup"><span data-stu-id="b50b3-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="b50b3-119">Voici un exemple de sortie de hello de hello précédant les commandes :</span><span class="sxs-lookup"><span data-stu-id="b50b3-119">An example of hello output from hello preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="b50b3-120">tooauthenticate tooAzure, vous devez également tooobtain avec l’ID de votre abonnement Azure [afficher de compte az](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="b50b3-120">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="b50b3-121">Vous utilisez la sortie hello à partir de ces deux commandes à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="b50b3-121">You use hello output from these two commands in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="b50b3-122">Définition du modèle Packer</span><span class="sxs-lookup"><span data-stu-id="b50b3-122">Define Packer template</span></span>
<span data-ttu-id="b50b3-123">toobuild images, vous créez un modèle en tant qu’un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="b50b3-123">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="b50b3-124">Dans le modèle de hello, vous définissez des générateurs et provisioners mener à bien hello réel des processus de génération.</span><span class="sxs-lookup"><span data-stu-id="b50b3-124">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="b50b3-125">Programme de compression a un [un fournisseur pour Azure](https://www.packer.io/docs/builders/azure.html) qui vous permet de toodefine Azure ressources, telles que hello principal des références de service créés dans hello précédant l’étape.</span><span class="sxs-lookup"><span data-stu-id="b50b3-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="b50b3-126">Créez un fichier nommé *ubuntu.json* et coller hello suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="b50b3-126">Create a file named *ubuntu.json* and paste hello following content.</span></span> <span data-ttu-id="b50b3-127">Entrez vos propres valeurs pour les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="b50b3-127">Enter your own values for hello following:</span></span>

| <span data-ttu-id="b50b3-128">Paramètre</span><span class="sxs-lookup"><span data-stu-id="b50b3-128">Parameter</span></span>                           | <span data-ttu-id="b50b3-129">Où tooobtain</span><span class="sxs-lookup"><span data-stu-id="b50b3-129">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="b50b3-130">*client_id*</span><span class="sxs-lookup"><span data-stu-id="b50b3-130">*client_id*</span></span>                         | <span data-ttu-id="b50b3-131">Première ligne de la sortie de la commande create `az ad sp` - *appId*</span><span class="sxs-lookup"><span data-stu-id="b50b3-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="b50b3-132">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="b50b3-132">*client_secret*</span></span>                     | <span data-ttu-id="b50b3-133">Deuxième ligne de la sortie de la commande create `az ad sp` - *password*</span><span class="sxs-lookup"><span data-stu-id="b50b3-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="b50b3-134">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="b50b3-134">*tenant_id*</span></span>                         | <span data-ttu-id="b50b3-135">Troisième ligne de la sortie de la commande create `az ad sp` - *tenant*</span><span class="sxs-lookup"><span data-stu-id="b50b3-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="b50b3-136">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="b50b3-136">*subscription_id*</span></span>                   | <span data-ttu-id="b50b3-137">Sortie de la commande `az account show`</span><span class="sxs-lookup"><span data-stu-id="b50b3-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="b50b3-138">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="b50b3-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="b50b3-139">Nom du groupe de ressources que vous avez créé dans la première étape de hello</span><span class="sxs-lookup"><span data-stu-id="b50b3-139">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="b50b3-140">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="b50b3-140">*managed_image_name*</span></span>                | <span data-ttu-id="b50b3-141">Nom d’image de disque géré hello qui est créé</span><span class="sxs-lookup"><span data-stu-id="b50b3-141">Name for hello managed disk image that is created</span></span> |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

<span data-ttu-id="b50b3-142">Ce modèle génère une image Ubuntu 16.04 LTS, installe NGINX, puis arrête la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="b50b3-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="b50b3-143">Si vous développez ce informations d’identification d’utilisateur tooprovision de modèle, ajuster la commande d’un fournisseur hello qu’arrête hello agent Azure tooread `-deprovision` plutôt que `deprovision+user`.</span><span class="sxs-lookup"><span data-stu-id="b50b3-143">If you expand on this template tooprovision user credentials, adjust hello provisioner command that deprovisions hello Azure agent tooread `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="b50b3-144">Hello `+user` indicateur supprime tous les comptes d’utilisateur de machine virtuelle de la source hello.</span><span class="sxs-lookup"><span data-stu-id="b50b3-144">hello `+user` flag removes all user accounts from hello source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="b50b3-145">Génération de l’image Packer</span><span class="sxs-lookup"><span data-stu-id="b50b3-145">Build Packer image</span></span>
<span data-ttu-id="b50b3-146">Si vous n’avez pas encore installé sur votre ordinateur local, un programme de compression [suivez les instructions d’installation du programme de compression hello](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="b50b3-146">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="b50b3-147">Créer hello image en spécifiant votre programme de compression des fichiers de modèle comme suit :</span><span class="sxs-lookup"><span data-stu-id="b50b3-147">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="b50b3-148">Voici un exemple de sortie de hello de hello précédant les commandes :</span><span class="sxs-lookup"><span data-stu-id="b50b3-148">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="b50b3-149">Création d’une machine virtuelle à partir d’une image Azure</span><span class="sxs-lookup"><span data-stu-id="b50b3-149">Create VM from Azure Image</span></span>
<span data-ttu-id="b50b3-150">Vous pouvez à présent créer une machine virtuelle à partir de votre image à l’aide de la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b50b3-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b50b3-151">Spécifiez hello Image que vous avez créé avec hello `--image` paramètre.</span><span class="sxs-lookup"><span data-stu-id="b50b3-151">Specify hello Image you created with hello `--image` parameter.</span></span> <span data-ttu-id="b50b3-152">Hello exemple suivant crée un ordinateur virtuel nommé *myVM* de *myPackerImage* et génère des clés SSH s’ils n’existent pas déjà :</span><span class="sxs-lookup"><span data-stu-id="b50b3-152">hello following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="b50b3-153">Il prend quelques minutes de toocreate hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b50b3-153">It takes a few minutes toocreate hello VM.</span></span> <span data-ttu-id="b50b3-154">Une fois que hello machine virtuelle a été créé, prenez note de hello `publicIpAddress` affiché par hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b50b3-154">Once hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="b50b3-155">Cette adresse est un site NGINX hello tooaccess utilisées via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="b50b3-155">This address is used tooaccess hello NGINX site via a web browser.</span></span>

<span data-ttu-id="b50b3-156">tooallow web tooreach de trafic de votre machine virtuelle, ouvrez port 80 du hello Internet avec [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="b50b3-156">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="b50b3-157">Test de la machine virtuelle et de NGINX</span><span class="sxs-lookup"><span data-stu-id="b50b3-157">Test VM and NGINX</span></span>
<span data-ttu-id="b50b3-158">Vous pouvez désormais ouvrir un navigateur web et entrez `http://publicIpAddress` dans la barre d’adresses hello.</span><span class="sxs-lookup"><span data-stu-id="b50b3-158">Now you can open a web browser and enter `http://publicIpAddress` in hello address bar.</span></span> <span data-ttu-id="b50b3-159">Fournissez vos propres adresse IP à partir de la machine virtuelle de hello créer le processus.</span><span class="sxs-lookup"><span data-stu-id="b50b3-159">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="b50b3-160">page NGINX Hello par défaut s’affiche comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b50b3-160">hello default NGINX page is displayed as in hello following example:</span></span>

![Site par défaut NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="b50b3-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b50b3-162">Next steps</span></span>
<span data-ttu-id="b50b3-163">Dans cet exemple, vous avez utilisé le programme de compression toocreate une image de machine virtuelle avec NGINX déjà installé.</span><span class="sxs-lookup"><span data-stu-id="b50b3-163">In this example, you used Packer toocreate a VM image with NGINX already installed.</span></span> <span data-ttu-id="b50b3-164">Vous pouvez utiliser cette image de machine virtuelle en même temps que les workflows existants de déploiement, telles que toodeploy tooVMs de votre application créé à partir de hello Image avec Ansible, Chef ou Puppet.</span><span class="sxs-lookup"><span data-stu-id="b50b3-164">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="b50b3-165">Pour obtenir d’autres exemples de modèles Packer pour d’autres distributions Linux, consultez [ce référentiel GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="b50b3-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>