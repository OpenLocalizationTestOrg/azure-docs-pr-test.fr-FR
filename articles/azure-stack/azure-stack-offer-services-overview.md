---
title: services aaaOffering dans la pile de Azure | Documents Microsoft
description: "Comme un opérateur cloud, vous pouvez offrir aux utilisateurs de tooyour de services."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: 47cff8bfb202527ae4c930c7d1b9eb3998bee85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-offering-services-in-azure-stack"></a><span data-ttu-id="012bd-103">Vue d’ensemble de l’offre de services dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="012bd-103">Overview of offering services in Azure Stack</span></span>

<span data-ttu-id="012bd-104">Microsoft Azure Stack est une plateforme cloud hybride qui vous permet de fournir des services à partir de votre centre de données.</span><span class="sxs-lookup"><span data-stu-id="012bd-104">Microsoft Azure Stack is a hybrid cloud platform that lets you deliver services from your datacenter.</span></span> <span data-ttu-id="012bd-105">En tant qu’un fournisseur de services, vous pouvez offrir aux clients de services tooyour.</span><span class="sxs-lookup"><span data-stu-id="012bd-105">As a service provider, you can offer services tooyour tenants.</span></span> <span data-ttu-id="012bd-106">Dans une entreprise ou une agence gouvernementale, vous pouvez proposer des employés de tooyour services local.</span><span class="sxs-lookup"><span data-stu-id="012bd-106">Within a business or government agency, you can offer on-premises services tooyour employees.</span></span> <span data-ttu-id="012bd-107">services Hello qui vous permet de remettre incluent, mais ne sont pas limités à :</span><span class="sxs-lookup"><span data-stu-id="012bd-107">hello services that you can deliver include, but are not limited to:</span></span>

- <span data-ttu-id="012bd-108">Services Paas (Platform as a Service) tels que App Services, Mobile Apps, API Apps, API Functions, SQL, MySQL.</span><span class="sxs-lookup"><span data-stu-id="012bd-108">Platform as a Service (PaaS) services like App Services, Mobile Apps, API Apps, API Functions, SQL, MySQL.</span></span>
- <span data-ttu-id="012bd-109">Services SaaS (Software as a Service) tels que Sharepoint.</span><span class="sxs-lookup"><span data-stu-id="012bd-109">Software as a Service (SaaS) services like Sharepoint.</span></span>

<span data-ttu-id="012bd-110">Vous pouvez même combiner toointegrate de services et créer des solutions complexes pour des utilisateurs différents.</span><span class="sxs-lookup"><span data-stu-id="012bd-110">You can even combine services toointegrate and build complex solutions for different users.</span></span>

<span data-ttu-id="012bd-111">toodeliver ces utilisateurs tooyour services, vous devez créer [plans, les offres et les quotas](azure-stack-plan-offer-quota-overview.md).</span><span class="sxs-lookup"><span data-stu-id="012bd-111">toodeliver these services tooyour users, you must create [plans, offers, and quotas](azure-stack-plan-offer-quota-overview.md).</span></span> <span data-ttu-id="012bd-112">Vos utilisateurs peuvent ensuite s’abonner à tooyour offres toouse hello services.</span><span class="sxs-lookup"><span data-stu-id="012bd-112">Your users can then subscribe tooyour offers toouse hello services.</span></span>

## <a name="plan-your-service-offers"></a><span data-ttu-id="012bd-113">Planifier vos offres de service</span><span class="sxs-lookup"><span data-stu-id="012bd-113">Plan your service offers</span></span>

<span data-ttu-id="012bd-114">Lorsque vous planifiez vos offres, gardez hello points suivants en mémoire :</span><span class="sxs-lookup"><span data-stu-id="012bd-114">When you’re planning your offers, keep hello following points in mind:</span></span>

<span data-ttu-id="012bd-115">**Offres d’évaluation**: vous pouvez utiliser des offres d’évaluation tooattract nouveaux utilisateurs, puis une tooadditional services.</span><span class="sxs-lookup"><span data-stu-id="012bd-115">**Trial offers**: You can use trial offers tooattract new users, who can then upgrade tooadditional services.</span></span> <span data-ttu-id="012bd-116">toocreate une offre d’évaluation, créez un petit [plan de base](azure-stack-plan-offer-quota-overview.md#base-plan) avec un plan de module complémentaire facultatif supérieure.</span><span class="sxs-lookup"><span data-stu-id="012bd-116">toocreate a trial offer, create a small [base plan](azure-stack-plan-offer-quota-overview.md#base-plan) with an optional larger add-on plan.</span></span>

<span data-ttu-id="012bd-117">**Planification de la capacité**: vous pouvez être concerné sur les utilisateurs en saisissant de grandes quantités de ressources et les objets système hello pour tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="012bd-117">**Capacity planning**: You might be concerned about users grabbing large amounts of resources and clogging hello system for all users.</span></span> <span data-ttu-id="012bd-118">toohelp des performances, vous pouvez [configurer vos plans avec les quotas](azure-stack-plan-offer-quota-overview.md#plans) toocap utilisation.</span><span class="sxs-lookup"><span data-stu-id="012bd-118">toohelp performance, you can [configure your plans with quotas](azure-stack-plan-offer-quota-overview.md#plans) toocap usage.</span></span>

<span data-ttu-id="012bd-119">**Délégué de fournisseurs**: vous pouvez accorder d’autres offres de toocreate possibilité hello dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="012bd-119">**Delegated providers**: You can grant others hello ability toocreate offers in your environment.</span></span> <span data-ttu-id="012bd-120">Par exemple, si vous êtes un fournisseur de services, vous pouvez [déléguer](azure-stack-delegated-provider.md) cette revendeurs tooyour de capacité.</span><span class="sxs-lookup"><span data-stu-id="012bd-120">For example, if you’re a service provider, you can [delegate](azure-stack-delegated-provider.md) this ability tooyour resellers.</span></span> <span data-ttu-id="012bd-121">Ou, si vous êtes une organisation, vous pouvez déléguer tooother divisions/filiales.</span><span class="sxs-lookup"><span data-stu-id="012bd-121">Or, if you’re an organization, you can delegate tooother divisions/subsidiaries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="012bd-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="012bd-122">Next steps</span></span>
[<span data-ttu-id="012bd-123">En savoir plus sur les offres, les plans, les quotas et les abonnements</span><span class="sxs-lookup"><span data-stu-id="012bd-123">Learn more about offers, plans, quotas, and subscriptions</span></span>](azure-stack-plan-offer-quota-overview.md)

