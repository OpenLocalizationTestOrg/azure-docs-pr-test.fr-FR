---
title: "aaaEnable chiffrement Transparent des données dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** activer Transparent de données chiffrement **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="9f8dd-103">Activation de Transparent Data Encryption dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9f8dd-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="9f8dd-104">Azure Security Center vous recommande d’activer TDE (Transparent Data Encryption) sur les bases de données SQL si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="9f8dd-105">Chiffrement transparent des données protègent vos données et vous aide à répondre aux exigences de conformité en chiffrant votre base de données, les sauvegardes associées et les fichiers journaux des transactions au repos, sans nécessiter de modifications tooyour application.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes tooyour application.</span></span> <span data-ttu-id="9f8dd-106">Voir toolearn [chiffrement Transparent des données avec Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="9f8dd-106">toolearn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="9f8dd-107">Cette recommandation s’applique toohello service SQL Azure uniquement. n’inclut pas SQL en cours d’exécution sur vos ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-107">This recommendation applies toohello Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="9f8dd-108">Ce document présente le service de hello à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="9f8dd-109">Il ne s’agit pas d’un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="9f8dd-110">Implémenter la recommandation de hello</span><span class="sxs-lookup"><span data-stu-id="9f8dd-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="9f8dd-111">Bonjour **recommandations** panneau, sélectionnez **activer Transparent Data Encryption**.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-111">In hello **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="9f8dd-112">![Activer Transparent Data Encryption][1]</span><span class="sxs-lookup"><span data-stu-id="9f8dd-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="9f8dd-113">Cette opération ouvre hello **activer le chiffrement Transparent des données sur les bases de données SQL** panneau.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-113">This opens hello **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="9f8dd-114">Sélectionnez un tooenable de base de données SQL chiffrement transparent des données.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-114">Select a SQL database tooenable TDE on.</span></span>
   <span data-ttu-id="9f8dd-115">![Sélectionnez la base de données SQL tooenable chiffrement transparent des données sur][2]</span><span class="sxs-lookup"><span data-stu-id="9f8dd-115">![Select SQL DB tooenable TDE on][2]</span></span>
3. <span data-ttu-id="9f8dd-116">Sur hello **chiffrement Transparent des données** panneau, sélectionnez **ON** sous le chiffrement des données et sélectionnez **enregistrer** dans le ruban supérieur de hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-116">On hello **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in hello top ribbon of hello blade.</span></span>
   <span data-ttu-id="9f8dd-117">![Activer le chiffrement transparent des données][3]</span><span class="sxs-lookup"><span data-stu-id="9f8dd-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="9f8dd-118">Une fois que le chiffrement transparent des données sont activée sur hello sélectionné base de données SQL, hello **état du chiffrement** modifiera trop**Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-118">Once TDE is enabled on hello selected SQL database, hello **Encryption status** will change too**Encrypted**.</span></span>    

   ![État du chiffrement][4]

## <a name="see-also"></a><span data-ttu-id="9f8dd-120">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9f8dd-120">See also</span></span>
<span data-ttu-id="9f8dd-121">Cet article vous a montré comment tooimplement hello recommandation du centre de sécurité « Activer Transparent Data Encryption ».</span><span class="sxs-lookup"><span data-stu-id="9f8dd-121">This article showed you how tooimplement hello Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="9f8dd-122">toolearn en savoir plus sur SQL TDE, voir hello :</span><span class="sxs-lookup"><span data-stu-id="9f8dd-122">toolearn more about SQL TDE, see hello following:</span></span>

* [<span data-ttu-id="9f8dd-123">Transparent Data Encryption avec Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="9f8dd-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="9f8dd-124">Prise en main du chiffrement transparent des données (TDE)</span><span class="sxs-lookup"><span data-stu-id="9f8dd-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="9f8dd-125">toolearn en savoir plus sur le centre de sécurité, voir hello :</span><span class="sxs-lookup"><span data-stu-id="9f8dd-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="9f8dd-126">[Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="9f8dd-127">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="9f8dd-128">[Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="9f8dd-129">[Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="9f8dd-130">[Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="9f8dd-131">[Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="9f8dd-132">[Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) --obtenir les dernières informations de sécurité Azure hello et informations.</span><span class="sxs-lookup"><span data-stu-id="9f8dd-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
