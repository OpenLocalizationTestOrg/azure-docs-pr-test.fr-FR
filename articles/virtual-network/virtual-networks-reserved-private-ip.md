---
title: "aaaStatic interne classique IP - Azure VM - privée"
description: "Présentation des adresses IP internes statique (adresses IP dynamiques) et la manière dont toomanage les"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="02224-103">Comment tooset une adresse IP privée interne statique d’adresses à l’aide de PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="02224-103">How tooset a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="02224-104">Dans la plupart des cas, vous ne devez toospecify une adresse IP interne statique pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="02224-104">In most cases, you won’t need toospecify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="02224-105">Les machines virtuelles dans un réseau virtuel recevront automatiquement une adresse IP interne à partir d'une plage que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="02224-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="02224-106">Toutefois, dans certains cas, il peut être bon de spécifier une adresse IP statique pour une machine virtuelle en particulier.</span><span class="sxs-lookup"><span data-stu-id="02224-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="02224-107">Par exemple, si votre machine virtuelle est continu toorun DNS ou être un contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="02224-107">For example, if your VM is going toorun DNS or will be a domain controller.</span></span> <span data-ttu-id="02224-108">Une adresse IP interne statique reste associée aux hello machine virtuelle, même par le biais d’un état d’arrêt/mise hors service.</span><span class="sxs-lookup"><span data-stu-id="02224-108">A static internal IP address stays with hello VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="02224-109">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="02224-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="02224-110">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="02224-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="02224-111">Microsoft recommande à la plupart des nouveaux déploiements hello [modèle de déploiement de gestionnaire de ressources](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="02224-111">Microsoft recommends that most new deployments use hello [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="02224-112">Comment tooverify si une adresse IP spécifique est disponible</span><span class="sxs-lookup"><span data-stu-id="02224-112">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="02224-113">tooverify si hello adresse IP *10.0.0.7* est disponible dans un réseau virtuel nommé *TestVnet*, exécutez hello suivant de commande PowerShell et vérifiez la valeur hello pour *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="02224-113">tooverify if hello IP address *10.0.0.7* is available in a vnet named *TestVnet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="02224-114">Si vous souhaitez que la commande de hello tootest ci-dessus dans un environnement sécurisé instructions hello dans [créer un réseau virtuel (classiques)](virtual-networks-create-vnet-classic-pportal.md) toocreate un réseau virtuel nommé *TestVnet* et assurez-vous qu’il utilise hello  *10.0.0.0/8* l’espace d’adressage.</span><span class="sxs-lookup"><span data-stu-id="02224-114">If you want tootest hello command above in a safe environment follow hello guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) toocreate a vnet named *TestVnet* and ensure it uses hello *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="02224-115">Comment toospecify une adresse IP interne statique lors de la création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="02224-115">How toospecify a static internal IP when creating a VM</span></span>
<span data-ttu-id="02224-116">Hello script PowerShell ci-dessous crée un nouveau service cloud nommé *TestService*, puis récupère une image à partir d’Azure, puis crée un ordinateur virtuel nommé *TestVM* dans le nouveau service cloud hello, à l’aide de l’image hello récupérée, jeux de hello toobe de machine virtuelle dans un sous-réseau nommé *Subnet-1*et définit *10.0.0.7* en tant qu’une adresse IP interne statique pour hello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="02224-116">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="02224-117">Comment tooretrieve internes informations IP statique pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="02224-117">How tooretrieve static internal IP information for a VM</span></span>
<span data-ttu-id="02224-118">tooview hello statique internes informations IP pour hello machine virtuelle créée avec le script hello ci-dessus, exécutez hello suivant de commande PowerShell et observer les valeurs hello pour *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="02224-118">tooview hello static internal IP information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="02224-119">Comment tooremove une adresse IP interne statique d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="02224-119">How tooremove a static internal IP from a VM</span></span>
<span data-ttu-id="02224-120">adresse IP interne statique de tooremove hello ajouté toohello machine virtuelle dans le script hello ci-dessus, exécutez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="02224-120">tooremove hello static internal IP added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a><span data-ttu-id="02224-121">Comment tooadd un tooan d’IP interne statique machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="02224-121">How tooadd a static internal IP tooan existing VM</span></span>
<span data-ttu-id="02224-122">tooadd un toohello IP interne statique machine virtuelle créée à l’aide de script hello ci-dessus, exécutez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02224-122">tooadd a static internal IP toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="02224-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="02224-123">Next steps</span></span>
[<span data-ttu-id="02224-124">Adresse IP réservée</span><span class="sxs-lookup"><span data-stu-id="02224-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="02224-125">Adresses IP publiques de niveau d’instance (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="02224-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="02224-126">API REST d’adresse IP réservée</span><span class="sxs-lookup"><span data-stu-id="02224-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

