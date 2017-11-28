---
title: "exemple de script CLI aaaAzure - le trafic réseau de machine virtuelle de filtre | Documents Microsoft"
description: "Exemple de script Azure CLI - Filtrer le trafic réseau de machine virtuelle entrant et sortant"
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="a9692-103">Filtrer le trafic réseau de machine virtuelle entrant et sortant</span><span class="sxs-lookup"><span data-stu-id="a9692-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="a9692-104">Cet exemple de script permet de créer un réseau virtuel avec des sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="a9692-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="a9692-105">Le trafic du réseau entrant toohello le sous-réseau frontal est limitée tooHTTP, HTTPS et SSH, pendant sortant du trafic toohello Internet à partir du sous-réseau de hello principal n’est pas autorisée.</span><span class="sxs-lookup"><span data-stu-id="a9692-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="a9692-106">Après avoir exécuté le script de hello, vous aurez une machine virtuelle avec deux cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="a9692-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="a9692-107">Chaque carte réseau est connectée tooa autre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="a9692-107">Each NIC is connected tooa different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a9692-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="a9692-108">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a9692-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="a9692-109">Clean up deployment</span></span> 

<span data-ttu-id="a9692-110">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="a9692-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="a9692-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="a9692-111">Script explanation</span></span>

<span data-ttu-id="a9692-112">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, de réseau virtuel et de groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="a9692-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="a9692-113">Chaque commande dans la table de hello lie documentation toocommand spécifique.</span><span class="sxs-lookup"><span data-stu-id="a9692-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="a9692-114">Commande</span><span class="sxs-lookup"><span data-stu-id="a9692-114">Command</span></span> | <span data-ttu-id="a9692-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="a9692-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a9692-116">az group create</span><span class="sxs-lookup"><span data-stu-id="a9692-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="a9692-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="a9692-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a9692-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="a9692-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="a9692-119">Crée un réseau virtuel et un sous-réseau frontal Azure.</span><span class="sxs-lookup"><span data-stu-id="a9692-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="a9692-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="a9692-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="a9692-121">Crée un sous-réseau principal.</span><span class="sxs-lookup"><span data-stu-id="a9692-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="a9692-122">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="a9692-122">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="a9692-123">Associe les groupes de sécurité réseau toosubnets.</span><span class="sxs-lookup"><span data-stu-id="a9692-123">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="a9692-124">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="a9692-124">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="a9692-125">Crée un Bonjour de tooaccess adresse IP publique machine virtuelle à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="a9692-125">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="a9692-126">az network nic create</span><span class="sxs-lookup"><span data-stu-id="a9692-126">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="a9692-127">Crée des interfaces réseau virtuelles et les attacher à des sous-réseaux du réseau virtuel toohello frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="a9692-127">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="a9692-128">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="a9692-128">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="a9692-129">Crée des groupes de sécurité réseau (NSG) qui sont des sous-réseaux frontaux et principaux toohello associé.</span><span class="sxs-lookup"><span data-stu-id="a9692-129">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="a9692-130">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="a9692-130">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="a9692-131">Crée des règles de groupe de sécurité réseau autoriser ou bloquent des sous-réseaux toospecific de ports spécifiques.</span><span class="sxs-lookup"><span data-stu-id="a9692-131">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="a9692-132">az vm create</span><span class="sxs-lookup"><span data-stu-id="a9692-132">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="a9692-133">Crée des machines virtuelles et attache un tooeach de carte réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a9692-133">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="a9692-134">Cette commande spécifie également hello machine virtuelle image toouse et les informations d’identification administratives.</span><span class="sxs-lookup"><span data-stu-id="a9692-134">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="a9692-135">az group delete</span><span class="sxs-lookup"><span data-stu-id="a9692-135">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="a9692-136">Supprime un groupe de ressources, ainsi que toutes ses ressources.</span><span class="sxs-lookup"><span data-stu-id="a9692-136">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a9692-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9692-137">Next steps</span></span>

<span data-ttu-id="a9692-138">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a9692-138">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="a9692-139">Vous trouverez des exemples de script CLI mise en réseau supplémentaires dans hello [documentation de vue d’ensemble de la mise en réseau Azure](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="a9692-139">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
