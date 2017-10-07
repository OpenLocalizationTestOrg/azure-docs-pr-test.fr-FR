---
title: "aaaIntroduction tooAzure centre de sécurité | Documents Microsoft"
description: "Découvrez le Centre de sécurité Azure, ses fonctionnalités principales et son fonctionnement."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 287dbaaa7e2004c522f103595bc316261daf05b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security-center"></a>Introduction tooAzure centre de sécurité
Découvrez le Centre de sécurité Azure, ses fonctionnalités principales et son fonctionnement.

> [!NOTE]
> À compter de début juin 2017, centre de sécurité utiliser hello Microsoft Monitoring Agent toocollect et stocker des données. Consultez [Migration de plateforme Azure Security Center](security-center-platform-migration.md) toolearn plus. informations Hello dans cet article représentent les fonctionnalités du centre de sécurité après la transition toohello Microsoft Monitoring Agent.
>
>

## <a name="what-is-azure-security-center"></a>Qu’est-ce que le Centre de sécurité Azure ?
 Centre de sécurité vous permet d’empêcher, détecter et répondre toothreats avec une meilleure visibilité et un contrôle accru de la sécurité hello de vos ressources Azure. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.

## <a name="key-capabilities"></a>Fonctionnalités clés
 Centre de sécurité offre des fonctions de prévention, de détection et de réponse qui sont générées dans tooAzure de menace efficace et facile à utiliser. Ses fonctionnalités principales sont les suivantes :

| Étape | Fonctionnalité |
| --- | --- |
| Prévention |Moniteurs hello état de sécurité de vos ressources Azure |
| Prévention | Définit les stratégies pour vos abonnements Azure, selon les exigences de sécurité de votre entreprise, les types de hello d’applications que vous utilisez et hello sensibilité de vos données |
| Prévention | Propriétaires de service utilise piloté par stratégie de sécurité recommandations tooguide via un processus hello d’implémentation nécessaires des contrôles |
| Prévention | Déploie rapidement des services de sécurité et les appliances de Microsoft et de partenaires |
| Détection |Collecte et analyse les données de sécurité de vos ressources Azure, hello réseau et les solutions de partenaire comme des programmes de logiciel anti-programme malveillant et les pare-feu automatiquement |
| Détection | Utilise global de la menace intelligence à partir de Microsoft produits et services, hello Microsoft Digital Crimes unité (DCU), hello MSRC Microsoft Security Response Center () et les flux externes |
| Détection | Applique des analyses avancées, notamment l’apprentissage automatique (Machine Learning) et des études du comportement |
| Réponse |Fournit des notifications d’incidents/alertes de sécurité hiérarchisées |
| Réponse | Offre un aperçu source hello d’attaque de hello et ressources concernés |
| Réponse | Suggère des façons toostop hello attaque en cours et d’empêcher des attaques futures |

## <a name="introductory-walkthrough"></a>Introduction pas à pas

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement. Ce document n'est pas un guide pas à pas.
>
>

 Vous accéder au centre de sécurité à partir de hello [portail Azure](https://azure.microsoft.com/features/azure-portal/). [Connectez-vous au portail de toohello](https://portal.azure.com). Sous les menus du portail principal hello, faites défiler toohello **centre de sécurité** option ou sélectionnez hello **centre de sécurité** vignette épinglées toohello portail tableau de bord.

![Mosaïque de sécurité dans le portail Azure][1]

Dans le Centre de sécurité, vous pouvez définir des stratégies de sécurité, surveiller des configurations de sécurité et afficher des alertes de sécurité.

### <a name="security-policies"></a>Stratégies de sécurité
Vous pouvez définir des stratégies pour vos abonnements Azure, selon les exigences de sécurité de la société tooyour. Vous pouvez également personnaliser les types toohello des applications que vous utilisez ou toohello de niveau de sensibilité des données de salutation dans chaque abonnement. Par exemple, les ressources utilisées pour le développement ou le test peuvent présenter des exigences de sécurité différentes de celles qui sont utilisées pour les applications de production. De même, les applications dont les données sont réglementées telles que les informations d’identification personnelle (PII)) peuvent nécessiter un niveau de sécurité plus élevé.

> [!NOTE]
> toomodify une stratégie de sécurité, vous devez être propriétaire d’un abonnement administrateur de sécurité ou hello ou un collaborateur. toolearn en savoir plus sur les rôles et les actions autorisées dans le centre de sécurité, consultez [autorisations dans le centre de sécurité Azure](security-center-permissions.md).
>
>

Sur hello **centre de sécurité** panneau, sélectionnez hello **stratégie** vignette pour obtenir la liste de vos abonnements et les groupes de ressources.   

![Panneau Centre de sécurité][2]

Sur hello **stratégie de sécurité** panneau, sélectionnez un abonnement tooview hello les détails de stratégie.

La **collecte de données** active la collecte de données pour une stratégie de sécurité. L’activation autorise les opérations suivantes :

