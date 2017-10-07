---
title: "ensemble d’une échelle de machine virtuelle Azure aaaCreate | Documents Microsoft"
description: "Créez et déployez un groupe de machines virtuelles identiques Linux ou Windows Azure avec Azure CLI, PowerShell, un modèle ou Visual Studio."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a><span data-ttu-id="ebadb-103">Créer et déployer un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="ebadb-103">Create and deploy a virtual machine scale set</span></span>
<span data-ttu-id="ebadb-104">Machines virtuelles identiques facilitent vous toodeploy et gérer des machines virtuelles identiques en tant qu’ensemble.</span><span class="sxs-lookup"><span data-stu-id="ebadb-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="ebadb-105">Les groupes à échelle identique fournissent une couche de calcul hautement évolutive et personnalisable pour les applications « hyperscale », et prennent en charge les images de plateforme Windows, les images de plateforme Linux, des images personnalisées et les extensions.</span><span class="sxs-lookup"><span data-stu-id="ebadb-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="ebadb-106">Pour plus d’informations sur les groupes identiques, consultez [Groupes de machines virtuelles identiques](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ebadb-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="ebadb-107">Ce didacticiel vous montre comment toocreate définie une échelle de machines virtuelles **sans** à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ebadb-107">This tutorial shows you how toocreate a virtual machine scale set **without** using hello Azure portal.</span></span> <span data-ttu-id="ebadb-108">Pour plus d’informations sur la façon dont toouse hello portail Azure, consultez [toocreate une échelle de machines virtuelles définition avec hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="ebadb-108">For information about how toouse hello Azure portal, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

>[!NOTE]
><span data-ttu-id="ebadb-109">Pour plus d’informations sur les ressources Azure Resource Manager, consultez [Déploiement Azure Resource Manager et déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ebadb-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="ebadb-110">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="ebadb-110">Sign in tooAzure</span></span>

<span data-ttu-id="ebadb-111">Si vous utilisez Azure CLI 2.0 ou Azure PowerShell toocreate une échelle définie, vous devez tout d’abord toosign dans tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="ebadb-111">If you're using Azure CLI 2.0 or Azure PowerShell toocreate a scale set, you first need toosign in tooyour subscription.</span></span>

<span data-ttu-id="ebadb-112">Pour plus d’informations sur la façon dont tooinstall, configurer et vous connecter tooAzure avec CLI d’Azure ou de PowerShell, consultez [prise en main d’Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) ou [prise en main des applets de commande Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ebadb-112">For more information about how tooinstall, set up, and sign in tooAzure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="ebadb-113">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="ebadb-113">Create a resource group</span></span>

<span data-ttu-id="ebadb-114">Vous devez tout d’abord toocreate un groupe de ressources ensemble d’échelle de machine virtuelle hello est associé.</span><span class="sxs-lookup"><span data-stu-id="ebadb-114">You first need toocreate a resource group that hello virtual machine scale set is associated with.</span></span>

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a><span data-ttu-id="ebadb-115">Créer à partir de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="ebadb-115">Create from Azure CLI</span></span>

<span data-ttu-id="ebadb-116">Avec Azure CLI, vous pouvez créer un groupe de machines virtuelles identiques avec un minimum d’effort.</span><span class="sxs-lookup"><span data-stu-id="ebadb-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span></span> <span data-ttu-id="ebadb-117">Si vous omettez les valeurs par défaut, elles vous sont fournies.</span><span class="sxs-lookup"><span data-stu-id="ebadb-117">If you omit default values, they are provided for you.</span></span> <span data-ttu-id="ebadb-118">Par exemple, si vous ne spécifiez pas les informations du réseau virtuel, un réseau virtuel est créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="ebadb-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span></span> <span data-ttu-id="ebadb-119">Si vous omettez les composants suivants de hello, ils sont créés pour vous :</span><span class="sxs-lookup"><span data-stu-id="ebadb-119">If you omit hello following parts, they are created for you:</span></span> 
- <span data-ttu-id="ebadb-120">Un équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="ebadb-120">A load balancer</span></span>
- <span data-ttu-id="ebadb-121">Un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="ebadb-121">A virtual network</span></span>
- <span data-ttu-id="ebadb-122">Une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="ebadb-122">A public IP address</span></span>

<span data-ttu-id="ebadb-123">Lorsque les choix hello image de machine virtuelle que vous souhaitez toouse sur l’ensemble d’échelle de machine virtuelle hello, vous avez le choix :</span><span class="sxs-lookup"><span data-stu-id="ebadb-123">When choosing hello virtual machine image that you want toouse on hello virtual machine scale set, you have a few choices:</span></span>

- <span data-ttu-id="ebadb-124">URN</span><span class="sxs-lookup"><span data-stu-id="ebadb-124">URN</span></span>  
<span data-ttu-id="ebadb-125">Identificateur Hello d’une ressource :</span><span class="sxs-lookup"><span data-stu-id="ebadb-125">hello identifier of a resource:</span></span>  
<span data-ttu-id="ebadb-126">**Win2012R2Datacenter**</span><span class="sxs-lookup"><span data-stu-id="ebadb-126">**Win2012R2Datacenter**</span></span>

- <span data-ttu-id="ebadb-127">Alias d’URN</span><span class="sxs-lookup"><span data-stu-id="ebadb-127">URN alias</span></span>  
<span data-ttu-id="ebadb-128">nom convivial de Hello d’un URN :</span><span class="sxs-lookup"><span data-stu-id="ebadb-128">hello friendly name of a URN:</span></span>  
<span data-ttu-id="ebadb-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span><span class="sxs-lookup"><span data-stu-id="ebadb-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span></span>

- <span data-ttu-id="ebadb-130">ID de ressource personnalisé</span><span class="sxs-lookup"><span data-stu-id="ebadb-130">Custom resource id</span></span>  
<span data-ttu-id="ebadb-131">tooan de chemin d’accès Hello ressource Azure :</span><span class="sxs-lookup"><span data-stu-id="ebadb-131">hello path tooan Azure resource:</span></span>  
<span data-ttu-id="ebadb-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span><span class="sxs-lookup"><span data-stu-id="ebadb-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span></span>

- <span data-ttu-id="ebadb-133">Ressource web</span><span class="sxs-lookup"><span data-stu-id="ebadb-133">Web resource</span></span>  
<span data-ttu-id="ebadb-134">tooan de chemin d’accès Hello URI HTTP :</span><span class="sxs-lookup"><span data-stu-id="ebadb-134">hello path tooan HTTP URI:</span></span>  
<span data-ttu-id="ebadb-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span><span class="sxs-lookup"><span data-stu-id="ebadb-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span></span>

>[!TIP]
><span data-ttu-id="ebadb-136">Vous pouvez obtenir la liste des images disponibles avec `az vm image list`.</span><span class="sxs-lookup"><span data-stu-id="ebadb-136">You can get a list of available images with `az vm image list`.</span></span>

<span data-ttu-id="ebadb-137">définie d’une échelle de machines virtuelles toocreate, vous devez spécifier hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="ebadb-137">toocreate a virtual machine scale set, you must specify hello following:</span></span>

- <span data-ttu-id="ebadb-138">Groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="ebadb-138">Resource group</span></span> 
- <span data-ttu-id="ebadb-139">Nom</span><span class="sxs-lookup"><span data-stu-id="ebadb-139">Name</span></span>
- <span data-ttu-id="ebadb-140">Image du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="ebadb-140">Operating system image</span></span>
- <span data-ttu-id="ebadb-141">Informations d’authentification</span><span class="sxs-lookup"><span data-stu-id="ebadb-141">Authentication information</span></span> 
 
<span data-ttu-id="ebadb-142">Hello, l’exemple suivant crée un ensemble d’échelle base ordinateur virtuel (cette étape peut prendre quelques minutes).</span><span class="sxs-lookup"><span data-stu-id="ebadb-142">hello following example creates a basic virtual machine scale set (this step might take a few minutes).</span></span>

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

<span data-ttu-id="ebadb-143">Une fois que la fin de la commande hello maintenant avoir votre échelle de l’ordinateur virtuel créé.</span><span class="sxs-lookup"><span data-stu-id="ebadb-143">Once hello command finishes you will now have your virtual machine scale set created.</span></span> <span data-ttu-id="ebadb-144">Vous devrez peut-être adresse tooget hello de machine virtuelle de hello afin que vous pouvez vous connecter à tooit.</span><span class="sxs-lookup"><span data-stu-id="ebadb-144">You may need tooget hello IP address of hello virtual machine so that you can connect tooit.</span></span> <span data-ttu-id="ebadb-145">Vous pouvez obtenir de nombreuses informations différents sur l’ordinateur virtuel de hello (y compris l’adresse IP de hello) avec hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="ebadb-145">You can get a lot of different information about hello virtual machine (including hello IP address) with hello following command.</span></span> 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a><span data-ttu-id="ebadb-146">Créer à partir de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebadb-146">Create from PowerShell</span></span>

<span data-ttu-id="ebadb-147">PowerShell est toouse plus compliqué que CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="ebadb-147">PowerShell is more complicated toouse than Azure CLI.</span></span> <span data-ttu-id="ebadb-148">Alors que l’interface CLI Azure fournit les valeurs par défaut pour les ressources relatives à la mise en réseau (équilibrage de charge, adresse IP, réseau virtuel), ce n’est pas le cas de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ebadb-148">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span></span> <span data-ttu-id="ebadb-149">La référence à une image avec PowerShell est également un peu plus complexe.</span><span class="sxs-lookup"><span data-stu-id="ebadb-149">Referencing an image with PowerShell is a slightly more complicated too.</span></span> <span data-ttu-id="ebadb-150">Vous pouvez obtenir des images avec hello suivant d’applets de commande :</span><span class="sxs-lookup"><span data-stu-id="ebadb-150">You can get images with hello following cmdlets:</span></span>

1. <span data-ttu-id="ebadb-151">Get-AzureRMVMImagePublisher</span><span class="sxs-lookup"><span data-stu-id="ebadb-151">Get-AzureRMVMImagePublisher</span></span>
2. <span data-ttu-id="ebadb-152">Get-AzureRMVMImageOffer</span><span class="sxs-lookup"><span data-stu-id="ebadb-152">Get-AzureRMVMImageOffer</span></span>
3. <span data-ttu-id="ebadb-153">Get-AzureRmVMImageSku</span><span class="sxs-lookup"><span data-stu-id="ebadb-153">Get-AzureRmVMImageSku</span></span>

<span data-ttu-id="ebadb-154">travail d’applets de commande Hello peut être transmis dans la séquence.</span><span class="sxs-lookup"><span data-stu-id="ebadb-154">hello cmdlets work can be piped in sequence.</span></span> <span data-ttu-id="ebadb-155">Voici un exemple de comment tooget toutes les images pour hello **ouest des États-Unis 2** région avec un serveur de publication qui a le nom de hello **microsoft** qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="ebadb-155">Here is an example of how tooget all images for hello **West US 2** region with a publisher that has hello name **microsoft** in it.</span></span>

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

<span data-ttu-id="ebadb-156">flux de travail Hello pour la création d’un ensemble d’échelle de machine virtuelle est la suivante :</span><span class="sxs-lookup"><span data-stu-id="ebadb-156">hello workflow for creating a virtual machine scale set is as follows:</span></span>

1. <span data-ttu-id="ebadb-157">Créer un objet de configuration qui conserve des informations sur l’ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="ebadb-157">Create a config object that holds information about hello scale set.</span></span>
2. <span data-ttu-id="ebadb-158">Référence hello du système d’exploitation image de base.</span><span class="sxs-lookup"><span data-stu-id="ebadb-158">Reference hello base OS image.</span></span>
3. <span data-ttu-id="ebadb-159">Configurer les paramètres de système d’exploitation hello : authentification, préfixe du nom de machine virtuelle et/passe de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ebadb-159">Configure hello operating system settings: authentication, VM name prefix, and user/pass.</span></span>
4. <span data-ttu-id="ebadb-160">Configurez la mise en réseau.</span><span class="sxs-lookup"><span data-stu-id="ebadb-160">Configure networking.</span></span>
5. <span data-ttu-id="ebadb-161">Créer un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="ebadb-161">Create hello scale set.</span></span>

<span data-ttu-id="ebadb-162">Cet exemple crée un groupe identique de base à deux instances pour un ordinateur où Windows Server 2016 est installé.</span><span class="sxs-lookup"><span data-stu-id="ebadb-162">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span></span>

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a><span data-ttu-id="ebadb-163">Utilisation d’une image de machine virtuelle personnalisée</span><span class="sxs-lookup"><span data-stu-id="ebadb-163">Using a custom virtual machine image</span></span>
<span data-ttu-id="ebadb-164">Si vous créez une échelle définie à partir de votre propre image personnalisée, au lieu de référencement d’une image de machine virtuelle à partir de la galerie de hello, hello _Set-AzureRmVmssStorageProfile_ commande ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="ebadb-164">If you are creating a scale set from your own custom image, instead of referencing a virtual machine image from hello gallery, hello _Set-AzureRmVmssStorageProfile_ command would look like this:</span></span>
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a><span data-ttu-id="ebadb-165">Créer à partir d’un modèle</span><span class="sxs-lookup"><span data-stu-id="ebadb-165">Create from a template</span></span>

<span data-ttu-id="ebadb-166">Vous pouvez déployer un groupe de machines virtuelles identiques à l’aide d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ebadb-166">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span></span> <span data-ttu-id="ebadb-167">Vous pouvez créer votre propre modèle, ou utilisez une de hello [référentiel de modèles](https://azure.microsoft.com/resources/templates/?term=vmss).</span><span class="sxs-lookup"><span data-stu-id="ebadb-167">You can create your own template or use one from hello [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span></span> <span data-ttu-id="ebadb-168">Ces modèles peuvent être déployés directement tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ebadb-168">These templates can be deployed directly tooyour Azure subscription.</span></span>

>[!NOTE]
><span data-ttu-id="ebadb-169">toocreate votre propre modèle, vous créez un fichier de texte JSON.</span><span class="sxs-lookup"><span data-stu-id="ebadb-169">toocreate your own template, you create a JSON text file.</span></span> <span data-ttu-id="ebadb-170">Pour plus d’informations sur la façon toocreate et personnaliser un modèle, consultez [modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ebadb-170">For general information about how toocreate and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="ebadb-171">Un exemple de modèle est disponible [sur GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span><span class="sxs-lookup"><span data-stu-id="ebadb-171">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span></span> <span data-ttu-id="ebadb-172">Pour plus d’informations sur la façon dont toocreate et utiliser ces exemples, consultez [un ensemble d’échelle viable Minimum](.\virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="ebadb-172">For more information about how toocreate and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span></span>

## <a name="create-from-visual-studio"></a><span data-ttu-id="ebadb-173">Créer à partir de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ebadb-173">Create from Visual Studio</span></span>

<span data-ttu-id="ebadb-174">Avec Visual Studio, vous pouvez créer un projet de groupe de ressources Azure et ajouter qu'une échelle de machines virtuelles des ensembles de tooit de modèle.</span><span class="sxs-lookup"><span data-stu-id="ebadb-174">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template tooit.</span></span> <span data-ttu-id="ebadb-175">Vous pouvez choisir si vous souhaitez que tooimport à partir de GitHub ou hello Galerie d’applications Web Azure.</span><span class="sxs-lookup"><span data-stu-id="ebadb-175">You can choose whether you want tooimport it from GitHub or hello Azure Web Application Gallery.</span></span> <span data-ttu-id="ebadb-176">Un script de déploiement PowerShell est également généré pour vous.</span><span class="sxs-lookup"><span data-stu-id="ebadb-176">A deployment PowerShell script is also generated for you.</span></span> <span data-ttu-id="ebadb-177">Pour plus d’informations, consultez [toocreate une échelle de machines virtuelles définition avec Visual Studio](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="ebadb-177">For more information, see [How toocreate a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span></span>

## <a name="create-from-hello-azure-portal"></a><span data-ttu-id="ebadb-178">Créer à partir de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="ebadb-178">Create from hello Azure portal</span></span>

<span data-ttu-id="ebadb-179">Hello portail Azure fournit un moyen pratique tooquickly créer un ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="ebadb-179">hello Azure portal provides a convenient way tooquickly create a scale set.</span></span> <span data-ttu-id="ebadb-180">Pour plus d’informations, consultez [toocreate une échelle de machines virtuelles définition avec hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="ebadb-180">For more information, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebadb-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ebadb-181">Next steps</span></span>

<span data-ttu-id="ebadb-182">En savoir plus sur les [disques de données](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="ebadb-182">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="ebadb-183">Découvrez comment trop[gérer vos applications](virtual-machine-scale-sets-deploy-app.md).</span><span class="sxs-lookup"><span data-stu-id="ebadb-183">Learn how too[manage your apps](virtual-machine-scale-sets-deploy-app.md).</span></span>
