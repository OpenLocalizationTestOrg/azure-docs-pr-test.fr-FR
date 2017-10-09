---
title: "aaaMove une machine virtuelle (classique) ou Services de cloud computing rôle instance tooa autre sous-réseau - Azure PowerShell | Documents Microsoft"
description: "Découvrez comment toomove machines virtuelles (classiques) et les instances de rôle des Services de cloud computing tooa autre sous-réseau à l’aide de PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d2de56f42a91be4a665414ea9641ffd46588fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a><span data-ttu-id="587e2-103">Déplacer une machine virtuelle (classique) ou les Services de cloud computing rôle instance tooa sous-réseau différent à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="587e2-103">Move a VM (Classic) or Cloud Services role instance tooa different subnet using PowerShell</span></span>
<span data-ttu-id="587e2-104">Vous pouvez utiliser PowerShell toomove vos machines virtuelles (classiques) à partir d’un sous-réseau tooanother Bonjour même réseau virtuel (VNet).</span><span class="sxs-lookup"><span data-stu-id="587e2-104">You can use PowerShell toomove your VMs (Classic) from one subnet tooanother in hello same virtual network (VNet).</span></span> <span data-ttu-id="587e2-105">Instances de rôle peuvent être déplacés en modifiant le fichier CSCFG de hello, plutôt qu’à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="587e2-105">Role instances can be moved by editing hello CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="587e2-106">Cet article explique comment les ordinateurs virtuels de toomove déployés via le modèle de déploiement classique hello uniquement.</span><span class="sxs-lookup"><span data-stu-id="587e2-106">This article explains how toomove VMs deployed through hello classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="587e2-107">Pourquoi déplacer des machines virtuelles tooanother sous-réseau ?</span><span class="sxs-lookup"><span data-stu-id="587e2-107">Why move VMs tooanother subnet?</span></span> <span data-ttu-id="587e2-108">Migration de sous-réseau est utile lorsque le sous-réseau plus ancien de hello est trop petite et ne peuvent pas être développée à l’échéance tooexisting machines virtuelles s’exécutant dans ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="587e2-108">Subnet migration is useful when hello older subnet is too small and cannot be expanded due tooexisting running VMs in that subnet.</span></span> <span data-ttu-id="587e2-109">Dans ce cas, vous pouvez créer un sous-réseau nouvelle et migrer de nouveau sous-réseau hello machines virtuelles toohello, puis une fois la migration terminée, vous pouvez supprimer le sous-réseau de vide ancien hello.</span><span class="sxs-lookup"><span data-stu-id="587e2-109">In that case, you can create a new, larger subnet and migrate hello VMs toohello new subnet, then after migration is complete, you can delete hello old empty subnet.</span></span>

## <a name="how-toomove-a-vm-tooanother-subnet"></a><span data-ttu-id="587e2-110">Comment toomove tooanother sous-réseau d’ordinateurs virtuels</span><span class="sxs-lookup"><span data-stu-id="587e2-110">How toomove a VM tooanother subnet</span></span>
<span data-ttu-id="587e2-111">toomove une machine virtuelle, exécutez hello Set-AzureSubnet applet de commande PowerShell à l’aide d’exemple hello ci-dessous comme modèle.</span><span class="sxs-lookup"><span data-stu-id="587e2-111">toomove a VM, run hello Set-AzureSubnet PowerShell cmdlet, using hello example below as a template.</span></span> <span data-ttu-id="587e2-112">Dans l’exemple hello ci-dessous, nous déplaçons TestVM de son sous-réseau actuel, tooSubnet-2.</span><span class="sxs-lookup"><span data-stu-id="587e2-112">In hello example below, we are moving TestVM from its present subnet, tooSubnet-2.</span></span> <span data-ttu-id="587e2-113">Être vraiment tooedit hello exemple tooreflect votre environnement.</span><span class="sxs-lookup"><span data-stu-id="587e2-113">Be sure tooedit hello example tooreflect your environment.</span></span> <span data-ttu-id="587e2-114">Notez que chaque fois que vous exécutez l’applet de commande Update-AzureVM hello dans le cadre d’une procédure, il redémarrera votre machine virtuelle dans le cadre du processus de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="587e2-114">Note that whenever you run hello Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of hello update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="587e2-115">Si vous avez spécifié une adresse IP privée interne statique pour votre machine virtuelle, vous devrez tooclear ce paramètre avant de pouvoir déplacer hello VM tooa sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="587e2-115">If you specified a static internal private IP for your VM, you'll have tooclear that setting before you can move hello VM tooa new subnet.</span></span> <span data-ttu-id="587e2-116">Dans ce cas, utilisez qui suit hello :</span><span class="sxs-lookup"><span data-stu-id="587e2-116">In that case, use hello following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a><span data-ttu-id="587e2-117">toomove un sous-réseau de tooanother instance rôle</span><span class="sxs-lookup"><span data-stu-id="587e2-117">toomove a role instance tooanother subnet</span></span>
<span data-ttu-id="587e2-118">toomove une instance de rôle, modifiez le fichier CSCFG de hello.</span><span class="sxs-lookup"><span data-stu-id="587e2-118">toomove a role instance, edit hello CSCFG file.</span></span> <span data-ttu-id="587e2-119">Dans l’exemple hello ci-dessous, nous déplaçons « Role0 » dans le réseau virtuel *VNETName* de son sous-réseau actuel trop*Subnet-2*.</span><span class="sxs-lookup"><span data-stu-id="587e2-119">In hello example below, we are moving "Role0" in virtual network *VNETName* from its present subnet too*Subnet-2*.</span></span> <span data-ttu-id="587e2-120">Étant donné que l’instance de rôle hello a déjà été déployé, vous devez juste modifier le nom du sous-réseau hello = Subnet-2.</span><span class="sxs-lookup"><span data-stu-id="587e2-120">Because hello role instance was already deployed, you'll just change hello Subnet name = Subnet-2.</span></span> <span data-ttu-id="587e2-121">Être vraiment tooedit hello exemple tooreflect votre environnement.</span><span class="sxs-lookup"><span data-stu-id="587e2-121">Be sure tooedit hello example tooreflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
