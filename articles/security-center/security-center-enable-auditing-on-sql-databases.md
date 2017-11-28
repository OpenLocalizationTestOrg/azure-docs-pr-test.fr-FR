---
title: "détection de l’audit et de la menace aaaEnable sur SQL des bases de données dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** activer la détection de menace et de l’audit sur les bases de données SQL **."
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
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="44513-103">Activation de l’audit et détection des menaces dans les bases de données SQL dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="44513-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="44513-104">Azure Security Center vous recommande d’activer l’audit et la détection des menaces sur toutes les bases de données SQL, si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="44513-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="44513-105">L’audit et la détection des menaces peuvent vous aider à respecter une conformité réglementaire, à comprendre l’activité de la base de données et à découvrir des discordances et des anomalies susceptibles d’indiquer des problèmes pour l’entreprise ou des violations de la sécurité.</span><span class="sxs-lookup"><span data-stu-id="44513-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="44513-106">Une fois que vous avez activé l’audit, vous pouvez configurer la détection des menaces paramètres et des messages électroniques tooreceive sécurité les alertes.</span><span class="sxs-lookup"><span data-stu-id="44513-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="44513-107">La détection des menaces détecte des activités de base de données anormales indiquant de base de données des toohello des menaces de sécurité potentielles.</span><span class="sxs-lookup"><span data-stu-id="44513-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="44513-108">Cela vous permet de toodetect et répond toopotential menaces qu’ils se produisent.</span><span class="sxs-lookup"><span data-stu-id="44513-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="44513-109">Cette recommandation s’applique toohello service SQL Azure uniquement. Il n’inclut pas SQL en cours d’exécution sur vos ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="44513-109">This recommendation applies toohello Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="44513-110">Ce document présente le service de hello à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="44513-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="44513-111">Il ne s’agit pas d’un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="44513-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="44513-112">Implémenter la recommandation de hello</span><span class="sxs-lookup"><span data-stu-id="44513-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="44513-113">Bonjour **recommandations** panneau, sélectionnez **activer l’audit et menace pour la détection sur les bases de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="44513-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="44513-114">Cette opération ouvre hello **activer l’audit et menace pour la détection sur les bases de données SQL** panneau.</span><span class="sxs-lookup"><span data-stu-id="44513-114">This opens hello **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![Activer l’audit sur les bases de données SQL][1]
2. <span data-ttu-id="44513-116">Sélectionnez une base de données tooenable l’audit SQL sur.</span><span class="sxs-lookup"><span data-stu-id="44513-116">Select a SQL database tooenable auditing on.</span></span> <span data-ttu-id="44513-117">Cette opération ouvre hello **audit et la détection des menaces** panneau.</span><span class="sxs-lookup"><span data-stu-id="44513-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="44513-118">Sur hello **audit et la détection des menaces** panneau, sélectionnez **ON** sous **audit**.</span><span class="sxs-lookup"><span data-stu-id="44513-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Activer l’audit et la détection des menaces][2]
4. <span data-ttu-id="44513-120">Suivez les étapes de hello dans [la détection des menaces de base de données SQL Bonjour Azure portal](../sql-database/sql-database-threat-detection-portal.md) tooturn sur et configurer la détection des menaces et la liste de hello tooconfigure d’adresses de messagerie qui recevront les alertes de sécurité lors de la détection des activités anormales sont.</span><span class="sxs-lookup"><span data-stu-id="44513-120">Follow hello steps in [SQL Database Threat Detection in hello Azure portal](../sql-database/sql-database-threat-detection-portal.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="44513-121">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="44513-121">See also</span></span>
<span data-ttu-id="44513-122">Cet article vous a montré comment tooimplement hello centre de sécurité recommandation « Enable Auditing & menace pour la détection sur les bases de données SQL. »</span><span class="sxs-lookup"><span data-stu-id="44513-122">This article showed you how tooimplement hello Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="44513-123">toolearn savoir plus sur la sécurisation de votre base de données SQL, voir hello :</span><span class="sxs-lookup"><span data-stu-id="44513-123">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="44513-124">Sécurisation de votre base de données SQL</span><span class="sxs-lookup"><span data-stu-id="44513-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="44513-125">toolearn en savoir plus sur le centre de sécurité, voir hello :</span><span class="sxs-lookup"><span data-stu-id="44513-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="44513-126">[Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="44513-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="44513-127">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="44513-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="44513-128">[Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="44513-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="44513-129">[Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="44513-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="44513-130">[Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.</span><span class="sxs-lookup"><span data-stu-id="44513-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="44513-131">[Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.</span><span class="sxs-lookup"><span data-stu-id="44513-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="44513-132">[Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) --obtenir les dernières informations de sécurité Azure hello et informations.</span><span class="sxs-lookup"><span data-stu-id="44513-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
