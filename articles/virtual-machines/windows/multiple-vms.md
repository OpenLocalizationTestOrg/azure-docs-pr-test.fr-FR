---
title: aaaCreate plusieurs machines virtuelles | Documents Microsoft
description: "Options de création de plusieurs machines virtuelles sous Windows"
services: virtual-machines-windows
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dfc1d1bb-a47d-4d7c-9fd2-f12050baacab
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: guybo
ms.openlocfilehash: 37729fabd91049744f6bd94c55221f5c1c65d527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-multiple-azure-virtual-machines"></a><span data-ttu-id="c0480-103">Création de plusieurs machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="c0480-103">Create multiple Azure virtual machines</span></span>
<span data-ttu-id="c0480-104">Il existe plusieurs scénarios où vous devez toocreate un grand nombre de machines virtuelles similaires (VM).</span><span class="sxs-lookup"><span data-stu-id="c0480-104">There are many scenarios where you need toocreate a large number of similar virtual machines (VMs).</span></span> <span data-ttu-id="c0480-105">C’est le cas notamment pour le calcul hautes performances (HPC), l’analyse des données à grande échelle, les serveurs intermédiaires ou principaux évolutifs et souvent sans état (comme les serveurs Web) ainsi que les bases de données distribuées.</span><span class="sxs-lookup"><span data-stu-id="c0480-105">Some examples include high-performance computing (HPC), large-scale data analysis, scalable and often stateless middle-tier or backend servers (such as webservers), and distributed databases.</span></span>

<span data-ttu-id="c0480-106">Cet article décrit hello options disponibles toocreate plusieurs machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c0480-106">This article discusses hello available options toocreate multiple VMs in Azure.</span></span> <span data-ttu-id="c0480-107">Ces options dépassent les cas simples hello où vous créez manuellement une série d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="c0480-107">These options go beyond hello simple cases where you manually create a series of VMs.</span></span> <span data-ttu-id="c0480-108">toocreate de machines virtuelles, les processus hello que vous utilisez habituellement ne sont pas évolutifs bien si vous devez toocreate plus d’un certain nombre de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c0480-108">toocreate many VMs, hello processes that you typically use don't scale well if you need toocreate more than a handful of VMs.</span></span>

<span data-ttu-id="c0480-109">Toocreate une façon de machines virtuelles similaires est la construction de gestionnaire de ressources Azure hello toouse de *ressource boucles*.</span><span class="sxs-lookup"><span data-stu-id="c0480-109">One way toocreate many similar VMs is toouse hello Azure Resource Manager construct of *resource loops*.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="c0480-110">boucles de ressources</span><span class="sxs-lookup"><span data-stu-id="c0480-110">Resource loops</span></span>
<span data-ttu-id="c0480-111">Les boucles de ressources sont un raccourci syntaxique dans les modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c0480-111">Resource loops are a syntactical shorthand in Azure Resource Manager templates.</span></span> <span data-ttu-id="c0480-112">Elles peuvent créer un ensemble de ressources à la configuration similaire dans une boucle.</span><span class="sxs-lookup"><span data-stu-id="c0480-112">Resource loops can create a set of similarly configured resources in a loop.</span></span> <span data-ttu-id="c0480-113">Vous pouvez utiliser la ressource boucles toocreate plusieurs comptes de stockage, les interfaces réseau ou les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c0480-113">You can use resource loops toocreate multiple storage accounts, network interfaces, or virtual machines.</span></span> <span data-ttu-id="c0480-114">Pour plus d’informations sur les boucles de ressources, consultez trop[créer des machines virtuelles dans des groupes à haute disponibilité à l’aide de la ressource boucles](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/).</span><span class="sxs-lookup"><span data-stu-id="c0480-114">For more information about resource loops, refer too[Create VMs in availability sets using resource loops](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/).</span></span>

## <a name="challenges-of-scale"></a><span data-ttu-id="c0480-115">Les problèmes de la mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="c0480-115">Challenges of scale</span></span>
<span data-ttu-id="c0480-116">Bien que les boucles de ressource rendent plus facile toobuild une infrastructure cloud à grande échelle et produisent des modèles plus concis, certains défis restent.</span><span class="sxs-lookup"><span data-stu-id="c0480-116">Although resource loops make it easier toobuild out a cloud infrastructure at scale and produce more concise templates, certain challenges remain.</span></span> <span data-ttu-id="c0480-117">Par exemple, si vous utilisez une ressource boucle toocreate 100 machines virtuelles, vous devez toocorrelate contrôleurs d’interface réseau (NIC) avec des machines virtuelles correspondants et les comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="c0480-117">For example, if you use a resource loop toocreate 100 virtual machines, you need toocorrelate network interface controllers (NICs) with corresponding VMs and storage accounts.</span></span> <span data-ttu-id="c0480-118">Nombre hello d’ordinateurs virtuels étant probablement toobe différent nombre hello de comptes de stockage, vous avez trop toodeal avec des tailles de boucle de ressources différent.</span><span class="sxs-lookup"><span data-stu-id="c0480-118">Because hello number of VMs is likely toobe different from hello number of storage accounts, you'll have toodeal with different resource loop sizes, too.</span></span> <span data-ttu-id="c0480-119">Il s’agit des problèmes peut être résolus, mais augmente considérablement la complexité de hello avec montée en puissance.</span><span class="sxs-lookup"><span data-stu-id="c0480-119">These are solvable problems, but hello complexity increases significantly with scale.</span></span>

