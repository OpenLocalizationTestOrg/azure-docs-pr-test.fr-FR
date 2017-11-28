---
title: Offre de services dans Azure Stack | Microsoft Docs
description: "En tant qu’opérateur cloud, vous pouvez proposer des services à vos utilisateurs."
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
ms.openlocfilehash: 785acbeba7eebea5a0414ac8bb9942410bf4252e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="overview-of-offering-services-in-azure-stack"></a><span data-ttu-id="a0c5f-103">Vue d’ensemble de l’offre de services dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a0c5f-103">Overview of offering services in Azure Stack</span></span>

<span data-ttu-id="a0c5f-104">Microsoft Azure Stack est une plateforme cloud hybride qui vous permet de fournir des services à partir de votre centre de données.</span><span class="sxs-lookup"><span data-stu-id="a0c5f-104">Microsoft Azure Stack is a hybrid cloud platform that lets you deliver services from your datacenter.</span></span> <span data-ttu-id="a0c5f-105">En tant que fournisseur de services, vous pouvez proposer des services à vos locataires.</span><span class="sxs-lookup"><span data-stu-id="a0c5f-105">As a service provider, you can offer services to your tenants.</span></span> <span data-ttu-id="a0c5f-106">Au sein d’une entreprise ou d’une agence gouvernementale, vous pouvez proposer des services locaux à vos employés.</span><span class="sxs-lookup"><span data-stu-id="a0c5f-106">Within a business or government agency, you can offer on-premises services to your employees.</span></span> <span data-ttu-id="a0c5f-107">Vous pouvez proposer entre autres les services suivants :</span><span class="sxs-lookup"><span data-stu-id="a0c5f-107">The services that you can deliver include, but are not limited to:</span></span>

- <span data-ttu-id="a0c5f-108">Services Paas (Platform as a Service) tels que App Services, Mobile Apps, API Apps, API Functions, SQL, MySQL.</span><span class="sxs-lookup"><span data-stu-id="a0c5f-108">Platform as a Service (PaaS) services like App Services, Mobile Apps, API Apps, API Functions, SQL, MySQL.</span></span>
- <span data-ttu-id="a0c5f-109">Services SaaS (Software as a Service) tels que Sharepoint.</span><span class="sxs-lookup"><span data-stu-id="a0c5f-109">Software as a Service (SaaS) services like Sharepoint.</span></span>

<span data-ttu-id="a0c5f-110">Vous pouvez même combiner des services pour intégrer et créer des solutions complexes pour différents utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a0c5f-110">You can even combine services to integrate and build complex solutions for different users.</span></span>

<span data-ttu-id="a0c5f-111">Pour fournir ces services à vos utilisateurs, vous devez créer [des plans, des offres et des quotas](azure-stack-plan-offer-quota-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0c5f-111">To deliver these services to your users, you must create [plans, offers, and quotas](azure-stack-plan-offer-quota-overview.md).</span></span> <span data-ttu-id="a0c5f-112">Vos utilisateurs peuvent ensuite s’abonner à vos offres pour utiliser les services.</span><span class="sxs-lookup"><span data-stu-id="a0c5f-112">Your users can then subscribe to your offers to use the services.</span></span>

## <a name="plan-your-service-offers"></a><span data-ttu-id="a0c5f-113">Planifier vos offres de service</span><span class="sxs-lookup"><span data-stu-id="a0c5f-113">Plan your service offers</span></span>

<span data-ttu-id="a0c5f-114">Quand vous planifiez vos offres, gardez à l’esprit les points suivants :</span><span class="sxs-lookup"><span data-stu-id="a0c5f-114">When you’re planning your offers, keep the following points in mind:</span></span>

<span data-ttu-id="a0c5f-115">**Offres d’évaluation** : vous pouvez utiliser des offres d’évaluation pour attirer de nouveaux utilisateurs, qui peuvent ensuite effectuer une mise à niveau pour obtenir des services supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a0c5f-115">**Trial offers**: You can use trial offers to attract new users, who can then upgrade to additional services.</span></span> <span data-ttu-id="a0c5f-116">Pour créer une offre d’évaluation, créez un petit [plan de base](azure-stack-plan-offer-quota-overview.md#base-plan) avec un plan complémentaire facultatif plus important.</span><span class="sxs-lookup"><span data-stu-id="a0c5f-116">To create a trial offer, create a small [base plan](azure-stack-plan-offer-quota-overview.md#base-plan) with an optional larger add-on plan.</span></span>

<span data-ttu-id="a0c5f-117">**Planification de la capacité** : peut-être craignez-vous que des utilisateurs s’accaparent de grandes quantités de ressources et encombrent le système pour tous les autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a0c5f-117">**Capacity planning**: You might be concerned about users grabbing large amounts of resources and clogging the system for all users.</span></span> <span data-ttu-id="a0c5f-118">Pour améliorer les performances, vous pouvez [configurer vos plans avec des quotas](azure-stack-plan-offer-quota-overview.md#plans) afin de limiter l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="a0c5f-118">To help performance, you can [configure your plans with quotas](azure-stack-plan-offer-quota-overview.md#plans) to cap usage.</span></span>

<span data-ttu-id="a0c5f-119">**Fournisseurs délégués** : vous pouvez accorder à d’autres personnes la capacité à créer des offres dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="a0c5f-119">**Delegated providers**: You can grant others the ability to create offers in your environment.</span></span> <span data-ttu-id="a0c5f-120">Par exemple, si vous êtes fournisseur de services, vous pouvez [déléguer](azure-stack-delegated-provider.md) cette capacité à vos revendeurs.</span><span class="sxs-lookup"><span data-stu-id="a0c5f-120">For example, if you’re a service provider, you can [delegate](azure-stack-delegated-provider.md) this ability to your resellers.</span></span> <span data-ttu-id="a0c5f-121">Si vous êtes une organisation, vous pouvez déléguer à d’autres divisions/filiales.</span><span class="sxs-lookup"><span data-stu-id="a0c5f-121">Or, if you’re an organization, you can delegate to other divisions/subsidiaries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0c5f-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0c5f-122">Next steps</span></span>
[<span data-ttu-id="a0c5f-123">En savoir plus sur les offres, les plans, les quotas et les abonnements</span><span class="sxs-lookup"><span data-stu-id="a0c5f-123">Learn more about offers, plans, quotas, and subscriptions</span></span>](azure-stack-plan-offer-quota-overview.md)

