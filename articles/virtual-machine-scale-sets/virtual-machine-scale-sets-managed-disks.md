---
title: "aaaUsing gérés disques avec Azure machines virtuelles identiques | Documents Microsoft"
description: "Découvrez pourquoi et comment toouse gérés disques avec les machines virtuelles identiques"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="a1586-103">Groupes de machines virtuelles identiques Azure et disques gérés</span><span class="sxs-lookup"><span data-stu-id="a1586-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="a1586-104">Les [groupes de machines virtuelles identiques](/azure/virtual-machine-scale-sets/) Azure prennent en charge les machines virtuelles avec disques gérés.</span><span class="sxs-lookup"><span data-stu-id="a1586-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) supports virtual machines with managed disks.</span></span> <span data-ttu-id="a1586-105">Les disques gérés avec groupes identiques présentent plusieurs avantages, notamment :</span><span class="sxs-lookup"><span data-stu-id="a1586-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="a1586-106">Vous n’avez plus besoin toopre-créer et gérer des disques de stockage comptes toostore hello du système d’exploitation pour l’ensemble d’échelle de hello de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="a1586-106">You no longer need toopre-create and manage storage accounts toostore hello OS disks for hello scale set VMs.</span></span>

* <span data-ttu-id="a1586-107">Vous pouvez joindre des données managées disques toohello identiques.</span><span class="sxs-lookup"><span data-stu-id="a1586-107">You can attach managed data disks toohello scale set.</span></span>

* <span data-ttu-id="a1586-108">Avec un disque géré, un groupe identique peut atteindre une capacité de 1 000 machines virtuelles à partir d’une image de plateforme ou de 100 machines virtuelles à partir d’une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="a1586-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="a1586-109">Prise en main</span><span class="sxs-lookup"><span data-stu-id="a1586-109">Get started</span></span>

<span data-ttu-id="a1586-110">Un moyen simple tooget main identiques de disque géré est un toodeploy de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a1586-110">A simple way tooget started with managed disk scale sets is toodeploy one from hello Azure portal.</span></span> <span data-ttu-id="a1586-111">Pour plus d’informations, consultez [cet article](./virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="a1586-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="a1586-112">Une autre façon simple tooget démarré est toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy une échelle définie.</span><span class="sxs-lookup"><span data-stu-id="a1586-112">Another simple way tooget started is toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy a scale set.</span></span> <span data-ttu-id="a1586-113">Hello suivant montre comment toocreate un Ubuntu en fonction de l’échelle avec des machines 10 virtuelles, chacun avec un disque de 50 Go et de 100 Go de données :</span><span class="sxs-lookup"><span data-stu-id="a1586-113">hello following example shows how toocreate an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="a1586-114">Vous pouvez également consulter hello [référentiel GitHub de modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates) pour les dossiers qui contiennent des `vmss` toosee prégénérées des exemples de modèles de déploiement identiques.</span><span class="sxs-lookup"><span data-stu-id="a1586-114">Alternatively, you could look in hello [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` toosee pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="a1586-115">tootell les modèles sont déjà à l’aide de disques gérés, vous pouvez faire référence trop[cette liste](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span><span class="sxs-lookup"><span data-stu-id="a1586-115">tootell which templates are already using managed disks, you can refer too[this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1586-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a1586-116">Next steps</span></span>

<span data-ttu-id="a1586-117">Pour plus d’informations sur les disques gérés en général, consultez [cet article](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1586-117">For more information on managed disks in general, see [this article](../virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="a1586-118">reportez-vous à la méthode de tooconvert une échelle de tooprovision de modèle de gestionnaire de ressources définit avec gestion des disques, toosee [cet article](./virtual-machine-scale-sets-convert-template-to-md.md).</span><span class="sxs-lookup"><span data-stu-id="a1586-118">toosee how tooconvert a Resource Manager template tooprovision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="a1586-119">Hello mêmes modèles de gestionnaire de ressources toohello modifications s’appliquent toohello API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="a1586-119">hello same modifications toohello Resource Manager templates apply toohello Azure REST API as well.</span></span>

<span data-ttu-id="a1586-120">toolearn savoir plus sur l’utilisation de disques de données managées avec identiques, consultez [cet article](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="a1586-120">toolearn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="a1586-121">toobegin les jeux à grande échelle, consultez trop[cet article](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="a1586-121">toobegin working with large scale sets, refer too[this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


