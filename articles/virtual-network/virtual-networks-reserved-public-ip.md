---
title: "Gestion des adresses IP réservées Azure (Classic) - PowerShell | Microsoft Docs"
description: "Comprendre les adresses IP réservées (Classic) et la manière de les gérer à l’aide de PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 5e9c83cebec96c6bc8afd53b0c637d7af899746f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="9fe65-103">Adresses IP réservées (Classic)</span><span class="sxs-lookup"><span data-stu-id="9fe65-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9fe65-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="9fe65-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="9fe65-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fe65-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="9fe65-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="9fe65-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="9fe65-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="9fe65-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="9fe65-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="9fe65-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="9fe65-109">Il existe deux catégories d’adresses IP dans Azure, les réservées et les dynamiques.</span><span class="sxs-lookup"><span data-stu-id="9fe65-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="9fe65-110">Les adresses IP publiques gérées par Azure sont dynamiques par défaut.</span><span class="sxs-lookup"><span data-stu-id="9fe65-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="9fe65-111">Cela signifie que l'adresse IP utilisée pour un service cloud donné (adresse IP virtuelle) ou pour accéder à une machine virtuelle ou à une instance de rôle directement (ILPIP) peut changer à tout moment, lorsque les ressources sont arrêtées ou désallouées.</span><span class="sxs-lookup"><span data-stu-id="9fe65-111">That means that the IP address used for a given cloud service (VIP) or to access a VM or role instance directly (ILPIP) can change from time to time, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="9fe65-112">Pour empêcher la modification des adresses IP, vous pouvez réserver une adresse IP.</span><span class="sxs-lookup"><span data-stu-id="9fe65-112">To prevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="9fe65-113">Les adresses IP réservées peuvent uniquement servir d’adresse IP virtuelle, garantissant que l'adresse IP utilisée pour le service cloud reste la même, et ce même si les ressources sont arrêtées ou désallouées.</span><span class="sxs-lookup"><span data-stu-id="9fe65-113">Reserved IPs can be used only as a VIP, ensuring that the IP address for the cloud service remains the same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="9fe65-114">Par ailleurs, vous pouvez convertir une adresse IP dynamique existante utilisée comme adresse IP virtuelle en adresse IP réservée.</span><span class="sxs-lookup"><span data-stu-id="9fe65-114">Furthermore, you can convert existing dynamic IPs used as a VIP to a reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fe65-115">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9fe65-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9fe65-116">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="9fe65-116">This article covers using the classic deployment model.</span></span> <span data-ttu-id="9fe65-117">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9fe65-117">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="9fe65-118">Découvrez comment réserver une adresse IP publique statique à l’aide du [modèle de déploiement Resource Manager](virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9fe65-118">Learn how to reserve a static public IP address using the [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="9fe65-119">Pour en savoir plus sur les adresses IP dans Azure, voir l’article [Adresses IP](virtual-network-ip-addresses-overview-classic.md).</span><span class="sxs-lookup"><span data-stu-id="9fe65-119">To learn more about IP addresses in Azure, read the [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="9fe65-120">Quand ai-je besoin d’une adresse IP réservée ?</span><span class="sxs-lookup"><span data-stu-id="9fe65-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="9fe65-121">**Vous souhaitez vous assurer que l'adresse IP est réservée dans votre abonnement**.</span><span class="sxs-lookup"><span data-stu-id="9fe65-121">**You want to ensure that the IP is reserved in your subscription**.</span></span> <span data-ttu-id="9fe65-122">Si vous souhaitez réserver une adresse IP qui reste associée à votre abonnement en toute circonstance, vous devez utiliser une adresse IP publique réservée.</span><span class="sxs-lookup"><span data-stu-id="9fe65-122">If you want to reserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="9fe65-123">**Vous souhaitez que votre adresse IP reste associée à votre service cloud, même lorsque les machines virtuelles sont arrêtées ou désallouées**.</span><span class="sxs-lookup"><span data-stu-id="9fe65-123">**You want your IP to stay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="9fe65-124">Si vous souhaitez que votre service soit accessible à l'aide d'une adresse IP qui ne change pas, même lorsque les machines virtuelles dans le service cloud sont arrêtées ou désallouées.</span><span class="sxs-lookup"><span data-stu-id="9fe65-124">If you want your service to be accessed by using an IP address that doesn't change, even when VMs in the cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="9fe65-125">**Vous souhaitez vous assurer que le trafic provenant d'Azure utilise une adresse IP prévisible**.</span><span class="sxs-lookup"><span data-stu-id="9fe65-125">**You want to ensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="9fe65-126">Il se peut que la configuration de votre pare-feu local autorise uniquement le trafic provenant d'adresses IP spécifiques.</span><span class="sxs-lookup"><span data-stu-id="9fe65-126">You may have your on-premises firewall configured to allow only traffic from specific IP addresses.</span></span> <span data-ttu-id="9fe65-127">En réservant une adresse IP, vous connaissez l'adresse IP source et n'avez pas besoin de mettre à jour les règles de pare-feu suite à une modification d'adresse IP.</span><span class="sxs-lookup"><span data-stu-id="9fe65-127">By reserving an IP, you know the source IP address, and don't need to update your firewall rules due to an IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="9fe65-128">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="9fe65-128">FAQ</span></span>
1. <span data-ttu-id="9fe65-129">Puis-je utiliser une adresse IP réservée pour tous les services Azure ?</span><span class="sxs-lookup"><span data-stu-id="9fe65-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="9fe65-130">Non.</span><span class="sxs-lookup"><span data-stu-id="9fe65-130">No.</span></span> <span data-ttu-id="9fe65-131">Les adresses IP réservées peuvent être utilisées uniquement pour les machines virtuelles et les rôles d'instance de service cloud exposés par une adresse IP virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9fe65-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="9fe65-132">Combien d’adresses IP réservées puis-je avoir ?</span><span class="sxs-lookup"><span data-stu-id="9fe65-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="9fe65-133">Pour plus d’informations, consultez la [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.</span><span class="sxs-lookup"><span data-stu-id="9fe65-133">For details, see the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="9fe65-134">L’obtention d’adresses IP réservées est-elle payante ?</span><span class="sxs-lookup"><span data-stu-id="9fe65-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="9fe65-135">Parfois.</span><span class="sxs-lookup"><span data-stu-id="9fe65-135">Sometimes.</span></span> <span data-ttu-id="9fe65-136">Pour plus d’informations sur la tarification, consultez la [Tarification – Adresses IP réservées](http://go.microsoft.com/fwlink/?LinkID=398482).</span><span class="sxs-lookup"><span data-stu-id="9fe65-136">For pricing details, see the [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="9fe65-137">Comment réserver une adresse IP ?</span><span class="sxs-lookup"><span data-stu-id="9fe65-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="9fe65-138">Vous pouvez utiliser PowerShell, le [API REST de gestion Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), ou [portail Azure](https://portal.azure.com) de réserver une adresse IP dans une région Azure.</span><span class="sxs-lookup"><span data-stu-id="9fe65-138">You can use PowerShell, the [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or the [Azure portal](https://portal.azure.com) to reserve an IP address in an Azure region.</span></span> <span data-ttu-id="9fe65-139">Une adresse IP réservée est associée à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="9fe65-139">A reserved IP address is associated to your subscription.</span></span>
5. <span data-ttu-id="9fe65-140">Puis-je utiliser une adresse IP réservée avec des réseaux virtuels basés sur un groupe d'affinités ?</span><span class="sxs-lookup"><span data-stu-id="9fe65-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="9fe65-141">Non.</span><span class="sxs-lookup"><span data-stu-id="9fe65-141">No.</span></span> <span data-ttu-id="9fe65-142">Les adresses IP réservées sont uniquement prises en charge dans les réseaux virtuels régionaux.</span><span class="sxs-lookup"><span data-stu-id="9fe65-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="9fe65-143">Les adresses IP réservées ne sont pas prises en charge dans les réseaux virtuels associés à des groupes d’affinités.</span><span class="sxs-lookup"><span data-stu-id="9fe65-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="9fe65-144">Pour plus d'informations sur l'association d'un réseau virtuel à une région ou un groupe d'affinités, consultez l’article [À propos des réseaux virtuels et groupes d’affinités régionaux](virtual-networks-migrate-to-regional-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="9fe65-144">For more information about associating a VNet with a region or affinity group, see the [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="9fe65-145">Gérer les adresses IP virtuelles réservées</span><span class="sxs-lookup"><span data-stu-id="9fe65-145">Manage reserved VIPs</span></span>

<span data-ttu-id="9fe65-146">Vérifiez que vous avez installé et configuré PowerShell en procédant de la manière décrite dans l’article [Installer et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9fe65-146">Ensure you have installed and configured PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="9fe65-147">Avant de pouvoir utiliser une adresse IP réservée, vous devez l'ajouter à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="9fe65-147">Before you can use reserved IPs, you must add it to your subscription.</span></span> <span data-ttu-id="9fe65-148">Pour créer une adresse IP réservée à partir du pool d’adresses IP publiques disponibles dans la région *États-Unis du Centre*, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9fe65-148">To create a reserved IP from the pool of public IP addresses available in the *Central US* location, run the following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="9fe65-149">Toutefois, veuillez noter que vous ne pouvez pas spécifier quelle adresse IP vous souhaitez réserver.</span><span class="sxs-lookup"><span data-stu-id="9fe65-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="9fe65-150">Pour voir quelles adresses IP sont réservées dans votre abonnement, exécutez la commande PowerShell suivante et notez les valeurs de *ReservedIPName* et *Address* :</span><span class="sxs-lookup"><span data-stu-id="9fe65-150">To view what IP addresses are reserved in your subscription, run the following PowerShell command, and notice the values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="9fe65-151">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="9fe65-151">Expected output:</span></span>

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
><span data-ttu-id="9fe65-152">Lorsque vous créez une adresse IP réservée avec PowerShell, vous ne pouvez pas spécifier un groupe de ressources pour y créer l’adresse IP réservée.</span><span class="sxs-lookup"><span data-stu-id="9fe65-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group to create the reserved IP in.</span></span> <span data-ttu-id="9fe65-153">Azure place automatiquement cette adresse dans un groupe de ressources nommé *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="9fe65-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="9fe65-154">Si vous créez l’adresse IP réservée à l’aide du [portail Azure](http://portal.azure.com), vous pouvez spécifier le groupe de ressources de votre choix.</span><span class="sxs-lookup"><span data-stu-id="9fe65-154">If you create the reserved IP using the [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="9fe65-155">Cependant, si vous créez l’adresse IP réservée dans un groupe de ressources autres que *Default-Networking*, chaque fois que vous référencez l’adresse IP réservée avec des commandes telles que `Get-AzureReservedIP` et `Remove-AzureReservedIP`, vous devez référencer le nom *Group resource-group-name reserved-ip-name*.</span><span class="sxs-lookup"><span data-stu-id="9fe65-155">If you create the reserved IP in a resource group other than *Default-Networking* however, whenever you reference the reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference the name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="9fe65-156">Par exemple, si vous créez une adresse IP réservée nommée *myReservedIP* dans un groupe de ressources nommé *myResourceGroup*, vous devez référencer le nom de l’adresse IP réservée comme *Group myResourceGroup myReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="9fe65-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference the name of the reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="9fe65-157">Une fois une adresse IP réservée, elle reste associée à votre abonnement jusqu'à ce que vous la supprimiez.</span><span class="sxs-lookup"><span data-stu-id="9fe65-157">Once an IP is reserved, it remains associated to your subscription until you delete it.</span></span> <span data-ttu-id="9fe65-158">Pour supprimer une adresse IP réservée, exécutez la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="9fe65-158">To delete a reserved IP, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-the-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="9fe65-159">Réserver l’adresse IP d’un service cloud existant</span><span class="sxs-lookup"><span data-stu-id="9fe65-159">Reserve the IP address of an existing cloud service</span></span>
<span data-ttu-id="9fe65-160">Vous pouvez réserver l’adresse IP d’un service cloud existant en ajoutant le paramètre `-ServiceName`.</span><span class="sxs-lookup"><span data-stu-id="9fe65-160">You can reserve the IP address of an existing cloud service by adding the `-ServiceName` parameter.</span></span> <span data-ttu-id="9fe65-161">Pour réserver l’adresse IP d’un service cloud *TestService* dans les *États-Unis du Centre*, exécutez la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="9fe65-161">To reserve the IP address of a cloud service *TestService* in the *Central US* location, run the following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-to-a-new-cloud-service"></a><span data-ttu-id="9fe65-162">Associer une adresse IP réservée à un service cloud</span><span class="sxs-lookup"><span data-stu-id="9fe65-162">Associate a reserved IP to a new cloud service</span></span>
<span data-ttu-id="9fe65-163">Le script suivant crée une adresse IP réservée, puis l’associe à un nouveau service cloud nommé *TestService*.</span><span class="sxs-lookup"><span data-stu-id="9fe65-163">The following script creates a new reserved IP, then associates it to a new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="9fe65-164">Lorsque vous créez une adresse IP réservée à utiliser avec un service cloud, vous devez toujours faire référence à la machine virtuelle en utilisant *VIP:&lt;numéro de port>* pour les communications entrantes.</span><span class="sxs-lookup"><span data-stu-id="9fe65-164">When you create a reserved IP to use with a cloud service, you still refer to the VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="9fe65-165">Avoir une adresse IP réservée ne signifie pas que vous pouvez vous connecter directement à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9fe65-165">Reserving an IP does not mean you can connect to the VM directly.</span></span> <span data-ttu-id="9fe65-166">L'adresse IP réservée est affectée au service cloud sur lequel la machine virtuelle a été déployée.</span><span class="sxs-lookup"><span data-stu-id="9fe65-166">The reserved IP is assigned to the cloud service that the VM has been deployed to.</span></span> <span data-ttu-id="9fe65-167">Si vous souhaitez vous connecter à une machine virtuelle directement avec l’adresse IP, vous devez configurer une adresse IP publique de niveau de l'instance.</span><span class="sxs-lookup"><span data-stu-id="9fe65-167">If you want to connect to a VM by IP directly, you have to configure an instance-level public IP.</span></span> <span data-ttu-id="9fe65-168">Une adresse IP publique de niveau d'instance est un type d'adresse IP publique (appelée ILPIP) qui est affectée directement à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9fe65-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly to your VM.</span></span> <span data-ttu-id="9fe65-169">Elle ne peut pas être réservée.</span><span class="sxs-lookup"><span data-stu-id="9fe65-169">It cannot be reserved.</span></span> <span data-ttu-id="9fe65-170">Pour plus d’informations, consultez l’article [Adresses IP publiques de niveau d’instance (ILPIP)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="9fe65-170">For more information, read the [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="9fe65-171">Supprimer une adresse IP réservée d’un déploiement en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="9fe65-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="9fe65-172">Pour supprimer une adresse IP réservée ajoutée à un nouveau service cloud, exécutez la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="9fe65-172">To remove a reserved IP added to a new cloud service, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="9fe65-173">Si vous supprimez une adresse IP réservée d’un déploiement en cours d'exécution, la réservation ne sera pas supprimée de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="9fe65-173">Removing a reserved IP from a running deployment does not remove the reservation from your subscription.</span></span> <span data-ttu-id="9fe65-174">Cela libérera simplement l'adresse IP à utiliser par une autre ressource dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="9fe65-174">It simply frees the IP to be used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-to-a-running-deployment"></a><span data-ttu-id="9fe65-175">Associer une adresse IP réservée à un déploiement en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="9fe65-175">Associate a reserved IP to a running deployment</span></span>
<span data-ttu-id="9fe65-176">Les commandes suivantes créent un service cloud nommé *TestService2* avec une nouvelle machine virtuelle appelée *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="9fe65-176">The following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="9fe65-177">L’adresse IP réservée nommée *MyReservedIP* est ensuite associée au service cloud.</span><span class="sxs-lookup"><span data-stu-id="9fe65-177">The existing reserved IP named *MyReservedIP* is then associated to the cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="9fe65-178">Associer une adresse réservée à un service cloud à l’aide d’un fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="9fe65-178">Associate a reserved IP to a cloud service by using a service configuration file</span></span>
<span data-ttu-id="9fe65-179">Vous pouvez aussi associer une IP réservée à un service cloud à l’aide d’un fichier de configuration de service (CSCFG).</span><span class="sxs-lookup"><span data-stu-id="9fe65-179">You can also associate a reserved IP to a cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="9fe65-180">L’exemple de code xml suivant indique comment configurer un service cloud pour l’utilisation d’une adresse IP réservée nommée *MyReservedIP* :</span><span class="sxs-lookup"><span data-stu-id="9fe65-180">The following sample xml shows how to configure a cloud service to use a reserved VIP named *MyReservedIP*:</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a><span data-ttu-id="9fe65-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9fe65-181">Next steps</span></span>
* <span data-ttu-id="9fe65-182">Découvrez comment [l’adressage IP](virtual-network-ip-addresses-overview-classic.md) fonctionne dans le modèle de déploiement Classic.</span><span class="sxs-lookup"><span data-stu-id="9fe65-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="9fe65-183">En savoir plus sur [les adresses IP privées réservées](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="9fe65-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="9fe65-184">En savoir plus sur [les adresses IP publiques de niveau d’instance (ILPIP)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="9fe65-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

