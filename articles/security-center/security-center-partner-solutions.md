---
title: "solutions de partenaire aaaManaging dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous guide tout au long de comment Azure Security Center vous permet de vous moniteur dans un état d’intégrité hello aperçu de vos solutions de partenaire intégré à votre abonnement Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="2ece7-103">Surveillance des solutions de partenaire avec le Centre de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="2ece7-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="2ece7-104">Ce document vous guide tout au long de la toomonitor hello état d’intégrité de vos solutions de partenaire dans le centre de sécurité Azure.</span><span class="sxs-lookup"><span data-stu-id="2ece7-104">This document walks you through how toomonitor hello health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="2ece7-105">Ce document présente le service de hello à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="2ece7-105">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="2ece7-106">Ce document n'est pas un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="2ece7-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="2ece7-107">Surveillance des solutions de partenaire</span><span class="sxs-lookup"><span data-stu-id="2ece7-107">Monitoring partner solutions</span></span>
<span data-ttu-id="2ece7-108">Hello **solutions de partenaire** vignette sur hello **centre de sécurité** panneau vous permet de contrôler dans un état d’intégrité hello aperçu de vos solutions de partenaire sont intégrées à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2ece7-108">hello **Partner solutions** tile on hello **Security Center** blade lets you monitor at a glance hello health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![Mosaïque Solutions de partenaire][1]

<span data-ttu-id="2ece7-110">Hello **solutions de partenaire** vignette affiche le nombre hello de solutions de partenaire intégré à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="2ece7-110">hello **Partner solutions** tile displays hello number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="2ece7-111">S’il n’y a aucune solution intégrée, vignette de hello affiche le nombre de hello zéro.</span><span class="sxs-lookup"><span data-stu-id="2ece7-111">If there are no solutions integrated, hello tile displays hello number zero.</span></span>

<span data-ttu-id="2ece7-112">contrôle d’intégrité de tooview hello de vos solutions de partenaire :</span><span class="sxs-lookup"><span data-stu-id="2ece7-112">tooview hello health of your partner solutions:</span></span>

1. <span data-ttu-id="2ece7-113">Sélectionnez hello **solutions de partenaire** vignette.</span><span class="sxs-lookup"><span data-stu-id="2ece7-113">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="2ece7-114">Hello **solutions de partenaire** s’ouvre le panneau affiche la liste de vos solutions de partenaire connecté tooSecurity Center.</span><span class="sxs-lookup"><span data-stu-id="2ece7-114">hello **Partner solutions** blade opens displaying a list of your partner solutions connected tooSecurity Center.</span></span>

   ![Solutions de partenaires][3]

   <span data-ttu-id="2ece7-116">état Hello d’une solution partenaire peut être :</span><span class="sxs-lookup"><span data-stu-id="2ece7-116">hello status of a partner solution can be:</span></span>

   * <span data-ttu-id="2ece7-117">Protégé (vert) : aucun problème d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="2ece7-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="2ece7-118">Défectueux (rouge) : problème d’intégrité nécessitant une action immédiate.</span><span class="sxs-lookup"><span data-stu-id="2ece7-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="2ece7-119">Arrêté (orange - création de rapports) des solutions de hello se sont arrêté reporting son intégrité.</span><span class="sxs-lookup"><span data-stu-id="2ece7-119">Stopped reporting (orange) - hello solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="2ece7-120">État de protection inconnu (orange) - intégrité hello de solution de hello est inconnu pour l’instant en raison des processus tooa échoué de l’ajout d’une solution existante de nouvelles ressources toohello.</span><span class="sxs-lookup"><span data-stu-id="2ece7-120">Unknown protection status (orange) - hello health of hello solution is unknown at this time due tooa failed process of adding a new resource toohello existing solution.</span></span>
   * <span data-ttu-id="2ece7-121">Pas signalé (gris) - solution de hello n’a pas signalé quoi que ce soit encore, le statut de la solution est peut-être pas signalée si elle a récemment été connecté et est toujours déploiement.</span><span class="sxs-lookup"><span data-stu-id="2ece7-121">Not reported (gray) - hello solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="2ece7-122">Sélectionnez une solution de partenaire.</span><span class="sxs-lookup"><span data-stu-id="2ece7-122">Select a partner solution.</span></span> <span data-ttu-id="2ece7-123">Dans cet exemple, vous permet de sélectionner hello **Qualys** solution.</span><span class="sxs-lookup"><span data-stu-id="2ece7-123">In this example, lets select hello **Qualys** solution.</span></span>  <span data-ttu-id="2ece7-124">Un panneau s’ouvre pour afficher l’état de hello des solutions de partenaire hello et la solution hello associés aux ressources.</span><span class="sxs-lookup"><span data-stu-id="2ece7-124">A blade opens showing you hello status of hello partner solution and hello solution's associated resources.</span></span> <span data-ttu-id="2ece7-125">Sélectionnez **console de la Solution** expérience de gestion des partenaires tooopen hello pour cette solution.</span><span class="sxs-lookup"><span data-stu-id="2ece7-125">Select **Solution console** tooopen hello partner management experience for this solution.</span></span>

   ![Détail de la solution partenaire][4]
3. <span data-ttu-id="2ece7-127">Revenir en arrière toohello **Qualys** panneau et sélectionnez **lien VM**.</span><span class="sxs-lookup"><span data-stu-id="2ece7-127">Go back toohello **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="2ece7-128">Hello **lien Applications** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="2ece7-128">hello **Link Applications** blade opens.</span></span> <span data-ttu-id="2ece7-129">Ici, vous pouvez connecter solutions de partenaire de ressources toohello.</span><span class="sxs-lookup"><span data-stu-id="2ece7-129">Here you can connect resources toohello partner solution.</span></span>

   ![Lien ressources toopartner solution][5]

## <a name="next-steps"></a><span data-ttu-id="2ece7-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2ece7-131">Next steps</span></span>
<span data-ttu-id="2ece7-132">Dans ce document, vous ont été introduite toohello **Solutions de partenaire** vignette dans le centre de sécurité.</span><span class="sxs-lookup"><span data-stu-id="2ece7-132">In this document, you were introduced toohello **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="2ece7-133">toolearn en savoir plus sur le centre de sécurité, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="2ece7-133">toolearn more about Security Center, see hello following articles:</span></span>

* <span data-ttu-id="2ece7-134">[Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) : Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="2ece7-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="2ece7-135">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="2ece7-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="2ece7-136">[Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) — Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="2ece7-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="2ece7-137">[Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) : en savoir comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="2ece7-137">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="2ece7-138">[Forum aux questions sur Azure Security Center](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche.</span><span class="sxs-lookup"><span data-stu-id="2ece7-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="2ece7-139">[Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenir les dernières informations de sécurité Azure hello et informations.</span><span class="sxs-lookup"><span data-stu-id="2ece7-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
