---
title: "alertes d’intégrité aaaResolve endpoint protection dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** alertes ** de résoudre la Protection de point de terminaison d’intégrité."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="3e290-103">Résoudre les alertes d’intégrité Endpoint Protection dans le Centre de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="3e290-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="3e290-104">Le Centre de sécurité Azure recommande de résoudre les alertes d’intégrité Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="3e290-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="3e290-105">Centre de sécurité vous permet de toosee les machines virtuelles (VM) ont des échecs de protection de point de terminaison et de combien.</span><span class="sxs-lookup"><span data-stu-id="3e290-105">Security Center enables you toosee which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="3e290-106">Ce document présente le service de hello à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="3e290-106">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="3e290-107">Il ne s’agit pas d’un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="3e290-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-hello-recommendation"></a><span data-ttu-id="3e290-108">Implémenter la recommandation de hello</span><span class="sxs-lookup"><span data-stu-id="3e290-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="3e290-109">Bonjour **Panneau de recommandations**, sélectionnez **alertes d’intégrité de résoudre la Protection de point de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="3e290-109">In hello **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="3e290-110">![Résoudre les alertes d’intégrité Endpoint Protection][1]</span><span class="sxs-lookup"><span data-stu-id="3e290-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="3e290-111">Cela ouvre le panneau de hello **Échec de la Protection de point de terminaison** qui répertorie les ordinateurs virtuels avec des échecs et nombre hello d’échecs pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3e290-111">This opens hello blade **Endpoint Protection failure** which lists VMs with failures and hello number of failures for each VM.</span></span> <span data-ttu-id="3e290-112">Sélectionnez une machine virtuelle à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="3e290-112">Select a VM from hello list.</span></span>
   <span data-ttu-id="3e290-113">![Endpoint protection failure][2]</span><span class="sxs-lookup"><span data-stu-id="3e290-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="3e290-114">A **échecs liste** panneau s’affiche pour hello sélectionné la machine virtuelle, affiche la liste des échecs.</span><span class="sxs-lookup"><span data-stu-id="3e290-114">A **Failures List** blade opens for hello selected VM, displaying a list of failures.</span></span> <span data-ttu-id="3e290-115">Sélectionnez un échec dans toolearn de liste hello plus.</span><span class="sxs-lookup"><span data-stu-id="3e290-115">Select a failure from hello list toolearn more.</span></span> <span data-ttu-id="3e290-116">Un panneau s’ouvre avec les informations sur les échecs de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3e290-116">This opens a blade with information about hello selected failure.</span></span>
   <span data-ttu-id="3e290-117">![Liste des échecs][3]
   ![Événement d’échec][4]</span><span class="sxs-lookup"><span data-stu-id="3e290-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="3e290-118">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3e290-118">See also</span></span>
<span data-ttu-id="3e290-119">toolearn en savoir plus sur le centre de sécurité, voir hello :</span><span class="sxs-lookup"><span data-stu-id="3e290-119">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="3e290-120">[Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md)--Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="3e290-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="3e290-121">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md): découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="3e290-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="3e290-122">[Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md)--Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="3e290-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="3e290-123">[Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md)--Découvrez comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="3e290-123">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="3e290-124">[Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.</span><span class="sxs-lookup"><span data-stu-id="3e290-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="3e290-125">[Forum aux questions sur Azure Security Center](security-center-faq.md)--rechercher Forum aux questions sur l’utilisation du service de hello.</span><span class="sxs-lookup"><span data-stu-id="3e290-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="3e290-126">[Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/)--obtenir les dernières informations de sécurité Azure hello et informations.</span><span class="sxs-lookup"><span data-stu-id="3e290-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