* Analyse quotidienne de toutes les machines virtuelles prises en charge pour la surveillance de la sécurité et le suivi des recommandations.
* Collecte d’événements de sécurité à des fins d’analyse et de détection de menaces.

> [!NOTE]
> Collecte de données est configurée au niveau d’abonnement hello.
>
>

Sélectionnez **stratégie de prévention de** tooopen hello **stratégie de prévention de** panneau. **Afficher les recommandations pour** vous permet de choisir des contrôles de sécurité hello toomonitor et hello recommandations que vous souhaitez toosee en fonction des besoins de sécurité hello des ressources de hello au sein de l’abonnement de hello souhaitées.

### <a name="security-recommendations"></a>Recommandations de sécurité
 Centre de sécurité analyse l’état de sécurité hello de vos ressources Azure tooidentify éventuelles failles de sécurité. Une liste de recommandations vous guide tout au long des processus de hello de la configuration de contrôles nécessaires. Voici quelques exemples :

* Configuration du logiciel anti-programme malveillant toohelp identifier et supprimer les logiciels malveillants
* Configuration réseau sécurité et groupes de règles toocontrol trafic tooVMs
* Configuration des pare-feu d’applications web toohelp vous défendre contre des attaques qui ciblent vos applications web
* Déploiement de mises à jour système manquantes
* Adressage des configurations de système d’exploitation qui ne correspondent pas hello recommandé de lignes de base

Cliquez sur hello **recommandations** vignette pour obtenir la liste des recommandations. Cliquez sur chaque des informations supplémentaires recommandation tooview ou un problème de hello tooresolve tootake action.

![Recommandations de sécurité dans le Centre de sécurité Azure][5]

### <a name="security-state-of-azure-resources"></a>État de sécurité des ressources Azure
Hello **prévention** section du tableau de bord hello affiche hello posture de sécurité globale de l’environnement hello par type de ressource, y compris des machines virtuelles, les applications web et autres ressources.   

Sélectionnez un type de ressource sous **prévention** tooview plus d’informations, notamment une liste de toutes les éventuelles failles de sécurité qui ont été identifiées. (**De calcul** est sélectionné dans l’exemple hello ci-dessous.)

![Mosaïque d’intégrité des ressources][6]

### <a name="security-alerts"></a>Alertes de sécurité
 Centre de sécurité automatiquement collecte, analyse et intègre des données de journal à partir de vos ressources Azure, hello réseau et les solutions de partenaire comme des programmes de logiciel anti-programme malveillant et les pare-feu. Quand des menaces sont détectées, une alerte de sécurité est créée. Voici quelques exemples de détections :

* Des machines virtuelles compromises qui communiquent avec des adresses IP connues comme étant malveillantes
* Des programmes malveillants avancés qui sont détectés à l’aide du rapport d’erreurs Windows
* Des attaques par force brute contre des machines virtuelles
* Des alertes de sécurité de logiciels anti-programme malveillant et de pare-feu intégrés

En cliquant sur hello **alertes de sécurité** vignette affiche une liste des alertes de priorité.

![Alertes de sécurité][7]

Sélectionnez une alerte pour afficher plus d’informations sur les attaques hello et des suggestions pour tooremediate il.

![Détails des alertes de sécurité][8]

### <a name="partner-solutions"></a>Solutions de partenaires
Hello **solutions de partenaire** vignette vous permet de contrôler à un état de sécurité hello aperçu de vos solutions de partenaire intégré à votre abonnement Azure. Centre de sécurité affiche les alertes provenant des solutions hello.

Sélectionnez hello **solutions de partenaire** vignette. Un panneau s'ouvre et affiche la liste de toutes les solutions de partenaires connectées.

![Solutions de partenaires][9]

## <a name="get-started"></a>Prise en main
tooget a démarré avec le centre de sécurité, vous devez un tooMicrosoft abonnement Azure. Le Centre de sécurité est activé avec votre abonnement Azure. Si vous n’avez pas d’abonnement, vous pouvez vous inscrire à un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).

 Vous accéder au centre de sécurité à partir de hello [portail Azure](https://azure.microsoft.com/features/azure-portal/). Consultez hello [documentation portail](https://azure.microsoft.com/documentation/services/azure-portal/) toolearn plus.

[Prise en main d’Azure Security Center](security-center-get-started.md) vous guide rapidement dans les composants de contrôle de la sécurité et de gestion hello du centre de sécurité.

## <a name="next-steps"></a>Étapes suivantes
Dans ce document, vous ont été introduites tooSecurity centre, ses fonctionnalités clées, et comment tooget a démarré. toolearn, voir hello suivant des ressources :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) : Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) — Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) : en savoir comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) — Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
- [Sécurité des données Azure Security Center](security-center-data-security.md) : découvrez comment les données sont gérées et protégées dans Security Center.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche.
* [Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenir les dernières informations de sécurité Azure hello et informations.

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
