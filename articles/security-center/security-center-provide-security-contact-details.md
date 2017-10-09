---
title: "aaaProvide les détails de contact de sécurité dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooprovide sécurité coordonnées dans le centre de sécurité Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="e9932-103">Fournir les détails du contact de sécurité dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="e9932-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="e9932-104">Azure Security Center vous recommande de fournir les détails du contact de sécurité pour votre abonnement Azure, si vous ne l’avez pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="e9932-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="e9932-105">Ces informations seront être utilisées par Microsoft toocontact si hello MSRC Microsoft Security Response Center () détecte que votre client a accédé aux données par un tiers illégal ou non autorisé.</span><span class="sxs-lookup"><span data-stu-id="e9932-105">This information will be used by Microsoft toocontact you if hello Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="e9932-106">MSRC réalise une surveillance de hello réseau Azure et l’infrastructure sélectionnez sécurité et reçoit des réclamations intelligence et abus de menace de tiers.</span><span class="sxs-lookup"><span data-stu-id="e9932-106">MSRC performs select security monitoring of hello Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="e9932-107">Une notification par courrier électronique est envoyée sur hello première quotidienne d’une alerte et uniquement pour les alertes de gravité élevée.</span><span class="sxs-lookup"><span data-stu-id="e9932-107">An email notification is sent on hello first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="e9932-108">Les préférences de courrier électronique peuvent uniquement être configurées pour les stratégies d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="e9932-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="e9932-109">Les groupes de ressources d’un abonnement hériteront de ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="e9932-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="e9932-110">Ce document présente le service de hello à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="e9932-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="e9932-111">Il ne s’agit pas d’un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="e9932-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="e9932-112">Implémenter la recommandation de hello</span><span class="sxs-lookup"><span data-stu-id="e9932-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="e9932-113">Bonjour **recommandations** panneau, sélectionnez **fournissent des détails de contact de sécurité**.</span><span class="sxs-lookup"><span data-stu-id="e9932-113">In hello **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="e9932-114">![Fournir le contact de sécurité][1]</span><span class="sxs-lookup"><span data-stu-id="e9932-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="e9932-115">Cela ouvre le panneau de hello **fournissent des détails de contact de sécurité**.</span><span class="sxs-lookup"><span data-stu-id="e9932-115">This opens hello blade **Provide security contact details**.</span></span> <span data-ttu-id="e9932-116">Sélectionnez les informations de contact tooprovide abonnement Azure hello sur.</span><span class="sxs-lookup"><span data-stu-id="e9932-116">Select hello Azure subscription tooprovide contact information on.</span></span>
   <span data-ttu-id="e9932-117">![Fournir des informations de contact de sécurité][2]</span><span class="sxs-lookup"><span data-stu-id="e9932-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="e9932-118">Un second panneau **Fournissez les détails du contact de sécurité** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="e9932-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="e9932-119">Entrez l’adresse de messagerie du contact de sécurité hello ou séparés par des virgules des adresses.</span><span class="sxs-lookup"><span data-stu-id="e9932-119">Enter hello security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="e9932-120">Il n’est pas un toohello limiter le nombre d’adresses de messagerie que vous pouvez entrer.</span><span class="sxs-lookup"><span data-stu-id="e9932-120">There is not a limit toohello number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="e9932-121">Entrez le numéro de téléphone international du contact de sécurité.</span><span class="sxs-lookup"><span data-stu-id="e9932-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="e9932-122">des messages électroniques tooreceive sur les alertes de gravité élevée, activez hello option **m’envoyer des e-mails sur les alertes**.</span><span class="sxs-lookup"><span data-stu-id="e9932-122">tooreceive emails about high severity alerts, turn on hello option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="e9932-123">Bonjour futures, vous aurez propriétaires toosubscription des notifications de messagerie hello option toosend.</span><span class="sxs-lookup"><span data-stu-id="e9932-123">In hello future, you will have hello option toosend email notifications toosubscription owners.</span></span> <span data-ttu-id="e9932-124">Cette option est actuellement grisée.</span><span class="sxs-lookup"><span data-stu-id="e9932-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="e9932-125">Sélectionnez **OK** sécurité de hello tooapply contactez tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="e9932-125">Select **OK** tooapply hello security contact information tooyour subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="e9932-126">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e9932-126">See also</span></span>
<span data-ttu-id="e9932-127">toolearn en savoir plus sur le centre de sécurité, voir hello :</span><span class="sxs-lookup"><span data-stu-id="e9932-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="e9932-128">[Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="e9932-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="e9932-129">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="e9932-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="e9932-130">[Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="e9932-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="e9932-131">[Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="e9932-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="e9932-132">[Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.</span><span class="sxs-lookup"><span data-stu-id="e9932-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="e9932-133">[Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.</span><span class="sxs-lookup"><span data-stu-id="e9932-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="e9932-134">[Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) --obtenir les dernières informations de sécurité Azure hello et informations.</span><span class="sxs-lookup"><span data-stu-id="e9932-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
