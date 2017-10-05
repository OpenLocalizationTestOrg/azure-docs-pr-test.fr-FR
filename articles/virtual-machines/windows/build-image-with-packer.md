---
title: "Comment créer des images de machines virtuelles Microsoft Azure avec Packer | Microsoft Docs"
description: "Découvrez comment utiliser Packer pour créer des images de machines virtuelles Windows dans Azure"
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
ms.openlocfilehash: 11a4a4d65be09e6c518836c25bb455a6df738dcb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-packer-to-create-windows-virtual-machine-images-in-azure"></a><span data-ttu-id="98d03-103">Comment utiliser Packer pour créer des images de machines virtuelles Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="98d03-103">How to use Packer to create Windows virtual machine images in Azure</span></span>
<span data-ttu-id="98d03-104">Chaque machine virtuelle dans Azure est créée à partir d’une image qui définit la distribution Windows et la version du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="98d03-104">Each virtual machine (VM) in Azure is created from an image that defines the Windows distribution and OS version.</span></span> <span data-ttu-id="98d03-105">Les images peuvent inclure des configurations et des applications pré-installées.</span><span class="sxs-lookup"><span data-stu-id="98d03-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="98d03-106">La Place de marché Microsoft Azure fournit de nombreuses images internes et de tiers pour les systèmes d’exploitation et environnements d’application les plus courants. Vous pouvez également créer vos propres images personnalisées selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="98d03-106">The Azure Marketplace provides many first and third-party images for most common OS' and application environments, or you can create your own custom images tailored to your needs.</span></span> <span data-ttu-id="98d03-107">Cet article explique comment utiliser l’outil open source [Packer](https://www.packer.io/) pour définir et générer des images personnalisées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="98d03-107">This article details how to use the open source tool [Packer](https://www.packer.io/) to define and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="98d03-108">Créer un groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="98d03-108">Create Azure resource group</span></span>
<span data-ttu-id="98d03-109">Pendant le processus de génération, Packer crée des ressources Azure temporaires lorsqu’il génère la machine virtuelle source.</span><span class="sxs-lookup"><span data-stu-id="98d03-109">During the build process, Packer creates temporary Azure resources as it builds the source VM.</span></span> <span data-ttu-id="98d03-110">Pour capturer cette machine virtuelle source afin de l’utiliser en tant qu’image, vous devez définir un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="98d03-110">To capture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="98d03-111">La sortie du processus de génération Packer est stockée dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="98d03-111">The output from the Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="98d03-112">Créez un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="98d03-112">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="98d03-113">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *eastus* :</span><span class="sxs-lookup"><span data-stu-id="98d03-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a><span data-ttu-id="98d03-114">Créer des informations d’identification Azure</span><span class="sxs-lookup"><span data-stu-id="98d03-114">Create Azure credentials</span></span>
<span data-ttu-id="98d03-115">Packer s’authentifie auprès d’Azure à l’aide d’un principal de service.</span><span class="sxs-lookup"><span data-stu-id="98d03-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="98d03-116">Un principal de service Azure est une identité de sécurité que vous pouvez utiliser avec des applications, des services et des outils d’automatisation comme Packer.</span><span class="sxs-lookup"><span data-stu-id="98d03-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="98d03-117">Vous contrôlez et définissez les opérations que le principal de service est autorisé à effectuer dans Azure.</span><span class="sxs-lookup"><span data-stu-id="98d03-117">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span>

