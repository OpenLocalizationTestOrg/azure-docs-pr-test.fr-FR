---
title: "Adresse IP privée interne statique - Machine virtuelle Azure - Classic"
description: Fonctionnement et gestion des adresses IP internes statiques (adresses IP dynamiques)
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
ms.openlocfilehash: cf9ee59ca4e44ed01836c2efb1f4df5f073bf6e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="9d201-103">Comment définir une adresse IP privée interne statique à l’aide de PowerShell (Classic)</span><span class="sxs-lookup"><span data-stu-id="9d201-103">How to set a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="9d201-104">Dans la plupart des cas, il n’est pas nécessaire de spécifier une adresse IP interne statique pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9d201-104">In most cases, you won’t need to specify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="9d201-105">Les machines virtuelles dans un réseau virtuel recevront automatiquement une adresse IP interne à partir d'une plage que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="9d201-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="9d201-106">Toutefois, dans certains cas, il peut être bon de spécifier une adresse IP statique pour une machine virtuelle en particulier.</span><span class="sxs-lookup"><span data-stu-id="9d201-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="9d201-107">Par exemple, si votre machine virtuelle doit exécuter DNS ou fait office de contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="9d201-107">For example, if your VM is going to run DNS or will be a domain controller.</span></span> <span data-ttu-id="9d201-108">Une adresse IP interne statique reste associée à la machine virtuelle même lorsque cette dernière se trouve en état d'arrêt/annulation de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="9d201-108">A static internal IP address stays with the VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9d201-109">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9d201-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9d201-110">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="9d201-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="9d201-111">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le [modèle de déploiement Resource Manager](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9d201-111">Microsoft recommends that most new deployments use the [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-to-verify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="9d201-112">Vérification de la disponibilité d'une adresse IP particulière</span><span class="sxs-lookup"><span data-stu-id="9d201-112">How to verify if a specific IP address is available</span></span>
<span data-ttu-id="9d201-113">Pour vérifier si l’adresse IP *10.0.0.7* est disponible dans un réseau virtuel nommé *TestVNet*, exécutez la commande PowerShell suivante et vérifiez la valeur pour *IsAvailable* :</span><span class="sxs-lookup"><span data-stu-id="9d201-113">To verify if the IP address *10.0.0.7* is available in a vnet named *TestVnet*, run the following PowerShell command and verify the value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="9d201-114">Si vous voulez tester la commande ci-dessus dans un environnement sécurisé, suivez les instructions de l’article [Créer un réseau virtuel (classique)](virtual-networks-create-vnet-classic-pportal.md) pour créer un réseau virtuel nommé *TestVnet* et vérifiez qu’il utilise l’espace d’adressage *10.0.0.0/8*.</span><span class="sxs-lookup"><span data-stu-id="9d201-114">If you want to test the command above in a safe environment follow the guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) to create a vnet named *TestVnet* and ensure it uses the *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-to-specify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="9d201-115">Spécification d’une adresse IP interne statique lors de la création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9d201-115">How to specify a static internal IP when creating a VM</span></span>
<span data-ttu-id="9d201-116">Le script PowerShell ci-dessous crée un service cloud nommé *TestService*, récupère une image auprès d’Azure, crée une machine virtuelle nommée *TestVM* dans le nouveau service cloud à partir de l’image récupérée, définit la machine virtuelle dans un sous-réseau nommé *Subnet-1*, puis définit *10.0.0.7* comme adresse IP interne statique pour la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="9d201-116">The PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in the new cloud service using the retrieved image, sets the VM to be in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for the VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-to-retrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="9d201-117">Récupération des informations d’adresse IP interne statique pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9d201-117">How to retrieve static internal IP information for a VM</span></span>
<span data-ttu-id="9d201-118">Pour visualiser les informations d’adresse interne statique concernant la machine virtuelle créée avec le script ci-dessus, exécutez la commande PowerShell ci-après et examinez les valeurs des éléments *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="9d201-118">To view the static internal IP information for the VM created with the script above, run the following PowerShell command and observe the values for *IpAddress*:</span></span>

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

## <a name="how-to-remove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="9d201-119">Suppression d’une adresse IP interne statique d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9d201-119">How to remove a static internal IP from a VM</span></span>
<span data-ttu-id="9d201-120">Pour supprimer l’adresse IP interne statique ajoutée à la machine virtuelle par le biais du script ci-dessus, exécutez la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="9d201-120">To remove the static internal IP added to the VM in the script above, run the following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-to-add-a-static-internal-ip-to-an-existing-vm"></a><span data-ttu-id="9d201-121">Ajout d’une adresse IP interne statique à une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="9d201-121">How to add a static internal IP to an existing VM</span></span>
<span data-ttu-id="9d201-122">Pour ajouter une adresse IP interne statique à la machine virtuelle créée à l’aide du script ci-dessus, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9d201-122">To add a static internal IP to the VM created using the script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="9d201-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9d201-123">Next steps</span></span>
[<span data-ttu-id="9d201-124">Adresse IP réservée</span><span class="sxs-lookup"><span data-stu-id="9d201-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="9d201-125">Adresses IP publiques de niveau d’instance (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="9d201-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="9d201-126">API REST d’adresse IP réservée</span><span class="sxs-lookup"><span data-stu-id="9d201-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

