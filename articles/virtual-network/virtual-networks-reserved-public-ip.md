---
title: "aaaManage Azure réservée d’adresses IP (classiques) - PowerShell | Documents Microsoft"
description: "Comprendre les adresses IP réservées (classiques) et comment toomanage les à l’aide de PowerShell."
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
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="1eb81-103">Adresses IP réservées (Classic)</span><span class="sxs-lookup"><span data-stu-id="1eb81-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1eb81-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="1eb81-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="1eb81-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1eb81-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="1eb81-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="1eb81-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="1eb81-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="1eb81-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="1eb81-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="1eb81-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="1eb81-109">Il existe deux catégories d’adresses IP dans Azure, les réservées et les dynamiques.</span><span class="sxs-lookup"><span data-stu-id="1eb81-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="1eb81-110">Les adresses IP publiques gérées par Azure sont dynamiques par défaut.</span><span class="sxs-lookup"><span data-stu-id="1eb81-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="1eb81-111">Que signifie que hello adresse IP utilisée pour un service de cloud donné (VIP) ou un tooaccess une machine virtuelle ou instance de rôle directement (ILPIP) peut changer à partir de l’heure tootime, lorsque des ressources sont arrêter ou arrêtés (désallouées).</span><span class="sxs-lookup"><span data-stu-id="1eb81-111">That means that hello IP address used for a given cloud service (VIP) or tooaccess a VM or role instance directly (ILPIP) can change from time tootime, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="1eb81-112">tooprevent les adresses IP à partir de la modification, vous pouvez réserver une adresse IP.</span><span class="sxs-lookup"><span data-stu-id="1eb81-112">tooprevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="1eb81-113">Adresses IP réservées peuvent être utilisé uniquement comme une adresse IP virtuelle, vous être assuré de cette adresse IP de hello pour le service cloud hello reste hello identiques, même si les ressources sont arrêtés ou arrêtée (désallouée).</span><span class="sxs-lookup"><span data-stu-id="1eb81-113">Reserved IPs can be used only as a VIP, ensuring that hello IP address for hello cloud service remains hello same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="1eb81-114">En outre, vous pouvez convertir des adresses IP dynamiques existante utilisée comme adresse IP VIP tooa réservé.</span><span class="sxs-lookup"><span data-stu-id="1eb81-114">Furthermore, you can convert existing dynamic IPs used as a VIP tooa reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1eb81-115">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1eb81-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1eb81-116">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="1eb81-116">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="1eb81-117">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="1eb81-117">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="1eb81-118">Découvrez comment un statique publique IP adresse à l’aide de tooreserve hello [modèle de déploiement de gestionnaire de ressources](virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="1eb81-118">Learn how tooreserve a static public IP address using hello [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="1eb81-119">toolearn savoir plus sur IP adresses dans Azure, lisez hello [des adresses IP](virtual-network-ip-addresses-overview-classic.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="1eb81-119">toolearn more about IP addresses in Azure, read hello [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="1eb81-120">Quand ai-je besoin d’une adresse IP réservée ?</span><span class="sxs-lookup"><span data-stu-id="1eb81-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="1eb81-121">**Vous souhaitez tooensure qui hello IP est réservée dans votre abonnement**.</span><span class="sxs-lookup"><span data-stu-id="1eb81-121">**You want tooensure that hello IP is reserved in your subscription**.</span></span> <span data-ttu-id="1eb81-122">Si vous souhaitez tooreserve une adresse IP qui n’est pas libérée à partir de votre abonnement dans aucune circonstance, vous devez utiliser une adresse IP publique réservée.</span><span class="sxs-lookup"><span data-stu-id="1eb81-122">If you want tooreserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="1eb81-123">**Vous souhaitez que votre toostay IP avec votre service cloud même à travers arrêté ou désalloué (machines virtuelles) d’état**.</span><span class="sxs-lookup"><span data-stu-id="1eb81-123">**You want your IP toostay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="1eb81-124">Si vous souhaitez que votre toobe service accessible à l’aide d’une adresse IP qui ne change pas, même lorsque le cloud de machines virtuelles dans hello service sont arrêtés ou l’arrêter (libéré).</span><span class="sxs-lookup"><span data-stu-id="1eb81-124">If you want your service toobe accessed by using an IP address that doesn't change, even when VMs in hello cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="1eb81-125">**Vous souhaitez que le trafic sortant d’Azure utilise une adresse IP prévisible de tooensure**.</span><span class="sxs-lookup"><span data-stu-id="1eb81-125">**You want tooensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="1eb81-126">Vous avez peut-être votre local configuré le pare-feu tooallow uniquement le trafic d’adresses IP spécifiques.</span><span class="sxs-lookup"><span data-stu-id="1eb81-126">You may have your on-premises firewall configured tooallow only traffic from specific IP addresses.</span></span> <span data-ttu-id="1eb81-127">En réservant une adresse IP, vous connaissez l’adresse IP source hello d’adresses et n’avez pas besoin de tooupdate votre pare-feu règles en raison de la modification de tooan IP.</span><span class="sxs-lookup"><span data-stu-id="1eb81-127">By reserving an IP, you know hello source IP address, and don't need tooupdate your firewall rules due tooan IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="1eb81-128">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="1eb81-128">FAQ</span></span>
1. <span data-ttu-id="1eb81-129">Puis-je utiliser une adresse IP réservée pour tous les services Azure ?</span><span class="sxs-lookup"><span data-stu-id="1eb81-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="1eb81-130">Non.</span><span class="sxs-lookup"><span data-stu-id="1eb81-130">No.</span></span> <span data-ttu-id="1eb81-131">Les adresses IP réservées peuvent être utilisées uniquement pour les machines virtuelles et les rôles d'instance de service cloud exposés par une adresse IP virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1eb81-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="1eb81-132">Combien d’adresses IP réservées puis-je avoir ?</span><span class="sxs-lookup"><span data-stu-id="1eb81-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="1eb81-133">Pour plus d’informations, consultez hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.</span><span class="sxs-lookup"><span data-stu-id="1eb81-133">For details, see hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="1eb81-134">L’obtention d’adresses IP réservées est-elle payante ?</span><span class="sxs-lookup"><span data-stu-id="1eb81-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="1eb81-135">Parfois.</span><span class="sxs-lookup"><span data-stu-id="1eb81-135">Sometimes.</span></span> <span data-ttu-id="1eb81-136">Pour plus d’informations de tarification, consultez hello [détails de tarification de l’adresse IP réservée](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span><span class="sxs-lookup"><span data-stu-id="1eb81-136">For pricing details, see hello [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="1eb81-137">Comment réserver une adresse IP ?</span><span class="sxs-lookup"><span data-stu-id="1eb81-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="1eb81-138">Vous pouvez utiliser PowerShell, hello [API REST de gestion Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), ou hello [portail Azure](https://portal.azure.com) tooreserve une adresse IP dans une région Azure.</span><span class="sxs-lookup"><span data-stu-id="1eb81-138">You can use PowerShell, hello [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or hello [Azure portal](https://portal.azure.com) tooreserve an IP address in an Azure region.</span></span> <span data-ttu-id="1eb81-139">Une adresse IP réservée est associée tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="1eb81-139">A reserved IP address is associated tooyour subscription.</span></span>
5. <span data-ttu-id="1eb81-140">Puis-je utiliser une adresse IP réservée avec des réseaux virtuels basés sur un groupe d'affinités ?</span><span class="sxs-lookup"><span data-stu-id="1eb81-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="1eb81-141">Non.</span><span class="sxs-lookup"><span data-stu-id="1eb81-141">No.</span></span> <span data-ttu-id="1eb81-142">Les adresses IP réservées sont uniquement prises en charge dans les réseaux virtuels régionaux.</span><span class="sxs-lookup"><span data-stu-id="1eb81-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="1eb81-143">Les adresses IP réservées ne sont pas prises en charge dans les réseaux virtuels associés à des groupes d’affinités.</span><span class="sxs-lookup"><span data-stu-id="1eb81-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="1eb81-144">Pour plus d’informations sur l’association d’un réseau virtuel avec une région ou un groupe d’affinités, consultez hello [sur des réseaux virtuels régionaux et des groupes d’affinités](virtual-networks-migrate-to-regional-vnet.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="1eb81-144">For more information about associating a VNet with a region or affinity group, see hello [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="1eb81-145">Gérer les adresses IP virtuelles réservées</span><span class="sxs-lookup"><span data-stu-id="1eb81-145">Manage reserved VIPs</span></span>

<span data-ttu-id="1eb81-146">Assurez-vous d’avoir installé et configuré PowerShell en effectuant les étapes hello Bonjour [installer et configurer PowerShell](/powershell/azure/overview) l’article.</span><span class="sxs-lookup"><span data-stu-id="1eb81-146">Ensure you have installed and configured PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="1eb81-147">Avant de pouvoir utiliser des adresses IP réservées, vous devez l’ajouter tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="1eb81-147">Before you can use reserved IPs, you must add it tooyour subscription.</span></span> <span data-ttu-id="1eb81-148">toocreate une adresse IP réservée à partir du pool hello de l’adresse IP publique adresses disponibles dans hello *du centre des États-Unis* emplacement, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1eb81-148">toocreate a reserved IP from hello pool of public IP addresses available in hello *Central US* location, run hello following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="1eb81-149">Toutefois, veuillez noter que vous ne pouvez pas spécifier quelle adresse IP vous souhaitez réserver.</span><span class="sxs-lookup"><span data-stu-id="1eb81-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="1eb81-150">tooview quelles sont les adresses IP sont réservées dans votre abonnement, exécutez hello suivant de commande PowerShell et notez les valeurs hello pour *ReservedIPName* et *adresse*:</span><span class="sxs-lookup"><span data-stu-id="1eb81-150">tooview what IP addresses are reserved in your subscription, run hello following PowerShell command, and notice hello values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="1eb81-151">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="1eb81-151">Expected output:</span></span>

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
><span data-ttu-id="1eb81-152">Lorsque vous créez une adresse IP réservée avec PowerShell, vous ne pouvez pas spécifier une groupe ressource toocreate adresse IP hello réservé dans.</span><span class="sxs-lookup"><span data-stu-id="1eb81-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group toocreate hello reserved IP in.</span></span> <span data-ttu-id="1eb81-153">Azure place automatiquement cette adresse dans un groupe de ressources nommé *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="1eb81-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="1eb81-154">Si vous créez IP hello réservé à l’aide de hello [portail Azure](http://portal.azure.com), vous pouvez spécifier n’importe quel groupe de ressources que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="1eb81-154">If you create hello reserved IP using hello [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="1eb81-155">Si vous créez hello réservée IP dans un groupe de ressources autre que *réseau par défaut* Toutefois, chaque fois que vous référencez hello IP réservée avec les commandes telles que `Get-AzureReservedIP` et `Remove-AzureReservedIP`, vous devez référencer le nom hello *-Nom d’ip réservée nom du groupe de ressources du groupe*.</span><span class="sxs-lookup"><span data-stu-id="1eb81-155">If you create hello reserved IP in a resource group other than *Default-Networking* however, whenever you reference hello reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference hello name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="1eb81-156">Par exemple, si vous créez une adresse IP réservée nommée *myReservedIP* dans un groupe de ressources nommé *myResourceGroup*, vous devez référencer le nom hello de l’adresse IP hello réservé en tant que *myResourceGroup de groupe myReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="1eb81-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference hello name of hello reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="1eb81-157">Une fois qu’une adresse IP est réservée, il reste associé tooyour abonnement jusqu'à ce que vous la supprimiez.</span><span class="sxs-lookup"><span data-stu-id="1eb81-157">Once an IP is reserved, it remains associated tooyour subscription until you delete it.</span></span> <span data-ttu-id="1eb81-158">toodelete une adresse IP réservée, hello exécution suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="1eb81-158">toodelete a reserved IP, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="1eb81-159">Réserver l’adresse IP de hello d’un service cloud existant</span><span class="sxs-lookup"><span data-stu-id="1eb81-159">Reserve hello IP address of an existing cloud service</span></span>
<span data-ttu-id="1eb81-160">Vous pouvez réserver l’adresse IP de hello d’un service cloud existant en ajoutant hello `-ServiceName` paramètre.</span><span class="sxs-lookup"><span data-stu-id="1eb81-160">You can reserve hello IP address of an existing cloud service by adding hello `-ServiceName` parameter.</span></span> <span data-ttu-id="1eb81-161">adresse tooreserve hello d’un service cloud *TestService* Bonjour *du centre des États-Unis* emplacement, exécutez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="1eb81-161">tooreserve hello IP address of a cloud service *TestService* in hello *Central US* location, run hello following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a><span data-ttu-id="1eb81-162">Associer un réservée IP tooa nouveau service cloud</span><span class="sxs-lookup"><span data-stu-id="1eb81-162">Associate a reserved IP tooa new cloud service</span></span>
<span data-ttu-id="1eb81-163">Hello script suivant crée une adresse IP réservée de nouveau, puis il associe le nouveau service de cloud tooa nommé *TestService*.</span><span class="sxs-lookup"><span data-stu-id="1eb81-163">hello following script creates a new reserved IP, then associates it tooa new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="1eb81-164">Lorsque vous créez un toouse IP réservée avec un service cloud, vous consultez toujours toohello machine virtuelle à l’aide de *VIP :&lt;numéro de port >* pour les communications entrantes.</span><span class="sxs-lookup"><span data-stu-id="1eb81-164">When you create a reserved IP toouse with a cloud service, you still refer toohello VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="1eb81-165">Réserver une adresse IP ne signifie pas que vous pouvez connecter directement toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1eb81-165">Reserving an IP does not mean you can connect toohello VM directly.</span></span> <span data-ttu-id="1eb81-166">Hello IP réservée est affectée toohello cloud service ce hello machine virtuelle a été déployée.</span><span class="sxs-lookup"><span data-stu-id="1eb81-166">hello reserved IP is assigned toohello cloud service that hello VM has been deployed to.</span></span> <span data-ttu-id="1eb81-167">Si vous souhaitez tooconnect tooa VM par IP directement, vous avez tooconfigure une adresse IP publique de niveau de l’instance.</span><span class="sxs-lookup"><span data-stu-id="1eb81-167">If you want tooconnect tooa VM by IP directly, you have tooconfigure an instance-level public IP.</span></span> <span data-ttu-id="1eb81-168">Une adresse IP publique de niveau de l’instance est un type d’adresse IP publique (appelé un ILPIP) qui est directement affectée tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1eb81-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly tooyour VM.</span></span> <span data-ttu-id="1eb81-169">Elle ne peut pas être réservée.</span><span class="sxs-lookup"><span data-stu-id="1eb81-169">It cannot be reserved.</span></span> <span data-ttu-id="1eb81-170">Pour plus d’informations, consultez hello [IP publique de niveau de l’Instance (ILPIP)](virtual-networks-instance-level-public-ip.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="1eb81-170">For more information, read hello [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="1eb81-171">Supprimer une adresse IP réservée d’un déploiement en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="1eb81-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="1eb81-172">tooremove une adresse IP réservée ajouté un nouveau service de cloud tooa, exécutez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="1eb81-172">tooremove a reserved IP added tooa new cloud service, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="1eb81-173">Suppression d’une adresse IP réservée à partir d’un déploiement en cours d’exécution ne supprime pas de réservation de hello à partir de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="1eb81-173">Removing a reserved IP from a running deployment does not remove hello reservation from your subscription.</span></span> <span data-ttu-id="1eb81-174">Elle libère simplement hello IP toobe est utilisé par une autre ressource dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="1eb81-174">It simply frees hello IP toobe used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a><span data-ttu-id="1eb81-175">Associer un tooa IP réservée déploiement en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="1eb81-175">Associate a reserved IP tooa running deployment</span></span>
<span data-ttu-id="1eb81-176">Hello commandes suivantes créent un service cloud nommé *TestService2* avec un nouvel ordinateur virtuel nommé *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="1eb81-176">hello following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="1eb81-177">Hello existant réservée IP nommé *MyReservedIP* est ensuite le service de cloud computing toohello associé.</span><span class="sxs-lookup"><span data-stu-id="1eb81-177">hello existing reserved IP named *MyReservedIP* is then associated toohello cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="1eb81-178">Associer un service de cloud tooa IP réservé à l’aide d’un fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="1eb81-178">Associate a reserved IP tooa cloud service by using a service configuration file</span></span>
<span data-ttu-id="1eb81-179">Vous pouvez également associer un service de cloud tooa IP réservé à l’aide d’un fichier de configuration (CSCFG) du service.</span><span class="sxs-lookup"><span data-stu-id="1eb81-179">You can also associate a reserved IP tooa cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="1eb81-180">Hello exemple de code xml suivant montre comment tooconfigure un toouse de service cloud une adresse IP virtuelle réservée nommée *MyReservedIP*:</span><span class="sxs-lookup"><span data-stu-id="1eb81-180">hello following sample xml shows how tooconfigure a cloud service toouse a reserved VIP named *MyReservedIP*:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1eb81-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1eb81-181">Next steps</span></span>
* <span data-ttu-id="1eb81-182">Comprendre comment [l’adressage IP](virtual-network-ip-addresses-overview-classic.md) fonctionne dans le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="1eb81-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="1eb81-183">En savoir plus sur [les adresses IP privées réservées](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="1eb81-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="1eb81-184">En savoir plus sur [les adresses IP publiques de niveau d’instance (ILPIP)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="1eb81-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