<span data-ttu-id="c0480-120">La mise en place d’une infrastructure évolutive et souple est un autre problème.</span><span class="sxs-lookup"><span data-stu-id="c0480-120">Another challenge occurs when you need an infrastructure that scales elastically.</span></span> <span data-ttu-id="c0480-121">Vous pourriez par exemple, une infrastructure de mise à l’échelle automatiquement augmente ou diminue le nombre hello d’ordinateurs virtuels dans tooworkload de réponse.</span><span class="sxs-lookup"><span data-stu-id="c0480-121">For example, you might want an autoscale infrastructure that automatically increases or decreases hello number of VMs in response tooworkload.</span></span> <span data-ttu-id="c0480-122">Machines virtuelles ne fournissent pas une toovary mécanisme intégré en nombre (montée en puissance parallèle et échelle).</span><span class="sxs-lookup"><span data-stu-id="c0480-122">VMs don't provide an integrated mechanism toovary in number (scale out and scale in).</span></span> <span data-ttu-id="c0480-123">Si vous mettez à l’échelle en supprimant les machines virtuelles, il est difficile tooguarantee haute disponibilité en faisant en sorte que les machines virtuelles sont équilibrés entre les domaines de mise à jour et d’erreur.</span><span class="sxs-lookup"><span data-stu-id="c0480-123">If you scale in by removing VMs, it's difficult tooguarantee high availability by making sure that VMs are balanced across update and fault domains.</span></span>

<span data-ttu-id="c0480-124">Enfin, lorsque vous utilisez une boucle de ressource, plusieurs ressources de toocreate appels accédez infrastructure sous-jacente de toohello.</span><span class="sxs-lookup"><span data-stu-id="c0480-124">Finally, when you use a resource loop, multiple calls toocreate resources go toohello underlying fabric.</span></span> <span data-ttu-id="c0480-125">Lorsque plusieurs appels de créent des ressources similaires, Azure a un tooimprove opportunité implicite lors de cette conception et optimiser les performances et la fiabilité du déploiement.</span><span class="sxs-lookup"><span data-stu-id="c0480-125">When multiple calls create similar resources, Azure has an implicit opportunity tooimprove upon this design and optimize deployment reliability and performance.</span></span> <span data-ttu-id="c0480-126">C’est ici qu’interviennent les *jeux de mise à l’échelle de machine virtuelle* .</span><span class="sxs-lookup"><span data-stu-id="c0480-126">This is where *virtual machine scale sets* come in.</span></span>

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="c0480-127">Groupes identiques de machines virtuelles </span><span class="sxs-lookup"><span data-stu-id="c0480-127">Virtual machine scale sets</span></span>
<span data-ttu-id="c0480-128">Machines virtuelles identiques sont une toodeploy de ressources de calcul Azure et de gérer un ensemble de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="c0480-128">Virtual machine scale sets are an Azure Compute resource toodeploy and manage a set of identical VMs.</span></span> <span data-ttu-id="c0480-129">Avec toutes les machines virtuelles configurées hello même, jeux de mise à l’échelle de machine virtuelle est tooscale facile dans et montée en puissance parallèle. Vous modifiez simplement nombre hello d’ordinateurs virtuels dans le jeu de hello.</span><span class="sxs-lookup"><span data-stu-id="c0480-129">With all VMs configured hello same, VM scale sets are easy tooscale in and scale out. You simply change hello number of VMs in hello set.</span></span> <span data-ttu-id="c0480-130">Vous pouvez également configurer des ordinateurs virtuels échelle jeux tooautoscale basé sur les demandes de charge de travail hello hello.</span><span class="sxs-lookup"><span data-stu-id="c0480-130">You can also configure VM scale sets tooautoscale based on hello demands of hello workload.</span></span>

<span data-ttu-id="c0480-131">Pour les applications qui ont besoin de ressources de calcul tooscale et de mise à l’échelle les opérations sont implicitement équilibrées entre domaines d’erreur et la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="c0480-131">For applications that need tooscale Compute resources out and in, scale operations are implicitly balanced across fault and update domains.</span></span>

<span data-ttu-id="c0480-132">Au lieu d’effectuer la mise en corrélation de plusieurs ressources telles que des cartes réseau et des machines virtuelles, un jeu de mise à l’échelle comprend un réseau, un stockage, une machine virtuelle et des propriétés d’extension que vous pouvez configurer de manière centralisée.</span><span class="sxs-lookup"><span data-stu-id="c0480-132">Instead of correlating multiple resources such as NICs and VMs, a VM scale set has network, storage, virtual machine, and extension properties that you can configure centrally.</span></span>

<span data-ttu-id="c0480-133">Pour une échelle de tooVM introduction jeux, consultez toohello [échelle de machines virtuelles définit la page produit](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="c0480-133">For an introduction tooVM scale sets, refer toohello [Virtual machine scale sets product page](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span> <span data-ttu-id="c0480-134">Pour plus d’informations, consultez toohello [mise à l’échelle de machines virtuelles définit documentation](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="c0480-134">For more detailed information, go toohello [Virtual machines scale sets documentation](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/).</span></span>
