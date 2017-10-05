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
ms.openlocfilehash: f643001c85e127ae39e9869ffdc689bcac232ccb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="ba799-103">Comment baliser une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="ba799-103">How to tag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="ba799-104">Cet article décrit différentes façons d’ajouter des balises à une machine virtuelle Linux dans Azure à l’aide du modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ba799-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="ba799-105">Les balises sont des paires clé/valeur définies par l’utilisateur, qui peuvent être placées directement sur une ressource ou sur un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ba799-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="ba799-106">Azure prend actuellement en charge jusqu’à 15 balises par ressource et par groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ba799-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="ba799-107">Les balises peuvent être placées sur une ressource au moment de la création ou bien ajoutées à une ressource existante.</span><span class="sxs-lookup"><span data-stu-id="ba799-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="ba799-108">Notez que les balises ne sont prises en charge que pour les ressources créées via le modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ba799-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="ba799-109">Balisage avec l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="ba799-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="ba799-110">Pour commencer, [installez et configurez l’interface de ligne de commande Azure](../../xplat-cli-azure-resource-manager.md), et assurez-vous que vous êtes en mode Resource Manager (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="ba799-110">To begin, [install and configure the Azure CLI](../../xplat-cli-azure-resource-manager.md) and make sure you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="ba799-111">Vous pouvez afficher toutes les propriétés d’une machine virtuelle donnée, y compris les balises, à l’aide de cette commande :</span><span class="sxs-lookup"><span data-stu-id="ba799-111">You can view all properties for a given Virtual Machine, including the tags, using this command:</span></span>

        azure vm show -g MyResourceGroup -n MyTestVM

<span data-ttu-id="ba799-112">Pour ajouter une nouvelle balise de machine virtuelle via l'interface de ligne de commande Azure, vous pouvez utiliser la commande `azure vm set` avec le paramètre de balise **-t**:</span><span class="sxs-lookup"><span data-stu-id="ba799-112">To add a new VM tag through the Azure CLI, you can use the `azure vm set` command along with the tag parameter **-t**:</span></span>

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

<span data-ttu-id="ba799-113">Pour supprimer toutes les balises, vous pouvez utiliser le paramètre **–T** dans la commande `azure vm set`.</span><span class="sxs-lookup"><span data-stu-id="ba799-113">To remove all tags, you can use the **–T** parameter in the `azure vm set` command.</span></span>

        azure vm set – g MyResourceGroup –n MyTestVM -T


<span data-ttu-id="ba799-114">Maintenant que nous avons appliqué des balises à nos ressources via l’interface de ligne de commande et le portail, examinons les détails d’utilisation pour afficher les balises dans le portail de facturation.</span><span class="sxs-lookup"><span data-stu-id="ba799-114">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="ba799-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ba799-115">Next steps</span></span>
* <span data-ttu-id="ba799-116">Pour en savoir plus sur le balisage de vos ressources Azure, consultez la rubrique [Présentation d’Azure Resource Manager][Azure Resource Manager Overview] et [Organisation des ressources Azure à l’aide de balises][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="ba799-116">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="ba799-117">Pour voir en quoi les balises peuvent vous aider à gérer votre utilisation des ressources Azure, consultez [Comprendre votre facture Azure][Understanding your Azure Bill] et [Obtenir une vue d’ensemble de votre consommation des ressources Microsoft Azure][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="ba799-117">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
