---
title: aaaHow toocreate Images de machine virtuelle Windows Azure avec compression | Documents Microsoft
description: "Découvrez comment les images toocreate toouse garniture de machines virtuelles Windows Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: d310fae3becb453b52d21281cb8ac53fa14a3fc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-windows-virtual-machine-images-in-azure"></a><span data-ttu-id="2eaf3-103">Comment l’image de machine virtuelle de toouse GARNITURE toocreate Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="2eaf3-103">How toouse Packer toocreate Windows virtual machine images in Azure</span></span>
<span data-ttu-id="2eaf3-104">Chaque ordinateur virtuel (VM) dans Azure est créé à partir d’une image qui définit hello distribution Windows et la version du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-104">Each virtual machine (VM) in Azure is created from an image that defines hello Windows distribution and OS version.</span></span> <span data-ttu-id="2eaf3-105">Les images peuvent inclure des configurations et des applications pré-installées.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="2eaf3-106">Hello Azure Marketplace fournit de nombreuses images premier et le tiers pour courants du système d’exploitation et environnements d’application, ou vous pouvez créer vos propres besoins de tooyour adaptés des images personnalisées.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-106">hello Azure Marketplace provides many first and third-party images for most common OS' and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="2eaf3-107">Cet article décrit en détail comment toouse hello ouvrir outil source [GARNITURE](https://www.packer.io/) toodefine et créer des images personnalisées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="2eaf3-108">Créer un groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="2eaf3-108">Create Azure resource group</span></span>
<span data-ttu-id="2eaf3-109">Pendant le processus de génération hello, GARNITURE crée des ressources Azure temporaires lorsqu’il crée l’ordinateur virtuel source de hello.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="2eaf3-110">toocapture qui de source pour une utilisation en tant qu’image de machine virtuelle, vous devez définir un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="2eaf3-111">Hello sortie à partir de processus de génération du programme de compression hello est stockée dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="2eaf3-112">Créez un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="2eaf3-112">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="2eaf3-113">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="2eaf3-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a><span data-ttu-id="2eaf3-114">Créer des informations d’identification Azure</span><span class="sxs-lookup"><span data-stu-id="2eaf3-114">Create Azure credentials</span></span>
<span data-ttu-id="2eaf3-115">Packer s’authentifie auprès d’Azure à l’aide d’un principal de service.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="2eaf3-116">Un principal de service Azure est une identité de sécurité que vous pouvez utiliser avec des applications, des services et des outils d’automatisation comme Packer.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="2eaf3-117">Contrôler et de définir des autorisations de hello comme principal du service hello toowhat opérations réalisables dans Azure.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="2eaf3-118">Créer un service principal avec [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) et attribuer des autorisations pour toocreate principal du service hello et gérer les ressources avec [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span><span class="sxs-lookup"><span data-stu-id="2eaf3-118">Create a service principal with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) and assign permissions for hello service principal toocreate and manage resources with [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span></span>

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="2eaf3-119">tooauthenticate tooAzure, vous devez également tooobtain votre ID client et un abonnement Azure avec [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span><span class="sxs-lookup"><span data-stu-id="2eaf3-119">tooauthenticate tooAzure, you also need tooobtain your Azure tenant and subscription IDs with [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span></span>

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

<span data-ttu-id="2eaf3-120">Vous utilisez ces deux ID à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-120">You use these two IDs in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="2eaf3-121">Définition du modèle Packer</span><span class="sxs-lookup"><span data-stu-id="2eaf3-121">Define Packer template</span></span>
<span data-ttu-id="2eaf3-122">toobuild images, vous créez un modèle en tant qu’un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-122">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="2eaf3-123">Dans le modèle de hello, vous définissez des générateurs et provisioners mener à bien hello réel des processus de génération.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-123">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="2eaf3-124">Programme de compression a un [un fournisseur pour Azure](https://www.packer.io/docs/builders/azure.html) qui vous permet de toodefine Azure ressources, telles que hello principal des références de service créés dans hello précédant l’étape.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-124">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="2eaf3-125">Créez un fichier nommé *windows.json* et coller hello suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-125">Create a file named *windows.json* and paste hello following content.</span></span> <span data-ttu-id="2eaf3-126">Entrez vos propres valeurs pour les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="2eaf3-126">Enter your own values for hello following:</span></span>

| <span data-ttu-id="2eaf3-127">Paramètre</span><span class="sxs-lookup"><span data-stu-id="2eaf3-127">Parameter</span></span>                           | <span data-ttu-id="2eaf3-128">Où tooobtain</span><span class="sxs-lookup"><span data-stu-id="2eaf3-128">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="2eaf3-129">*client_id*</span><span class="sxs-lookup"><span data-stu-id="2eaf3-129">*client_id*</span></span>                         | <span data-ttu-id="2eaf3-130">Affichage de l’ID du principal de service avec `$sp.applicationId`</span><span class="sxs-lookup"><span data-stu-id="2eaf3-130">View service principal ID with `$sp.applicationId`</span></span> |
| <span data-ttu-id="2eaf3-131">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="2eaf3-131">*client_secret*</span></span>                     | <span data-ttu-id="2eaf3-132">Mot de passe que vous avez spécifié dans `$securePassword`</span><span class="sxs-lookup"><span data-stu-id="2eaf3-132">Password you specified in `$securePassword`</span></span> |
| <span data-ttu-id="2eaf3-133">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="2eaf3-133">*tenant_id*</span></span>                         | <span data-ttu-id="2eaf3-134">Sortie de la commande `$sub.TenantId`</span><span class="sxs-lookup"><span data-stu-id="2eaf3-134">Output from `$sub.TenantId` command</span></span> |
| <span data-ttu-id="2eaf3-135">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="2eaf3-135">*subscription_id*</span></span>                   | <span data-ttu-id="2eaf3-136">Sortie de la commande `$sub.SubscriptionId`</span><span class="sxs-lookup"><span data-stu-id="2eaf3-136">Output from `$sub.SubscriptionId` command</span></span> |
| <span data-ttu-id="2eaf3-137">*object_id*</span><span class="sxs-lookup"><span data-stu-id="2eaf3-137">*object_id*</span></span>                         | <span data-ttu-id="2eaf3-138">Affichage de l’ID d’objet du principal de service avec `$sp.Id`</span><span class="sxs-lookup"><span data-stu-id="2eaf3-138">View service principal object ID with `$sp.Id`</span></span> |
| <span data-ttu-id="2eaf3-139">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="2eaf3-139">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="2eaf3-140">Nom du groupe de ressources que vous avez créé dans la première étape de hello</span><span class="sxs-lookup"><span data-stu-id="2eaf3-140">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="2eaf3-141">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="2eaf3-141">*managed_image_name*</span></span>                | <span data-ttu-id="2eaf3-142">Nom d’image de disque géré hello qui est créé</span><span class="sxs-lookup"><span data-stu-id="2eaf3-142">Name for hello managed disk image that is created</span></span> |

```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "0831b578-8ab6-40b9-a581-9a880a94aab1",
    "client_secret": "P@ssw0rd!",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",
    "object_id": "a7dfb070-0d5b-47ac-b9a5-cf214fff0ae2",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Windows",
    "image_publisher": "MicrosoftWindowsServer",
    "image_offer": "WindowsServer",
    "image_sku": "2016-Datacenter",

    "communicator": "winrm",
    "winrm_use_ssl": "true",
    "winrm_insecure": "true",
    "winrm_timeout": "3m",
    "winrm_username": "packer",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "type": "powershell",
    "inline": [
      "Add-WindowsFeature Web-Server",
      "if( Test-Path $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml ){ rm $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml -Force}",
      "& $Env:SystemRoot\\System32\\Sysprep\\Sysprep.exe /oobe /generalize /shutdown /quiet"
    ]
  }]
}
```

<span data-ttu-id="2eaf3-143">Ce modèle génère un ordinateur Windows Server 2016, installe les services IIS, puis généralise hello machine virtuelle avec Sysprep.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-143">This template builds a Windows Server 2016 VM, installs IIS, then generalizes hello VM with Sysprep.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="2eaf3-144">Génération de l’image Packer</span><span class="sxs-lookup"><span data-stu-id="2eaf3-144">Build Packer image</span></span>
<span data-ttu-id="2eaf3-145">Si vous n’avez pas encore installé sur votre ordinateur local, un programme de compression [suivez les instructions d’installation du programme de compression hello](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="2eaf3-145">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="2eaf3-146">Créer hello image en spécifiant votre programme de compression des fichiers de modèle comme suit :</span><span class="sxs-lookup"><span data-stu-id="2eaf3-146">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build windows.json
```

<span data-ttu-id="2eaf3-147">Voici un exemple de sortie de hello de hello précédant les commandes :</span><span class="sxs-lookup"><span data-stu-id="2eaf3-147">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> task : Image deployment
==> azure-arm:  ->> dept : Engineering
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting hello certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM toobecome available...
==> azure-arm: Connected tooWinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-pq0mthtbtt/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Compute Name              : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

<span data-ttu-id="2eaf3-148">Il prend quelques minutes pour hello toobuild de programme de compression machine virtuelle, exécutez provisioners de hello, installation et de nettoyage hello déploiement.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-148">It takes a few minutes for Packer toobuild hello VM, run hello provisioners, and clean up hello deployment.</span></span>


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="2eaf3-149">Création d’une machine virtuelle à partir d’une image Azure</span><span class="sxs-lookup"><span data-stu-id="2eaf3-149">Create VM from Azure Image</span></span>
<span data-ttu-id="2eaf3-150">Définir un administrateur de nom d’utilisateur et mot de passe pour les machines virtuelles hello avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span><span class="sxs-lookup"><span data-stu-id="2eaf3-150">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="2eaf3-151">Vous pouvez à présent créer une machine virtuelle à partir de votre image à l’aide de la commande [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="2eaf3-151">You can now create a VM from your Image with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="2eaf3-152">Hello exemple suivant crée un ordinateur virtuel nommé *myVM* de *myPackerImage*.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-152">hello following example creates a VM named *myVM* from *myPackerImage*.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod "Static" `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Define hello image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

<span data-ttu-id="2eaf3-153">Il prend quelques minutes de toocreate hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-153">It takes a few minutes toocreate hello VM.</span></span>


## <a name="test-vm-and-iis"></a><span data-ttu-id="2eaf3-154">Test de la machine virtuelle et d’IIS</span><span class="sxs-lookup"><span data-stu-id="2eaf3-154">Test VM and IIS</span></span>
<span data-ttu-id="2eaf3-155">Obtenir hello une adresse IP publique de votre machine virtuelle avec [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="2eaf3-155">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="2eaf3-156">exemple Hello obtient adresse IP hello *myPublicIP* créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="2eaf3-156">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="2eaf3-157">Vous pouvez entrer ensuite des adresse IP publique de hello dans tooa navigateur.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-157">You can then enter hello public IP address in tooa web browser.</span></span>

![Site IIS par défaut](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a><span data-ttu-id="2eaf3-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2eaf3-159">Next steps</span></span>
<span data-ttu-id="2eaf3-160">Dans cet exemple, vous avez utilisé le programme de compression toocreate une image de machine virtuelle avec IIS est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-160">In this example, you used Packer toocreate a VM image with IIS already installed.</span></span> <span data-ttu-id="2eaf3-161">Vous pouvez utiliser cette image de machine virtuelle en même temps que les workflows existants de déploiement, telles que toodeploy tooVMs de votre application créé à partir de hello Image avec Team Services, Ansible, Chef ou Puppet.</span><span class="sxs-lookup"><span data-stu-id="2eaf3-161">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Team Services, Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="2eaf3-162">Pour obtenir d’autres exemples de modèles Packer pour d’autres distributions Windows, consultez [ce référentiel GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="2eaf3-162">For additional example Packer templates for other Windows distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>