---
title: "Comment créer des images de machines virtuelles Azure Linux avec Packer | Microsoft Docs"
description: "Découvrez comment utiliser Packer pour créer des images de machines virtuelles Linux dans Azure"
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
ms.openlocfilehash: 49a74648bd3953647d581c4e7c548985c5000f17
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-packer-to-create-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="937b3-103">Comment utiliser Packer pour créer des images de machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="937b3-103">How to use Packer to create Linux virtual machine images in Azure</span></span>
<span data-ttu-id="937b3-104">Chaque machine virtuelle dans Azure est créée à partir d’une image qui définit la distribution Linux et la version du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="937b3-104">Each virtual machine (VM) in Azure is created from an image that defines the Linux distribution and OS version.</span></span> <span data-ttu-id="937b3-105">Les images peuvent inclure des configurations et des applications pré-installées.</span><span class="sxs-lookup"><span data-stu-id="937b3-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="937b3-106">La Place de marché Microsoft Azure fournit de nombreuses images internes et de tiers pour les distributions et environnements d’application les plus courants. Vous pouvez également créer vos propres images personnalisées selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="937b3-106">The Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored to your needs.</span></span> <span data-ttu-id="937b3-107">Cet article explique comment utiliser l’outil open source [Packer](https://www.packer.io/) pour définir et générer des images personnalisées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="937b3-107">This article details how to use the open source tool [Packer](https://www.packer.io/) to define and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="937b3-108">Créer un groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="937b3-108">Create Azure resource group</span></span>
<span data-ttu-id="937b3-109">Pendant le processus de génération, Packer crée des ressources Azure temporaires lorsqu’il génère la machine virtuelle source.</span><span class="sxs-lookup"><span data-stu-id="937b3-109">During the build process, Packer creates temporary Azure resources as it builds the source VM.</span></span> <span data-ttu-id="937b3-110">Pour capturer cette machine virtuelle source afin de l’utiliser en tant qu’image, vous devez définir un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="937b3-110">To capture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="937b3-111">La sortie du processus de génération Packer est stockée dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="937b3-111">The output from the Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="937b3-112">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="937b3-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="937b3-113">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *eastus* :</span><span class="sxs-lookup"><span data-stu-id="937b3-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="937b3-114">Créer des informations d’identification Azure</span><span class="sxs-lookup"><span data-stu-id="937b3-114">Create Azure credentials</span></span>
<span data-ttu-id="937b3-115">Packer s’authentifie auprès d’Azure à l’aide d’un principal de service.</span><span class="sxs-lookup"><span data-stu-id="937b3-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="937b3-116">Un principal de service Azure est une identité de sécurité que vous pouvez utiliser avec des applications, des services et des outils d’automatisation comme Packer.</span><span class="sxs-lookup"><span data-stu-id="937b3-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="937b3-117">Vous contrôlez et définissez les opérations que le principal de service est autorisé à effectuer dans Azure.</span><span class="sxs-lookup"><span data-stu-id="937b3-117">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span>

