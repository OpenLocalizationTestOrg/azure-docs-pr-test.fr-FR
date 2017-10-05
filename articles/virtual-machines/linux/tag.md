---
title: Comment baliser une machine virtuelle Azure Linux | Microsoft Docs
description: "Découvrez comment baliser une machine virtuelle Azure Linux créée dans Azure à l’aide du modèle de déploiement de Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: da3ff0de2a5d6ac8994b7c16b758f976228a53b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="cc73a-103">Comment baliser une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="cc73a-103">How to tag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="cc73a-104">Cet article décrit différentes façons d’ajouter des balises à une machine virtuelle Linux dans Azure à l’aide du modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cc73a-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="cc73a-105">Les balises sont des paires clé/valeur définies par l’utilisateur, qui peuvent être placées directement sur une ressource ou sur un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="cc73a-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="cc73a-106">Azure prend actuellement en charge jusqu’à 15 balises par ressource et par groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="cc73a-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="cc73a-107">Les balises peuvent être placées sur une ressource au moment de la création ou bien ajoutées à une ressource existante.</span><span class="sxs-lookup"><span data-stu-id="cc73a-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="cc73a-108">Notez que les balises ne sont prises en charge que pour les ressources créées via le modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cc73a-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="cc73a-109">Balisage avec l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="cc73a-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="cc73a-110">Pour commencer, vous devez disposer de la dernière version [d’Azure CLI 2.0 (version préliminaire)](/cli/azure/install-az-cli2) et vous connecter à un compte Azure avec la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="cc73a-110">To begin, you need the latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="cc73a-111">Vous pouvez également effectuer ces étapes à l’aide [d’Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc73a-111">You can also perform these steps with the [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="cc73a-112">Vous pouvez afficher toutes les propriétés d’une machine virtuelle donnée, y compris les balises, à l’aide de cette commande :</span><span class="sxs-lookup"><span data-stu-id="cc73a-112">You can view all properties for a given Virtual Machine, including the tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="cc73a-113">Pour ajouter une nouvelle balise de machine virtuelle via l'interface de ligne de commande Azure, vous pouvez utiliser la commande `azure vm update` avec le paramètre de balise **--set** :</span><span class="sxs-lookup"><span data-stu-id="cc73a-113">To add a new VM tag through the Azure CLI, you can use the `azure vm update` command along with the tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="cc73a-114">Pour supprimer les balises, vous pouvez utiliser le paramètre **--remove** dans la commande `azure vm update`.</span><span class="sxs-lookup"><span data-stu-id="cc73a-114">To remove tags, you can use the **--remove** parameter in the `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="cc73a-115">Maintenant que nous avons appliqué des balises à nos ressources via l’interface de ligne de commande et le portail, examinons les détails d’utilisation pour afficher les balises dans le portail de facturation.</span><span class="sxs-lookup"><span data-stu-id="cc73a-115">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="cc73a-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cc73a-116">Next steps</span></span>
* <span data-ttu-id="cc73a-117">Pour en savoir plus sur le balisage de vos ressources Azure, consultez la rubrique [Présentation d’Azure Resource Manager][Azure Resource Manager Overview] et [Organisation des ressources Azure à l’aide de balises][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="cc73a-117">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="cc73a-118">Pour voir en quoi les balises peuvent vous aider à gérer votre utilisation des ressources Azure, consultez [Comprendre votre facture Azure][Understanding your Azure Bill] et [Obtenir une vue d’ensemble de votre consommation des ressources Microsoft Azure][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="cc73a-118">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
