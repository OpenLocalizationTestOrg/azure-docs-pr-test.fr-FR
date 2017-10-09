---
title: "collecte des données dans le centre de sécurité Azure aaaEnable | Documents Microsoft"
description: " Découvrez comment tooenable collecte des données dans le centre de sécurité Azure. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 78bbf9a3d852095e2a1387c1606ff4bbb778a0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a>Activer la collecte des données dans Azure Security Center

> [!NOTE]
> À compter de début juin 2017, centre de sécurité utiliser hello Microsoft Monitoring Agent toocollect et stocker des données. toolearn, voir [Azure Security Center Platform Migration](security-center-platform-migration.md). informations Hello dans cet article représentent les fonctionnalités du centre de sécurité après la transition toohello Microsoft Monitoring Agent.
>
>

Centre de sécurité collecte des données à partir de votre tooassess de machines virtuelles (VM) leur état de sécurité, fournir des recommandations de sécurité et vous alerter toothreats. Lorsque vous accédez centre de sécurité, vous avez hello option tooenable collecte des données pour tous les ordinateurs virtuels dans votre abonnement. Si la collecte de données n’est pas activée, le centre de sécurité vous recommande d’activer la collecte de données dans la stratégie de sécurité hello pour cet abonnement.

Lors de la collecte des données est activée, hello de dispositions de centre de sécurité Microsoft Monitoring Agent sur toutes les existantes prise en charge des machines virtuelles et nouveaux qui sont créés. Hello Microsoft Monitoring Agent analyse les diverses configurations liées à la sécurité. En outre, système d’exploitation de hello déclenche des événements de journal des événements. Il peut s’agir des données suivantes : type et version de système d’exploitation, journaux de système d’exploitation (journaux d’événements Windows), processus en cours d’exécution, nom de machine, adresses IP, utilisateur connecté et ID de locataire. Hello Microsoft Monitoring Agent lit les configurations et les entrées de journal des événements et copie l’espace de travail tooyour de données hello pour l’analyse. Hello Microsoft Monitoring Agent copie également l’espace de travail du tooyour fichiers dump sur incident.

Si vous utilisez le niveau gratuit de hello du centre de sécurité, vous pouvez désactiver la collecte de données à partir d’ordinateurs virtuels en désactivant la collecte de données dans la stratégie de sécurité hello. Le fait de désactiver la collecte de données limite les évaluations de sécurité pour vos machines virtuelles. toolearn, voir [la désactivation de la collecte de données](#disabling-data-collection). La collecte des artefacts et les captures instantanées des disques de machine virtuelle sont activées, même si la collecte de données est désactivée. Collecte de données est requise pour les abonnements sur le niveau Standard de hello du centre de sécurité.

> [!NOTE]
> En savoir plus sur les [niveaux tarifaires](security-center-pricing.md) Gratuit et Standard de Security Center.
>
>

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement. Ce document n'est pas un guide pas à pas.
>
>

1. Bonjour **recommandations** panneau, sélectionnez **activer la collecte des données pour les abonnements**.  Cette opération ouvre hello **activer la collecte de données de** panneau.
   ![Panneau Recommandations][2]
2. Sur hello **activer la collecte de données de** panneau, sélectionnez votre abonnement. Hello **stratégie de sécurité** panneau pour cet abonnement s’ouvre.
3. Sur hello **stratégie de sécurité** panneau, sélectionnez **sur** sous **collecte des données** tooautomatically collecter les journaux. Mise sous tension hello de dispositions de collection de données analyse d’extension sur tous les actuelle et la nouvelle prise en charge machines virtuelles dans l’abonnement de hello.
4. Sélectionnez **Enregistrer**.
5. Sélectionnez **OK**.

## <a name="disabling-data-collection"></a>Désactivation de la collecte des données
Si vous utilisez le niveau gratuit de hello du centre de sécurité, vous pouvez désactiver la collecte des données à partir d’ordinateurs virtuels à tout moment en désactivant la collecte de données dans la stratégie de sécurité hello. Collecte de données est requise pour les abonnements sur le niveau Standard de hello du centre de sécurité.

1. Retourner toohello **centre de sécurité** panneau et sélectionnez hello **stratégie** vignette. Cette opération ouvre hello **sécurité définir stratégie stratégie par abonnement** panneau.
   ![Sélectionnez la vignette de stratégie hello][5]
2. Sur hello **sécurité définir stratégie stratégie par abonnement** panneau, sélectionnez hello souscription que toodisable la collecte de données.
3. Hello **stratégie de sécurité** panneau pour cet abonnement s’ouvre.  Sélectionnez **Désactivée** sous Collecte des données.
4. Sélectionnez **enregistrer** dans le ruban supérieur de hello.

## <a name="next-steps"></a>Étapes suivantes
Cet article vous a montré comment tooimplement hello centre de sécurité recommandation « activer collecte de données. » toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md)--Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md)--Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
- [Sécurité des données Azure Security Center](security-center-data-security.md) : découvrez comment les données sont gérées et protégées dans Security Center.
* [Forum aux questions sur Azure Security Center](security-center-faq.md)--rechercher Forum aux questions sur l’utilisation du service de hello.
* [Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/)--obtenir les dernières informations de sécurité Azure hello et informations.

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