<span data-ttu-id="937b3-118">Créez un principal de service avec la commande [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) et affichez les informations d’identification nécessaires à Packer :</span><span class="sxs-lookup"><span data-stu-id="937b3-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="937b3-119">Voici un exemple de sortie issue des commandes précédentes :</span><span class="sxs-lookup"><span data-stu-id="937b3-119">An example of the output from the preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="937b3-120">Pour s’authentifier sur Azure, vous devez également obtenir votre ID d’abonnement Azure avec [az account show](/cli/azure/account#show) :</span><span class="sxs-lookup"><span data-stu-id="937b3-120">To authenticate to Azure, you also need to obtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="937b3-121">Vous utiliserez la sortie de ces deux commandes à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="937b3-121">You use the output from these two commands in the next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="937b3-122">Définition du modèle Packer</span><span class="sxs-lookup"><span data-stu-id="937b3-122">Define Packer template</span></span>
<span data-ttu-id="937b3-123">Pour générer les images, vous devez créer un modèle en tant que fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="937b3-123">To build images, you create a template as a JSON file.</span></span> <span data-ttu-id="937b3-124">Dans le modèle, vous définissez des générateurs et des fournisseurs pour mener à bien le processus de génération réel.</span><span class="sxs-lookup"><span data-stu-id="937b3-124">In the template, you define builders and provisioners that carry out the actual build process.</span></span> <span data-ttu-id="937b3-125">Packer possède un [fournisseur pour Azure](https://www.packer.io/docs/builders/azure.html) qui vous permet de définir des ressources Azure, telles que les informations d’identification du principal de service créées à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="937b3-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you to define Azure resources, such as the service principal credentials created in the preceding step.</span></span>

<span data-ttu-id="937b3-126">Créez un fichier nommé *ubuntu.json* et collez le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="937b3-126">Create a file named *ubuntu.json* and paste the following content.</span></span> <span data-ttu-id="937b3-127">Saisissez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="937b3-127">Enter your own values for the following:</span></span>

| <span data-ttu-id="937b3-128">Paramètre</span><span class="sxs-lookup"><span data-stu-id="937b3-128">Parameter</span></span>                           | <span data-ttu-id="937b3-129">Emplacement</span><span class="sxs-lookup"><span data-stu-id="937b3-129">Where to obtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="937b3-130">*client_id*</span><span class="sxs-lookup"><span data-stu-id="937b3-130">*client_id*</span></span>                         | <span data-ttu-id="937b3-131">Première ligne de la sortie de la commande create `az ad sp` - *appId*</span><span class="sxs-lookup"><span data-stu-id="937b3-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="937b3-132">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="937b3-132">*client_secret*</span></span>                     | <span data-ttu-id="937b3-133">Deuxième ligne de la sortie de la commande create `az ad sp` - *password*</span><span class="sxs-lookup"><span data-stu-id="937b3-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="937b3-134">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="937b3-134">*tenant_id*</span></span>                         | <span data-ttu-id="937b3-135">Troisième ligne de la sortie de la commande create `az ad sp` - *tenant*</span><span class="sxs-lookup"><span data-stu-id="937b3-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="937b3-136">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="937b3-136">*subscription_id*</span></span>                   | <span data-ttu-id="937b3-137">Sortie de la commande `az account show`</span><span class="sxs-lookup"><span data-stu-id="937b3-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="937b3-138">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="937b3-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="937b3-139">Nom du groupe de ressources créé lors de la première étape</span><span class="sxs-lookup"><span data-stu-id="937b3-139">Name of resource group you created in the first step</span></span> |
| <span data-ttu-id="937b3-140">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="937b3-140">*managed_image_name*</span></span>                | <span data-ttu-id="937b3-141">Nom de l’image de disque géré créée</span><span class="sxs-lookup"><span data-stu-id="937b3-141">Name for the managed disk image that is created</span></span> |


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

<span data-ttu-id="937b3-142">Ce modèle génère une image Ubuntu 16.04 LTS, installe NGINX, puis déprovisionne la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="937b3-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="937b3-143">Si vous développez ce modèle pour approvisionner les informations d’identification utilisateur, définissez la commande du fournisseur qui déprovisionne l’agent Azure de sorte qu’elle indique `-deprovision` et non `deprovision+user`.</span><span class="sxs-lookup"><span data-stu-id="937b3-143">If you expand on this template to provision user credentials, adjust the provisioner command that deprovisions the Azure agent to read `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="937b3-144">L’indicateur `+user` supprime tous les comptes d’utilisateur de la machine virtuelle source.</span><span class="sxs-lookup"><span data-stu-id="937b3-144">The `+user` flag removes all user accounts from the source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="937b3-145">Génération de l’image Packer</span><span class="sxs-lookup"><span data-stu-id="937b3-145">Build Packer image</span></span>
<span data-ttu-id="937b3-146">Si Packer n’est pas encore installé sur votre ordinateur local, [suivez les instructions d’installation de Packer](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="937b3-146">If you don't already have Packer installed on your local machine, [follow the Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="937b3-147">Générez l’image en spécifiant votre fichier de modèle Packer comme suit :</span><span class="sxs-lookup"><span data-stu-id="937b3-147">Build the image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="937b3-148">Voici un exemple de la sortie des commandes précédentes :</span><span class="sxs-lookup"><span data-stu-id="937b3-148">An example of the output from the preceding commands is as follows:</span></span>

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
==> azure-arm: Getting the VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH to become available...
==> azure-arm: Connected to SSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! The waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able to login as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying the machine’s properties ...
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
==> azure-arm: Deleting the temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. The artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="937b3-149">Création d’une machine virtuelle à partir d’une image Azure</span><span class="sxs-lookup"><span data-stu-id="937b3-149">Create VM from Azure Image</span></span>
<span data-ttu-id="937b3-150">Vous pouvez à présent créer une machine virtuelle à partir de votre image à l’aide de la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="937b3-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="937b3-151">Spécifiez l’image que vous avez créée avec le paramètre `--image`.</span><span class="sxs-lookup"><span data-stu-id="937b3-151">Specify the Image you created with the `--image` parameter.</span></span> <span data-ttu-id="937b3-152">L’exemple suivant crée une machine virtuelle nommée *myVM* à partir de *myPackerImage* et génère des clés SSH si elles n’existent pas déjà :</span><span class="sxs-lookup"><span data-stu-id="937b3-152">The following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="937b3-153">La création de la machine virtuelle ne nécessite que quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="937b3-153">It takes a few minutes to create the VM.</span></span> <span data-ttu-id="937b3-154">Une fois la machine virtuelle créée, notez la valeur de `publicIpAddress` qui s’affiche dans l’interface Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="937b3-154">Once the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="937b3-155">Cette adresse est utilisée pour accéder au site NGINX à l’aide d’un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="937b3-155">This address is used to access the NGINX site via a web browser.</span></span>

<span data-ttu-id="937b3-156">Pour autoriser le trafic web à accéder à votre machine virtuelle, ouvrez le port 80 à partir d’Internet à l’aide de la commande [az vm open-port](/cli/azure/vm#open-port) :</span><span class="sxs-lookup"><span data-stu-id="937b3-156">To allow web traffic to reach your VM, open port 80 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="937b3-157">Test de la machine virtuelle et de NGINX</span><span class="sxs-lookup"><span data-stu-id="937b3-157">Test VM and NGINX</span></span>
<span data-ttu-id="937b3-158">Vous pouvez maintenant ouvrir un navigateur web et entrer `http://publicIpAddress` dans la barre d’adresse.</span><span class="sxs-lookup"><span data-stu-id="937b3-158">Now you can open a web browser and enter `http://publicIpAddress` in the address bar.</span></span> <span data-ttu-id="937b3-159">Indiquez votre propre adresse IP publique à partir du processus de création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="937b3-159">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="937b3-160">La page NGINX par défaut s’affiche comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="937b3-160">The default NGINX page is displayed as in the following example:</span></span>

![Site par défaut NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="937b3-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="937b3-162">Next steps</span></span>
<span data-ttu-id="937b3-163">Dans cet exemple, NGINX était déjà installé et vous avez utilisé Packer pour créer une image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="937b3-163">In this example, you used Packer to create a VM image with NGINX already installed.</span></span> <span data-ttu-id="937b3-164">Vous pouvez utiliser cette image de machine virtuelle avec les flux de travail de déploiement existants, par exemple pour déployer votre application sur les machines virtuelles créées à partir de l’image avec Ansible, Chef ou Puppet.</span><span class="sxs-lookup"><span data-stu-id="937b3-164">You can use this VM image alongside existing deployment workflows, such as to deploy your app to VMs created from the Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="937b3-165">Pour obtenir d’autres exemples de modèles Packer pour d’autres distributions Linux, consultez [ce référentiel GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="937b3-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>