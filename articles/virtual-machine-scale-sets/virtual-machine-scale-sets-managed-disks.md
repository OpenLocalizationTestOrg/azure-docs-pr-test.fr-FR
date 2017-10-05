---
title: "Utiliser des disques gérés avec des groupes de machines virtuelles identiques Azure | Microsoft Docs"
description: "Découvrez pourquoi et comment utiliser des disques gérés avec des groupes de machines virtuelles identiques"
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
ms.openlocfilehash: 3ab1d432a2f90db57b99f0e7d419d85e2958c308
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="7e329-103">Groupes de machines virtuelles identiques Azure et disques gérés</span><span class="sxs-lookup"><span data-stu-id="7e329-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="7e329-104">Les [groupes de machines virtuelles identiques](/azure/virtual-machine-scale-sets/) Azure prennent en charge les machines virtuelles avec disques gérés.</span><span class="sxs-lookup"><span data-stu-id="7e329-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) supports virtual machines with managed disks.</span></span> <span data-ttu-id="7e329-105">Les disques gérés avec groupes identiques présentent plusieurs avantages, notamment :</span><span class="sxs-lookup"><span data-stu-id="7e329-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="7e329-106">Vous n’avez plus besoin de créer au préalable et de gérer des comptes de stockage pour stocker les disques du système d’exploitation pour les machines virtuelles de groupes identiques.</span><span class="sxs-lookup"><span data-stu-id="7e329-106">You no longer need to pre-create and manage storage accounts to store the OS disks for the scale set VMs.</span></span>

* <span data-ttu-id="7e329-107">Vous pouvez attacher des disques de données gérés au groupe identique.</span><span class="sxs-lookup"><span data-stu-id="7e329-107">You can attach managed data disks to the scale set.</span></span>

* <span data-ttu-id="7e329-108">Avec un disque géré, un groupe identique peut atteindre une capacité de 1 000 machines virtuelles à partir d’une image de plateforme ou de 100 machines virtuelles à partir d’une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="7e329-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="7e329-109">Prise en main</span><span class="sxs-lookup"><span data-stu-id="7e329-109">Get started</span></span>

<span data-ttu-id="7e329-110">Un moyen simple de se familiariser avec les groupes de disques gérés identiques consiste à en déployer un à partir du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7e329-110">A simple way to get started with managed disk scale sets is to deploy one from the Azure portal.</span></span> <span data-ttu-id="7e329-111">Pour plus d’informations, consultez [cet article](./virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="7e329-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="7e329-112">Il est aussi possible, pour commencer, d’utiliser [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) afin de déployer un groupe identique.</span><span class="sxs-lookup"><span data-stu-id="7e329-112">Another simple way to get started is to use [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) to deploy a scale set.</span></span> <span data-ttu-id="7e329-113">L’exemple suivant montre comment créer un groupe identique sous Ubuntu avec 10 machines virtuelles, comprenant chacune un disque de données de 50 Go et de 100 Go :</span><span class="sxs-lookup"><span data-stu-id="7e329-113">The following example shows how to create an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="7e329-114">Vous pouvez également consulter le [Référentiel GitHub de modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates), dans les dossiers qui contiennent `vmss`, pour voir des exemples prédéfinis de modèles qui déploient des groupes identiques.</span><span class="sxs-lookup"><span data-stu-id="7e329-114">Alternatively, you could look in the [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` to see pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="7e329-115">Pour savoir quels modèles utilisent déjà des disques gérés, vous pouvez consulter [cette liste](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span><span class="sxs-lookup"><span data-stu-id="7e329-115">To tell which templates are already using managed disks, you can refer to [this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e329-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7e329-116">Next steps</span></span>

<span data-ttu-id="7e329-117">Pour plus d’informations sur les disques gérés en général, consultez [cet article](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7e329-117">For more information on managed disks in general, see [this article](../virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="7e329-118">Pour savoir comment convertir un modèle Resource Manager afin d’approvisionner des groupes identiques avec disques gérés, consultez [cet article](./virtual-machine-scale-sets-convert-template-to-md.md).</span><span class="sxs-lookup"><span data-stu-id="7e329-118">To see how to convert a Resource Manager template to provision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="7e329-119">Les modifications apportées aux modèles Resource Manager s’appliquent également à l’API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="7e329-119">The same modifications to the Resource Manager templates apply to the Azure REST API as well.</span></span>

<span data-ttu-id="7e329-120">Pour en savoir plus sur l’utilisation de disques de données gérés avec des groupes identiques, consultez [cet article](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="7e329-120">To learn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="7e329-121">Pour commencer à travailler avec des groupes identiques, consultez [cet article](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="7e329-121">To begin working with large scale sets, refer to [this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


