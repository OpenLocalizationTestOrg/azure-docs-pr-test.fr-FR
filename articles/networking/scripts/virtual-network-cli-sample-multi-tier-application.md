---
title: "script CLI aaaAzure exemple : création d’un réseau pour les applications multicouches | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer un réseau pour les applications multiniveau."
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
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="10d1b-103">Créer un réseau pour les applications multiniveau</span><span class="sxs-lookup"><span data-stu-id="10d1b-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="10d1b-104">Cet exemple de script permet de créer un réseau virtuel avec des sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="10d1b-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="10d1b-105">Sous-réseau de trafic toohello frontal est limitée tooHTTP et SSH, lors du trafic toohello sous-réseau principal est limitée tooMySQL, port 3306.</span><span class="sxs-lookup"><span data-stu-id="10d1b-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="10d1b-106">Après l’exécution du script hello, vous aurez deux machines virtuelles, une dans chaque sous-réseau que vous pouvez déployer le serveur web et le logiciel MySQL.</span><span class="sxs-lookup"><span data-stu-id="10d1b-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="10d1b-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="10d1b-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="10d1b-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="10d1b-108">Clean up deployment</span></span> 

<span data-ttu-id="10d1b-109">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="10d1b-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="10d1b-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="10d1b-110">Script explanation</span></span>

<span data-ttu-id="10d1b-111">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, de réseau virtuel et de groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="10d1b-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="10d1b-112">Chaque commande dans la table de hello lie documentation toocommand spécifique.</span><span class="sxs-lookup"><span data-stu-id="10d1b-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="10d1b-113">Commande</span><span class="sxs-lookup"><span data-stu-id="10d1b-113">Command</span></span> | <span data-ttu-id="10d1b-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="10d1b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="10d1b-115">az group create</span><span class="sxs-lookup"><span data-stu-id="10d1b-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="10d1b-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="10d1b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="10d1b-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="10d1b-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="10d1b-118">Crée un réseau virtuel et un sous-réseau frontal Azure.</span><span class="sxs-lookup"><span data-stu-id="10d1b-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="10d1b-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="10d1b-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="10d1b-120">Crée un sous-réseau principal.</span><span class="sxs-lookup"><span data-stu-id="10d1b-120">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="10d1b-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="10d1b-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="10d1b-122">Crée un Bonjour de tooaccess adresse IP publique machine virtuelle à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="10d1b-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="10d1b-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="10d1b-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="10d1b-124">Crée des interfaces réseau virtuelles et les attacher à des sous-réseaux du réseau virtuel toohello frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="10d1b-124">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="10d1b-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="10d1b-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="10d1b-126">Crée des groupes de sécurité réseau (NSG) qui sont des sous-réseaux frontaux et principaux toohello associé.</span><span class="sxs-lookup"><span data-stu-id="10d1b-126">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="10d1b-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="10d1b-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="10d1b-128">Crée des règles de groupe de sécurité réseau autoriser ou bloquent des sous-réseaux toospecific de ports spécifiques.</span><span class="sxs-lookup"><span data-stu-id="10d1b-128">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="10d1b-129">az vm create</span><span class="sxs-lookup"><span data-stu-id="10d1b-129">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="10d1b-130">Crée des machines virtuelles et attache un tooeach de carte réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="10d1b-130">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="10d1b-131">Cette commande spécifie également hello machine virtuelle image toouse et les informations d’identification administratives.</span><span class="sxs-lookup"><span data-stu-id="10d1b-131">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="10d1b-132">az group delete</span><span class="sxs-lookup"><span data-stu-id="10d1b-132">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="10d1b-133">Supprime un groupe de ressources, ainsi que toutes ses ressources.</span><span class="sxs-lookup"><span data-stu-id="10d1b-133">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="10d1b-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="10d1b-134">Next steps</span></span>

<span data-ttu-id="10d1b-135">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="10d1b-135">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="10d1b-136">Vous trouverez des exemples de script CLI mise en réseau supplémentaires dans hello [documentation de vue d’ensemble de la mise en réseau Azure](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="10d1b-136">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
