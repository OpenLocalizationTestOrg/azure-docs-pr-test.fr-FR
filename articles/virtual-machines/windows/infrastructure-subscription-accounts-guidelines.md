---
title: Abonnement et comptes pour les machines virtuelles Windows dans Azure | Microsoft Docs
description: "Découvrez les principales instructions de conception et d’implémentation pour les abonnements et les comptes sur Azure."
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
ms.openlocfilehash: 8b54e18ed6ecef26a059a6ce742bca03a6434183
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a><span data-ttu-id="894df-103">Instructions pour les abonnements et les comptes Azure pour machines virtuelles Windows</span><span class="sxs-lookup"><span data-stu-id="894df-103">Azure subscription and accounts guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="894df-104">Cet article se concentre sur la compréhension de l’approche de la gestion des abonnements et des comptes lorsque votre environnement et votre base d’utilisateurs augmentent.</span><span class="sxs-lookup"><span data-stu-id="894df-104">This article focuses on understanding how to approach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="894df-105">Instructions d’implémentation pour les abonnements et les comptes</span><span class="sxs-lookup"><span data-stu-id="894df-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="894df-106">Décisions :</span><span class="sxs-lookup"><span data-stu-id="894df-106">Decisions:</span></span>

* <span data-ttu-id="894df-107">Quel est l’ensemble d’abonnements et de comptes dont vous avez besoin pour héberger votre charge de travail ou votre infrastructure informatique ?</span><span class="sxs-lookup"><span data-stu-id="894df-107">What set of subscriptions and accounts do you need to host your IT workload or infrastructure?</span></span>
* <span data-ttu-id="894df-108">Comment détailler la hiérarchie pour l’adapter à votre organisation ?</span><span class="sxs-lookup"><span data-stu-id="894df-108">How to break down the hierarchy to fit your organization?</span></span>

<span data-ttu-id="894df-109">Tâches :</span><span class="sxs-lookup"><span data-stu-id="894df-109">Tasks:</span></span>

* <span data-ttu-id="894df-110">Définissez la hiérarchie logique de votre organisation que vous souhaitez gérer à partir d’un niveau d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="894df-110">Define your logical organization hierarchy as you would like to manage it from a subscription level.</span></span>
* <span data-ttu-id="894df-111">Pour faire correspondre cette hiérarchie logique, définissez les comptes nécessaires et les abonnements sous chaque compte.</span><span class="sxs-lookup"><span data-stu-id="894df-111">To match this logical hierarchy, define the accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="894df-112">Créez l’ensemble d’abonnements et de comptes à l’aide de votre convention d’affectation de noms.</span><span class="sxs-lookup"><span data-stu-id="894df-112">Create the set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="894df-113">Abonnements et comptes</span><span class="sxs-lookup"><span data-stu-id="894df-113">Subscriptions and accounts</span></span>
<span data-ttu-id="894df-114">Pour utiliser Azure, vous avez besoin d’un ou de plusieurs abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="894df-114">To work with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="894df-115">Des ressources telles que des machines virtuelles ou des réseaux virtuels existent dans le contexte de ces abonnements.</span><span class="sxs-lookup"><span data-stu-id="894df-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="894df-116">Les clients d’entreprises disposent généralement d’une inscription d’entreprise, qui est la ressource principale dans la hiérarchie et est associée à un ou plusieurs comptes.</span><span class="sxs-lookup"><span data-stu-id="894df-116">Enterprise customers typically have an Enterprise Enrollment, which is the top-most resource in the hierarchy, and is associated to one or more accounts.</span></span>
* <span data-ttu-id="894df-117">Pour les particuliers et les clients sans inscription d’entreprise, la ressource principale est le compte.</span><span class="sxs-lookup"><span data-stu-id="894df-117">For consumers and customers without an Enterprise Enrollment, the top-most resource is the account.</span></span>
* <span data-ttu-id="894df-118">Les abonnements sont associés à des comptes, et chaque compte peut être associé à un ou plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="894df-118">Subscriptions are associated to accounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="894df-119">Azure enregistre les informations de facturation au niveau de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="894df-119">Azure records billing information at the subscription level.</span></span>

<span data-ttu-id="894df-120">La relation compte/abonnement étant limitée à deux niveaux de hiérarchie, il est important d'aligner la convention d'affectation de noms des comptes et des abonnements sur les besoins liés à la facturation.</span><span class="sxs-lookup"><span data-stu-id="894df-120">Due to the limit of two hierarchy levels on the Account/Subscription relationship, it is important to align the naming convention of accounts and subscriptions to the billing needs.</span></span> <span data-ttu-id="894df-121">Par exemple, si une entreprise multinationale utilise Azure, elle peut choisir d’avoir un seul compte par région et des abonnements gérés au niveau régional :</span><span class="sxs-lookup"><span data-stu-id="894df-121">For instance, if a global company uses Azure, they might choose to have one account per region, and have subscriptions managed at the region level:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="894df-122">Par exemple, vous pouvez utiliser la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="894df-122">For instance, you might use the following structure:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="894df-123">Si une région décide d’avoir plusieurs abonnements associés à un groupe spécifique, la convention d’affectation de noms doit comprendre un code pour les données supplémentaires dans le nom du compte ou de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="894df-123">If a region decides to have more than one subscription associated to a particular group, the naming convention should incorporate a way to encode the extra data on either the account or the subscription name.</span></span> <span data-ttu-id="894df-124">Cette organisation permet le transfert de données de facturation pour générer de nouveaux niveaux de hiérarchie lors de l’établissement de rapports de facturation :</span><span class="sxs-lookup"><span data-stu-id="894df-124">This organization allows massaging billing data to generate the new levels of hierarchy during billing reports:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="894df-125">L’organisation peut ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="894df-125">The organization could look like the following example:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="894df-126">Nous fournissons une facturation détaillée au moyen d’un fichier téléchargeable, pour un compte unique ou pour tous les comptes liés à un accord d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="894df-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="894df-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="894df-127">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

