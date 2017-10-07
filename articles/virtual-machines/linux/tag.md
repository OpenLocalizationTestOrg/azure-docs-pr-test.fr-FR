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
ms.openlocfilehash: 456b226af4495c3b446cb79c99cf9494dde9fca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="f6c00-103">Comment tootag une machine virtuelle de Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="f6c00-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="f6c00-104">Cet article décrit les différentes façons tootag une machine virtuelle de Linux dans Azure via le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f6c00-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="f6c00-105">Les balises sont des paires clé/valeur définies par l’utilisateur, qui peuvent être placées directement sur une ressource ou sur un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f6c00-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="f6c00-106">Azure prend actuellement en charge des balises de too15 par la ressource et le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f6c00-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="f6c00-107">Balises peuvent être placées sur une ressource au moment de la création de hello ou ajouté tooan les ressources existantes.</span><span class="sxs-lookup"><span data-stu-id="f6c00-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="f6c00-108">Notez les balises sont pris en charge pour les ressources créées via le modèle de déploiement Resource Manager hello uniquement.</span><span class="sxs-lookup"><span data-stu-id="f6c00-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="f6c00-109">Balisage avec l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f6c00-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="f6c00-110">toobegin, vous devez hello dernières [Azure CLI 2.0 (version préliminaire)](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f6c00-110">toobegin, you need hello latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="f6c00-111">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f6c00-111">You can also perform these steps with hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="f6c00-112">Vous pouvez afficher toutes les propriétés d’un ordinateur virtuel donné, y compris les balises de hello, à l’aide de cette commande :</span><span class="sxs-lookup"><span data-stu-id="f6c00-112">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="f6c00-113">tooadd une nouvelle balise de machine virtuelle via hello CLI d’Azure, vous pouvez utiliser hello `azure vm update` commande en même temps que le paramètre de la balise hello **--définir**:</span><span class="sxs-lookup"><span data-stu-id="f6c00-113">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm update` command along with hello tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="f6c00-114">les balises tooremove, vous pouvez utiliser hello **--supprimer** paramètre Bonjour `azure vm update` commande.</span><span class="sxs-lookup"><span data-stu-id="f6c00-114">tooremove tags, you can use hello **--remove** parameter in hello `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="f6c00-115">Maintenant que nous ont appliqué les balises tooour ressources CLI d’Azure et hello Portal, examinons un toosee de détails d’utilisation hello les balises hello dans le portail de facturation hello.</span><span class="sxs-lookup"><span data-stu-id="f6c00-115">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="f6c00-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f6c00-116">Next steps</span></span>
* <span data-ttu-id="f6c00-117">toolearn en savoir plus sur le marquage de vos ressources Azure, consultez [vue d’ensemble du Gestionnaire de ressources Azure] [ Azure Resource Manager Overview] et [à l’aide de balises tooorganize vos ressources Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="f6c00-117">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="f6c00-118">toosee balises peuvent vous aider à gérer votre utilisation des ressources Azure, voir [comprendre votre facture Azure] [ Understanding your Azure Bill] et [obtenir votre consommation de ressources Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="f6c00-118">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
