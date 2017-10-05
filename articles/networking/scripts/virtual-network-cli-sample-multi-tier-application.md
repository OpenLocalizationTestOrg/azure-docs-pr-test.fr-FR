---
title: "Exemple de script Azure CLI - Créer un réseau pour les applications multiniveau | Microsoft Docs"
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
ms.openlocfilehash: de65d820f2d9eea49b58185c81d815675fd76740
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="ccaaa-103">Créer un réseau pour les applications multiniveau</span><span class="sxs-lookup"><span data-stu-id="ccaaa-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="ccaaa-104">Cet exemple de script permet de créer un réseau virtuel avec des sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="ccaaa-105">Le trafic vers le sous-réseau frontal est limité à HTTP et SSH, tandis que le trafic vers le sous-réseau principal est limité à MySQL, port 3306.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="ccaaa-106">Après avoir exécuté le script, vous obtenez deux machines virtuelles, une dans chaque sous-réseau sur laquelle que vous pouvez déployer le serveur web et le logiciel MySQL.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="ccaaa-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="ccaaa-107">Sample script</span></span>


<span data-ttu-id="ccaaa-108">[!code-azurecli-interactive[principal](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Créer un réseau virtuel pour les applications multiniveau")]</span><span class="sxs-lookup"><span data-stu-id="ccaaa-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ccaaa-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="ccaaa-109">Clean up deployment</span></span> 

<span data-ttu-id="ccaaa-110">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="ccaaa-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="ccaaa-111">Script explanation</span></span>

<span data-ttu-id="ccaaa-112">Ce script utilise les commandes suivantes pour créer un groupe de ressources, un réseau virtuel et les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="ccaaa-113">Chaque commande de la table renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="ccaaa-114">Commande</span><span class="sxs-lookup"><span data-stu-id="ccaaa-114">Command</span></span> | <span data-ttu-id="ccaaa-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="ccaaa-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ccaaa-116">az group create</span><span class="sxs-lookup"><span data-stu-id="ccaaa-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="ccaaa-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ccaaa-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="ccaaa-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="ccaaa-119">Crée un réseau virtuel et un sous-réseau frontal Azure.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="ccaaa-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="ccaaa-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="ccaaa-121">Crée un sous-réseau principal.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="ccaaa-122">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="ccaaa-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="ccaaa-123">Crée une adresse IP publique pour accéder à la machine virtuelle à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="ccaaa-124">az network nic create</span><span class="sxs-lookup"><span data-stu-id="ccaaa-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="ccaaa-125">Crée des interfaces réseau virtuelles et les attache aux sous-réseaux frontaux et principaux du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-125">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="ccaaa-126">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="ccaaa-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="ccaaa-127">Crée des groupes de sécurité réseau (NSG) associés aux sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-127">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="ccaaa-128">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="ccaaa-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="ccaaa-129">Crée des règles NSG qui autorisent ou bloquent des ports spécifiques sur des sous-réseaux donnés.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-129">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="ccaaa-130">az vm create</span><span class="sxs-lookup"><span data-stu-id="ccaaa-130">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="ccaaa-131">Crée des machines virtuelles et associe une carte d’interface réseau à chacune d’elles.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-131">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="ccaaa-132">Cette commande spécifie également l’image de machine virtuelle à utiliser ainsi que les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-132">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="ccaaa-133">az group delete</span><span class="sxs-lookup"><span data-stu-id="ccaaa-133">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="ccaaa-134">Supprime un groupe de ressources, ainsi que toutes ses ressources.</span><span class="sxs-lookup"><span data-stu-id="ccaaa-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ccaaa-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ccaaa-135">Next steps</span></span>

<span data-ttu-id="ccaaa-136">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ccaaa-136">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="ccaaa-137">Vous pouvez trouver des exemples supplémentaires de scripts CLI de mise en réseau dans la [documentation Vue d’ensemble de la mise en réseau Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ccaaa-137">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>