<span data-ttu-id="98d03-118">Créez un principal de service avec la commande [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) et assignez au principal de service les autorisations requises pour créer et gérer des ressources avec la commande [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) :</span><span class="sxs-lookup"><span data-stu-id="98d03-118">Create a service principal with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) and assign permissions for the service principal to create and manage resources with [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span></span>

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="98d03-119">Pour vous authentifier auprès d’Azure, vous devez également obtenir vos ID client et d’abonnement Azure à l’aide de la commande [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription) :</span><span class="sxs-lookup"><span data-stu-id="98d03-119">To authenticate to Azure, you also need to obtain your Azure tenant and subscription IDs with [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span></span>

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

<span data-ttu-id="98d03-120">Vous utiliserez ces deux ID à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="98d03-120">You use these two IDs in the next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="98d03-121">Définition du modèle Packer</span><span class="sxs-lookup"><span data-stu-id="98d03-121">Define Packer template</span></span>
<span data-ttu-id="98d03-122">Pour générer les images, vous devez créer un modèle en tant que fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="98d03-122">To build images, you create a template as a JSON file.</span></span> <span data-ttu-id="98d03-123">Dans le modèle, vous définissez des générateurs et des fournisseurs pour mener à bien le processus de génération réel.</span><span class="sxs-lookup"><span data-stu-id="98d03-123">In the template, you define builders and provisioners that carry out the actual build process.</span></span> <span data-ttu-id="98d03-124">Packer possède un [fournisseur pour Azure](https://www.packer.io/docs/builders/azure.html) qui vous permet de définir des ressources Azure, telles que les informations d’identification du principal de service créées à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="98d03-124">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you to define Azure resources, such as the service principal credentials created in the preceding step.</span></span>

<span data-ttu-id="98d03-125">Créez un fichier nommé *windows.json* et collez le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="98d03-125">Create a file named *windows.json* and paste the following content.</span></span> <span data-ttu-id="98d03-126">Saisissez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="98d03-126">Enter your own values for the following:</span></span>

| <span data-ttu-id="98d03-127">Paramètre</span><span class="sxs-lookup"><span data-stu-id="98d03-127">Parameter</span></span>                           | <span data-ttu-id="98d03-128">Emplacement</span><span class="sxs-lookup"><span data-stu-id="98d03-128">Where to obtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="98d03-129">*client_id*</span><span class="sxs-lookup"><span data-stu-id="98d03-129">*client_id*</span></span>                         | <span data-ttu-id="98d03-130">Affichage de l’ID du principal de service avec `$sp.applicationId`</span><span class="sxs-lookup"><span data-stu-id="98d03-130">View service principal ID with `$sp.applicationId`</span></span> |
| <span data-ttu-id="98d03-131">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="98d03-131">*client_secret*</span></span>                     | <span data-ttu-id="98d03-132">Mot de passe que vous avez spécifié dans `$securePassword`</span><span class="sxs-lookup"><span data-stu-id="98d03-132">Password you specified in `$securePassword`</span></span> |
| <span data-ttu-id="98d03-133">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="98d03-133">*tenant_id*</span></span>                         | <span data-ttu-id="98d03-134">Sortie de la commande `$sub.TenantId`</span><span class="sxs-lookup"><span data-stu-id="98d03-134">Output from `$sub.TenantId` command</span></span> |
| <span data-ttu-id="98d03-135">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="98d03-135">*subscription_id*</span></span>                   | <span data-ttu-id="98d03-136">Sortie de la commande `$sub.SubscriptionId`</span><span class="sxs-lookup"><span data-stu-id="98d03-136">Output from `$sub.SubscriptionId` command</span></span> |
| <span data-ttu-id="98d03-137">*object_id*</span><span class="sxs-lookup"><span data-stu-id="98d03-137">*object_id*</span></span>                         | <span data-ttu-id="98d03-138">Affichage de l’ID d’objet du principal de service avec `$sp.Id`</span><span class="sxs-lookup"><span data-stu-id="98d03-138">View service principal object ID with `$sp.Id`</span></span> |
| <span data-ttu-id="98d03-139">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="98d03-139">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="98d03-140">Nom du groupe de ressources créé lors de la première étape</span><span class="sxs-lookup"><span data-stu-id="98d03-140">Name of resource group you created in the first step</span></span> |
| <span data-ttu-id="98d03-141">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="98d03-141">*managed_image_name*</span></span>                | <span data-ttu-id="98d03-142">Nom de l’image de disque géré créée</span><span class="sxs-lookup"><span data-stu-id="98d03-142">Name for the managed disk image that is created</span></span> |

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

<span data-ttu-id="98d03-143">Ce modèle génère une machine virtuelle Windows Server 2016, installe IIS, puis généralise la machine virtuelle avec Sysprep.</span><span class="sxs-lookup"><span data-stu-id="98d03-143">This template builds a Windows Server 2016 VM, installs IIS, then generalizes the VM with Sysprep.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="98d03-144">Génération de l’image Packer</span><span class="sxs-lookup"><span data-stu-id="98d03-144">Build Packer image</span></span>
<span data-ttu-id="98d03-145">Si Packer n’est pas encore installé sur votre ordinateur local, [suivez les instructions d’installation de Packer](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="98d03-145">If you don't already have Packer installed on your local machine, [follow the Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="98d03-146">Générez l’image en spécifiant votre fichier de modèle Packer comme suit :</span><span class="sxs-lookup"><span data-stu-id="98d03-146">Build the image by specifying your Packer template file as follows:</span></span>

```bash
./packer build windows.json
```

<span data-ttu-id="98d03-147">Voici un exemple de sortie issue des commandes précédentes :</span><span class="sxs-lookup"><span data-stu-id="98d03-147">An example of the output from the preceding commands is as follows:</span></span>

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
==> azure-arm: Getting the certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting the certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting the VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM to become available...
==> azure-arm: Connected to WinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying the machine’s properties ...
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
==> azure-arm: Deleting the temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. The artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

<span data-ttu-id="98d03-148">La génération de la machine virtuelle, l’exécution des fournisseurs et le nettoyage du déploiement par Packer ne prennent que quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="98d03-148">It takes a few minutes for Packer to build the VM, run the provisioners, and clean up the deployment.</span></span>


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="98d03-149">Création d’une machine virtuelle à partir d’une image Azure</span><span class="sxs-lookup"><span data-stu-id="98d03-149">Create VM from Azure Image</span></span>
<span data-ttu-id="98d03-150">Définissez un nom d’utilisateur administrateur et un mot de passe pour les machines virtuelles avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span><span class="sxs-lookup"><span data-stu-id="98d03-150">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="98d03-151">Vous pouvez à présent créer une machine virtuelle à partir de votre image à l’aide de la commande [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="98d03-151">You can now create a VM from your Image with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="98d03-152">L’exemple suivant permet de créer une machine virtuelle nommée *myVM* à partir de *myPackerImage*.</span><span class="sxs-lookup"><span data-stu-id="98d03-152">The following example creates a VM named *myVM* from *myPackerImage*.</span></span>

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

# Define the image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

<span data-ttu-id="98d03-153">La création de la machine virtuelle ne nécessite que quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="98d03-153">It takes a few minutes to create the VM.</span></span>


## <a name="test-vm-and-iis"></a><span data-ttu-id="98d03-154">Test de la machine virtuelle et d’IIS</span><span class="sxs-lookup"><span data-stu-id="98d03-154">Test VM and IIS</span></span>
<span data-ttu-id="98d03-155">Obtenez l’adresse IP publique de votre machine virtuelle avec [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="98d03-155">Obtain the public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="98d03-156">L’exemple suivant obtient l’adresse IP pour *myPublicIP* créée précédemment :</span><span class="sxs-lookup"><span data-stu-id="98d03-156">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="98d03-157">Vous pouvez alors entrer l’adresse IP publique dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="98d03-157">You can then enter the public IP address in to a web browser.</span></span>

![Site IIS par défaut](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a><span data-ttu-id="98d03-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="98d03-159">Next steps</span></span>
<span data-ttu-id="98d03-160">Dans cet exemple, IIS était déjà installé et vous avez utilisé Packer pour créer une image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="98d03-160">In this example, you used Packer to create a VM image with IIS already installed.</span></span> <span data-ttu-id="98d03-161">Vous pouvez utiliser cette image de machine virtuelle avec les flux de travail de déploiement existants, par exemple pour déployer votre application sur les machines virtuelles créées à partir de l’image avec Team Services, Ansible, Chef ou Puppet.</span><span class="sxs-lookup"><span data-stu-id="98d03-161">You can use this VM image alongside existing deployment workflows, such as to deploy your app to VMs created from the Image with Team Services, Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="98d03-162">Pour obtenir d’autres exemples de modèles Packer pour d’autres distributions Windows, consultez [ce référentiel GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="98d03-162">For additional example Packer templates for other Windows distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>