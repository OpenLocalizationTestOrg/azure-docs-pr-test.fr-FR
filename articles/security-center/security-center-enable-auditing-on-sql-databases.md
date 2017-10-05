---
title: "Activation de l’audit et détection des menaces dans les bases de données SQL dans Azure Security Center | Microsoft Docs"
description: "Ce document vous montre comment implémenter la recommandation Azure Security Center ** activer la détection de menace et de l’audit sur les bases de données SQL **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: 8f4febdaa4497fee0dc690b59cd6eaa415c5e5cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="8474f-103">Activation de l’audit et détection des menaces dans les bases de données SQL dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="8474f-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="8474f-104">Azure Security Center vous recommande d’activer l’audit et la détection des menaces sur toutes les bases de données SQL, si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="8474f-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="8474f-105">L’audit et la détection des menaces peuvent vous aider à respecter une conformité réglementaire, à comprendre l’activité de la base de données et à découvrir des discordances et des anomalies susceptibles d’indiquer des problèmes pour l’entreprise ou des violations de la sécurité.</span><span class="sxs-lookup"><span data-stu-id="8474f-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="8474f-106">Une fois que vous avez activé l’audit, vous pouvez configurer les paramètres Threat Detection et les adresses électroniques pour recevoir des alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="8474f-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="8474f-107">Threat Detection permet de détecter les activités base de données anormales indiquant la présence potentielle de menaces de sécurité pour la base de données.</span><span class="sxs-lookup"><span data-stu-id="8474f-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="8474f-108">Cela vous permet de détecter et de répondre aux menaces potentielles à mesure qu’elles surviennent.</span><span class="sxs-lookup"><span data-stu-id="8474f-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="8474f-109">Cette recommandation s’applique uniquement au service SQL Azure, elle ne concerne pas SQL en cours d’exécution sur vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8474f-109">This recommendation applies to the Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="8474f-110">Ce document présente le service à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="8474f-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="8474f-111">Il ne s’agit pas d’un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="8474f-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="8474f-112">Implémenter la recommandation</span><span class="sxs-lookup"><span data-stu-id="8474f-112">Implement the recommendation</span></span>
1. <span data-ttu-id="8474f-113">Dans le panneau **Recommandations**, sélectionnez **Activer l’audit et la détection des menaces sur les bases de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="8474f-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="8474f-114">Cette opération ouvre le panneau **Activer l’audit et la détection des menaces sur les bases de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="8474f-114">This opens the **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![Activer l’audit sur les bases de données SQL][1]
2. <span data-ttu-id="8474f-116">Sélectionnez une base de données SQL sur laquelle activer l’audit.</span><span class="sxs-lookup"><span data-stu-id="8474f-116">Select a SQL database to enable auditing on.</span></span> <span data-ttu-id="8474f-117">Cette opération ouvre le panneau **Audit et détection des menaces**.</span><span class="sxs-lookup"><span data-stu-id="8474f-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="8474f-118">Dans le panneau **Audit et détection des menaces**, sélectionnez **ON** sous **Audit**.</span><span class="sxs-lookup"><span data-stu-id="8474f-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Activer l’audit et la détection des menaces][2]
4. <span data-ttu-id="8474f-120">Suivez les étapes de la rubrique [Détection de menaces pour les bases de données SQL dans le portail Azure](../sql-database/sql-database-threat-detection-portal.md) pour activer et configurer la détection des menaces (Threat Detection) et configurer la liste des adresses électroniques qui recevront les alertes de sécurité lors de la détection d’activités anormales.</span><span class="sxs-lookup"><span data-stu-id="8474f-120">Follow the steps in [SQL Database Threat Detection in the Azure portal](../sql-database/sql-database-threat-detection-portal.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="8474f-121">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8474f-121">See also</span></span>
<span data-ttu-id="8474f-122">Cet article vous a montré comment implémenter la recommandation de Security Center « Activer l’audit et la détection des menaces sur les bases de données SQL ».</span><span class="sxs-lookup"><span data-stu-id="8474f-122">This article showed you how to implement the Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="8474f-123">Pour en savoir plus sur la sécurisation de votre base de données SQL, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="8474f-123">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="8474f-124">Sécurisation de votre base de données SQL</span><span class="sxs-lookup"><span data-stu-id="8474f-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="8474f-125">Pour plus d’informations sur le Centre de sécurité, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="8474f-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="8474f-126">[Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md) : découvrez comment configurer des stratégies de sécurité pour vos groupes de ressources et abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="8474f-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="8474f-127">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="8474f-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="8474f-128">[Surveillance de l’intégrité de la sécurité dans Azure Security Center](security-center-monitoring.md) : découvrez comment surveiller l’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="8474f-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="8474f-129">[Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="8474f-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="8474f-130">[Surveillance des solutions partenaires avec Azure Security Center](security-center-partner-solutions.md) : découvrez comment surveiller l’état d’intégrité de vos solutions partenaires.</span><span class="sxs-lookup"><span data-stu-id="8474f-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="8474f-131">[FAQ sur Azure Security Center](security-center-faq.md) : forum aux questions concernant l’utilisation de ce service.</span><span class="sxs-lookup"><span data-stu-id="8474f-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="8474f-132">[Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : découvrez les dernières nouvelles et informations sur la sécurité Azure.</span><span class="sxs-lookup"><span data-stu-id="8474f-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
