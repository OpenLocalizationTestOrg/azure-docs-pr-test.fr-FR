---
title: aaaHow tootag une machine virtuelle de Azure Linux | Documents Microsoft
description: "En savoir plus sur le balisage d’une machine virtuelle de Azure Linux créée dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources hello."
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
ms.openlocfilehash: 0e99ea66a87b7e00eb21a2f72dd2bce8673778dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="220e0-103">Comment tootag une machine virtuelle de Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="220e0-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="220e0-104">Cet article décrit les différentes façons tootag une machine virtuelle de Linux dans Azure via le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="220e0-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="220e0-105">Les balises sont des paires clé/valeur définies par l’utilisateur, qui peuvent être placées directement sur une ressource ou sur un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="220e0-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="220e0-106">Azure prend actuellement en charge des balises de too15 par la ressource et le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="220e0-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="220e0-107">Balises peuvent être placées sur une ressource au moment de la création de hello ou ajouté tooan les ressources existantes.</span><span class="sxs-lookup"><span data-stu-id="220e0-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="220e0-108">Notez les balises sont pris en charge pour les ressources créées via le modèle de déploiement Resource Manager hello uniquement.</span><span class="sxs-lookup"><span data-stu-id="220e0-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="220e0-109">Balisage avec l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="220e0-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="220e0-110">toobegin, [installer et configurer hello CLI d’Azure](../../xplat-cli-azure-resource-manager.md) et assurez-vous que vous êtes en mode de gestionnaire de ressources (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="220e0-110">toobegin, [install and configure hello Azure CLI](../../xplat-cli-azure-resource-manager.md) and make sure you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="220e0-111">Vous pouvez afficher toutes les propriétés d’un ordinateur virtuel donné, y compris les balises de hello, à l’aide de cette commande :</span><span class="sxs-lookup"><span data-stu-id="220e0-111">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        azure vm show -g MyResourceGroup -n MyTestVM

<span data-ttu-id="220e0-112">tooadd une nouvelle balise de machine virtuelle via hello CLI d’Azure, vous pouvez utiliser hello `azure vm set` commande en même temps que le paramètre de la balise hello **-t**:</span><span class="sxs-lookup"><span data-stu-id="220e0-112">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm set` command along with hello tag parameter **-t**:</span></span>

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

<span data-ttu-id="220e0-113">tooremove toutes les balises, vous pouvez utiliser hello **– T** paramètre Bonjour `azure vm set` commande.</span><span class="sxs-lookup"><span data-stu-id="220e0-113">tooremove all tags, you can use hello **–T** parameter in hello `azure vm set` command.</span></span>

        azure vm set – g MyResourceGroup –n MyTestVM -T


<span data-ttu-id="220e0-114">Maintenant que nous ont appliqué les balises tooour ressources CLI d’Azure et hello Portal, examinons un toosee de détails d’utilisation hello les balises hello dans le portail de facturation hello.</span><span class="sxs-lookup"><span data-stu-id="220e0-114">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="220e0-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="220e0-115">Next steps</span></span>
* <span data-ttu-id="220e0-116">toolearn en savoir plus sur le marquage de vos ressources Azure, consultez [vue d’ensemble du Gestionnaire de ressources Azure] [ Azure Resource Manager Overview] et [à l’aide de balises tooorganize vos ressources Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="220e0-116">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="220e0-117">toosee balises peuvent vous aider à gérer votre utilisation des ressources Azure, voir [comprendre votre facture Azure] [ Understanding your Azure Bill] et [obtenir votre consommation de ressources Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="220e0-117">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
