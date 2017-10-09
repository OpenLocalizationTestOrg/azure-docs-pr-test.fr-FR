---
title: aaaSubscription et les comptes pour les machines virtuelles Windows dans Azure | Documents Microsoft
description: "Découvrez hello clé conception et implémentation des recommandations pour les abonnements et les comptes dans Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 761fa847-78b0-4078-a33a-d95d198d1029
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f9dc712af559b04490be1dc721a9b9f7fe9ed88f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a><span data-ttu-id="faabe-103">Instructions pour les abonnements et les comptes Azure pour machines virtuelles Windows</span><span class="sxs-lookup"><span data-stu-id="faabe-103">Azure subscription and accounts guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="faabe-104">Cet article se concentre sur comment tooapproach abonnement et gestion des comptes en tant que votre environnement et de la base d’utilisateurs augmente.</span><span class="sxs-lookup"><span data-stu-id="faabe-104">This article focuses on understanding how tooapproach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="faabe-105">Instructions d’implémentation pour les abonnements et les comptes</span><span class="sxs-lookup"><span data-stu-id="faabe-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="faabe-106">Décisions :</span><span class="sxs-lookup"><span data-stu-id="faabe-106">Decisions:</span></span>

* <span data-ttu-id="faabe-107">Le jeu de comptes et les abonnements devez-vous toohost votre charge de travail informatique ou d’infrastructure ?</span><span class="sxs-lookup"><span data-stu-id="faabe-107">What set of subscriptions and accounts do you need toohost your IT workload or infrastructure?</span></span>
* <span data-ttu-id="faabe-108">Comment toobreak vers le bas hello hiérarchie toofit votre organisation ?</span><span class="sxs-lookup"><span data-stu-id="faabe-108">How toobreak down hello hierarchy toofit your organization?</span></span>

<span data-ttu-id="faabe-109">Tâches :</span><span class="sxs-lookup"><span data-stu-id="faabe-109">Tasks:</span></span>

* <span data-ttu-id="faabe-110">Définir la hiérarchie logique que vous aimeriez toomanage à partir d’un niveau d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="faabe-110">Define your logical organization hierarchy as you would like toomanage it from a subscription level.</span></span>
* <span data-ttu-id="faabe-111">toomatch cette hiérarchie logique, les comptes hello requis et des abonnements sous chaque compte.</span><span class="sxs-lookup"><span data-stu-id="faabe-111">toomatch this logical hierarchy, define hello accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="faabe-112">Créer un jeu hello des abonnements et des comptes à l’aide de votre convention d’affectation de noms.</span><span class="sxs-lookup"><span data-stu-id="faabe-112">Create hello set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="faabe-113">Abonnements et comptes</span><span class="sxs-lookup"><span data-stu-id="faabe-113">Subscriptions and accounts</span></span>
<span data-ttu-id="faabe-114">toowork avec Azure, vous devez un ou plusieurs abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="faabe-114">toowork with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="faabe-115">Des ressources telles que des machines virtuelles ou des réseaux virtuels existent dans le contexte de ces abonnements.</span><span class="sxs-lookup"><span data-stu-id="faabe-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="faabe-116">Les clients d’entreprise ont généralement une inscription d’entreprise, hello des ressources de plus haut dans la hiérarchie de hello et tooone associée ou autres comptes.</span><span class="sxs-lookup"><span data-stu-id="faabe-116">Enterprise customers typically have an Enterprise Enrollment, which is hello top-most resource in hello hierarchy, and is associated tooone or more accounts.</span></span>
* <span data-ttu-id="faabe-117">Pour les particuliers et les clients sans une inscription de l’entreprise, la ressource de plus de hello est compte de hello.</span><span class="sxs-lookup"><span data-stu-id="faabe-117">For consumers and customers without an Enterprise Enrollment, hello top-most resource is hello account.</span></span>
* <span data-ttu-id="faabe-118">Les abonnements sont associés tooaccounts, et il peut y avoir un ou plusieurs abonnements par compte.</span><span class="sxs-lookup"><span data-stu-id="faabe-118">Subscriptions are associated tooaccounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="faabe-119">Azure enregistre les informations au niveau d’abonnement hello de facturation.</span><span class="sxs-lookup"><span data-stu-id="faabe-119">Azure records billing information at hello subscription level.</span></span>

<span data-ttu-id="faabe-120">En raison de la limite de toohello de niveaux de hiérarchie deux sur la relation d’abonnement de compte/hello, il est important tooalign hello conventions d’affectation des comptes et des abonnements toohello besoins de facturation.</span><span class="sxs-lookup"><span data-stu-id="faabe-120">Due toohello limit of two hierarchy levels on hello Account/Subscription relationship, it is important tooalign hello naming convention of accounts and subscriptions toohello billing needs.</span></span> <span data-ttu-id="faabe-121">Par exemple, si une entreprise internationale utilise Azure, ils peuvent choisir le compte de toohave un par région et ont des abonnements gérés au niveau de la région de hello :</span><span class="sxs-lookup"><span data-stu-id="faabe-121">For instance, if a global company uses Azure, they might choose toohave one account per region, and have subscriptions managed at hello region level:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="faabe-122">Par exemple, vous pouvez utiliser hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="faabe-122">For instance, you might use hello following structure:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="faabe-123">Si une région décide toohave plus de groupe tooa associé à un seul abonnement, convention d’affectation de noms de hello doit incorporer un tooencode moyen hello des données supplémentaires sur le compte de hello ou nom de l’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="faabe-123">If a region decides toohave more than one subscription associated tooa particular group, hello naming convention should incorporate a way tooencode hello extra data on either hello account or hello subscription name.</span></span> <span data-ttu-id="faabe-124">Cette organisation permet masser facturation données toogenerate hello nouveaux niveaux de hiérarchie au cours de la facturation de rapports :</span><span class="sxs-lookup"><span data-stu-id="faabe-124">This organization allows massaging billing data toogenerate hello new levels of hierarchy during billing reports:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="faabe-125">organisation de Hello pourrait ressembler à hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="faabe-125">hello organization could look like hello following example:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="faabe-126">Nous fournissons une facturation détaillée au moyen d’un fichier téléchargeable, pour un compte unique ou pour tous les comptes liés à un accord d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="faabe-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="faabe-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="faabe-127">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

