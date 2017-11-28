---
title: "Activer l’audit et la détection des menaces sur les serveurs SQL dans Azure Security Center | Microsoft Docs"
description: "Ce document vous montre comment implémenter la recommandation Azure Security Center ** activer l’audit et menace pour la détection sur les serveurs SQL **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: 660b537aef8d175a478ff93d60b8391d55fc92ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a><span data-ttu-id="92b4b-103">Activer l’audit et la détection des menaces sur les serveurs SQL dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="92b4b-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span></span>
<span data-ttu-id="92b4b-104">Azure Security Center vous recommande d’activer l’audit et la détection des menaces pour toutes les bases de données sur vos serveurs SQL Azure si l’audit n’est pas déjà activé.</span><span class="sxs-lookup"><span data-stu-id="92b4b-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span></span> <span data-ttu-id="92b4b-105">L’audit et la détection des menaces peuvent vous aider à respecter une conformité réglementaire, à comprendre l’activité de la base de données, et à découvrir des discordances et des anomalies susceptibles d’indiquer des problèmes pour l’entreprise ou des violations de la sécurité.</span><span class="sxs-lookup"><span data-stu-id="92b4b-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="92b4b-106">Une fois que vous avez activé l’audit, vous pouvez configurer les paramètres Threat Detection et les adresses électroniques pour recevoir des alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="92b4b-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="92b4b-107">Threat Detection permet de détecter les activités base de données anormales indiquant la présence potentielle de menaces de sécurité pour la base de données.</span><span class="sxs-lookup"><span data-stu-id="92b4b-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="92b4b-108">Cela vous permet de détecter et de répondre aux menaces potentielles à mesure qu’elles surviennent.</span><span class="sxs-lookup"><span data-stu-id="92b4b-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="92b4b-109">Cette recommandation s’applique uniquement au service SQL Azure, elle ne concerne pas SQL Server en cours d’exécution sur vos machines virtuelles dans Azure Infrastructure Services (Azure IaaS).</span><span class="sxs-lookup"><span data-stu-id="92b4b-109">This recommendation applies to the Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span></span>

> [!NOTE]
> <span data-ttu-id="92b4b-110">Ce document présente le service à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="92b4b-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="92b4b-111">Il ne s’agit pas d’un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="92b4b-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="92b4b-112">Implémenter la recommandation</span><span class="sxs-lookup"><span data-stu-id="92b4b-112">Implement the recommendation</span></span>
1. <span data-ttu-id="92b4b-113">Dans le panneau **Recommandations**, sélectionnez **Activer l’audit et la détection des menaces sur les serveurs SQL**.</span><span class="sxs-lookup"><span data-stu-id="92b4b-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span></span>  <span data-ttu-id="92b4b-114">Ceci ouvre le panneau **Activer l’audit et la détection des menaces sur les serveurs SQL**.</span><span class="sxs-lookup"><span data-stu-id="92b4b-114">This opens the **Enable Auditing & Threat detection on SQL servers** blade.</span></span>

   ![Activer l’audit sur les serveurs SQL][1]
2. <span data-ttu-id="92b4b-116">Sélectionnez un serveur SQL sur lequel activer l’audit et la détection des menaces.</span><span class="sxs-lookup"><span data-stu-id="92b4b-116">Select a SQL server to enable auditing and threat detection on.</span></span> <span data-ttu-id="92b4b-117">Ceci opération ouvre le panneau **Audit et détection des menaces**.</span><span class="sxs-lookup"><span data-stu-id="92b4b-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="92b4b-118">Dans le panneau **Audit et détection des menaces**, sélectionnez **ACTIVÉ** sous **Audit**.</span><span class="sxs-lookup"><span data-stu-id="92b4b-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Activer l’audit des paramètres][2]
4. <span data-ttu-id="92b4b-120">Suivez les étapes de la rubrique [Audit de base de données SQL dans le portail Azure](../sql-database/sql-database-auditing-portal.md) pour configurer l’emplacement de stockage de vos journaux d’audit.</span><span class="sxs-lookup"><span data-stu-id="92b4b-120">Follow the steps in [SQL database auditing in the Azure portal](../sql-database/sql-database-auditing-portal.md) to configure storage where your audit logs will be stored.</span></span> <span data-ttu-id="92b4b-121">Le compte de stockage de l’abonnement pour la collecte de données est le compte de stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="92b4b-121">The subscription's storage account for data collection is the default storage account.</span></span>
5. <span data-ttu-id="92b4b-122">Suivez les étapes de la rubrique [Prise en main de Threat Detection pour la base de données SQL](../sql-database/sql-database-threat-detection.md) pour activer et configurer la détection des menaces (Threat Detection) et configurer la liste des adresses électroniques qui recevront les alertes de sécurité lors de la détection d’activités anormales.</span><span class="sxs-lookup"><span data-stu-id="92b4b-122">Follow the steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="92b4b-123">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="92b4b-123">See also</span></span>
<span data-ttu-id="92b4b-124">Cet article vous a montré comment implémenter la recommandation de Security Center « Activer l’audit et la détection des menaces sur les serveurs SQL ».</span><span class="sxs-lookup"><span data-stu-id="92b4b-124">This article showed you how to implement the Security Center recommendation "Enable auditing and threat detection on SQL servers."</span></span> <span data-ttu-id="92b4b-125">Pour en savoir plus sur la sécurisation de votre base de données SQL, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="92b4b-125">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="92b4b-126">Sécurisation de votre base de données SQL</span><span class="sxs-lookup"><span data-stu-id="92b4b-126">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="92b4b-127">Pour plus d’informations sur le Centre de sécurité, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="92b4b-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="92b4b-128">[Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md) : découvrez comment configurer des stratégies de sécurité pour vos groupes de ressources et abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="92b4b-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="92b4b-129">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="92b4b-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="92b4b-130">[Surveillance de l’intégrité de la sécurité dans Azure Security Center](security-center-monitoring.md) : découvrez comment surveiller l’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="92b4b-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="92b4b-131">[Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="92b4b-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="92b4b-132">[Surveillance des solutions partenaires avec Azure Security Center](security-center-partner-solutions.md) : découvrez comment surveiller l’état d’intégrité de vos solutions partenaires.</span><span class="sxs-lookup"><span data-stu-id="92b4b-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="92b4b-133">[FAQ sur Azure Security Center](security-center-faq.md) : forum aux questions concernant l’utilisation de ce service.</span><span class="sxs-lookup"><span data-stu-id="92b4b-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="92b4b-134">[Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : découvrez les dernières nouvelles et informations sur la sécurité Azure.</span><span class="sxs-lookup"><span data-stu-id="92b4b-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
