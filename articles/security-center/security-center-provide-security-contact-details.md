---
title: "Fournir les détails du contact de sécurité dans Azure Security Center | Microsoft Docs"
description: "Ce document vous montre comment fournir les détails du contact de sécurité dans Azure Security Center."
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
ms.openlocfilehash: 1a6e5e915745dd3588fbc54b353daa947b1c4289
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="231e5-103">Fournir les détails du contact de sécurité dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="231e5-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="231e5-104">Azure Security Center vous recommande de fournir les détails du contact de sécurité pour votre abonnement Azure, si vous ne l’avez pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="231e5-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="231e5-105">Ces informations seront être utilisées par Microsoft pour vous contacter si Microsoft Security Response Center (MSRC) découvre que vos données client ont été utilisées par un tiers illégal ou non autorisé.</span><span class="sxs-lookup"><span data-stu-id="231e5-105">This information will be used by Microsoft to contact you if the Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="231e5-106">MSRC procède à une surveillance de la sécurité sur l'infrastructure et le réseau Azure et reçoit des plaintes concernant l’intelligence des menaces et des mauvaises utilisations de tiers.</span><span class="sxs-lookup"><span data-stu-id="231e5-106">MSRC performs select security monitoring of the Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="231e5-107">Une notification par courrier électronique est envoyée à la première occurrence quotidienne d’une alerte et uniquement pour les alertes de gravité élevée.</span><span class="sxs-lookup"><span data-stu-id="231e5-107">An email notification is sent on the first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="231e5-108">Les préférences de courrier électronique peuvent uniquement être configurées pour les stratégies d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="231e5-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="231e5-109">Les groupes de ressources d’un abonnement hériteront de ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="231e5-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="231e5-110">Ce document présente le service à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="231e5-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="231e5-111">Il ne s’agit pas d’un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="231e5-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="231e5-112">Implémenter la recommandation</span><span class="sxs-lookup"><span data-stu-id="231e5-112">Implement the recommendation</span></span>
1. <span data-ttu-id="231e5-113">Dans le panneau **Recommandations**, sélectionnez **Fournissez les détails du contact de sécurité**.</span><span class="sxs-lookup"><span data-stu-id="231e5-113">In the **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="231e5-114">![Fournir le contact de sécurité][1]</span><span class="sxs-lookup"><span data-stu-id="231e5-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="231e5-115">Le panneau **Fournissez les détails du contact de sécurité**s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="231e5-115">This opens the blade **Provide security contact details**.</span></span> <span data-ttu-id="231e5-116">Sélectionnez l’abonnement Azure pour lequel fournir les informations du contact.</span><span class="sxs-lookup"><span data-stu-id="231e5-116">Select the Azure subscription to provide contact information on.</span></span>
   <span data-ttu-id="231e5-117">![Fournissez les détails du contact de sécurité][2]</span><span class="sxs-lookup"><span data-stu-id="231e5-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="231e5-118">Un second panneau **Fournissez les détails du contact de sécurité** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="231e5-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="231e5-119">Entrez l’adresse e-mail du contact de sécurité. S’il y a plusieurs adresses, séparez-les par des virgules.</span><span class="sxs-lookup"><span data-stu-id="231e5-119">Enter the security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="231e5-120">Vous pouvez entrer le nombre d’adresses e-mail que vous voulez.</span><span class="sxs-lookup"><span data-stu-id="231e5-120">There is not a limit to the number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="231e5-121">Entrez le numéro de téléphone international du contact de sécurité.</span><span class="sxs-lookup"><span data-stu-id="231e5-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="231e5-122">Pour recevoir des courriers électroniques concernant les alertes de gravité élevée, activez l’option **Send me emails about alerts**(M’envoyer des messages électroniques concernant les alertes).</span><span class="sxs-lookup"><span data-stu-id="231e5-122">To receive emails about high severity alerts, turn on the option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="231e5-123">À l’avenir, vous aurez la possibilité d’envoyer des notifications par courrier électronique aux propriétaires de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="231e5-123">In the future, you will have the option to send email notifications to subscription owners.</span></span> <span data-ttu-id="231e5-124">Cette option est actuellement grisée.</span><span class="sxs-lookup"><span data-stu-id="231e5-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="231e5-125">Sélectionnez **OK** pour appliquer les informations du contact de sécurité à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="231e5-125">Select **OK** to apply the security contact information to your subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="231e5-126">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="231e5-126">See also</span></span>
<span data-ttu-id="231e5-127">Pour plus d’informations sur le Centre de sécurité, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="231e5-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="231e5-128">[Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md) : découvrez comment configurer des stratégies de sécurité pour vos groupes de ressources et abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="231e5-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="231e5-129">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="231e5-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="231e5-130">[Surveillance de l’intégrité de la sécurité dans Azure Security Center](security-center-monitoring.md) : découvrez comment surveiller l’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="231e5-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="231e5-131">[Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="231e5-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="231e5-132">[Surveillance des solutions partenaires avec Azure Security Center](security-center-partner-solutions.md) : découvrez comment surveiller l’état d’intégrité de vos solutions partenaires.</span><span class="sxs-lookup"><span data-stu-id="231e5-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="231e5-133">[FAQ sur Azure Security Center](security-center-faq.md) : forum aux questions concernant l’utilisation de ce service.</span><span class="sxs-lookup"><span data-stu-id="231e5-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="231e5-134">[Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : découvrez les dernières nouvelles et informations sur la sécurité Azure.</span><span class="sxs-lookup"><span data-stu-id="231e5-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
