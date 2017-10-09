---
title: "guide de démarrage rapide du centre de sécurité d’aaaAzure | Documents Microsoft"
description: "Cet article vous aide à commencer rapidement Azure Security Center en vous guidant à travers hello analyse et la stratégie de gestion les composants de sécurité en liant vous toonext étapes."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 61e95a87-39c5-48f5-aee6-6f90ddcd336e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 23b2444ba1ba30d0a1bd1a1afbc4fd0abfd0827c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-quick-start-guide"></a>Guide de démarrage rapide du Centre de sécurité Azure
Cet article vous permet de rapidement commencer à utiliser Azure Security Center en vous guidant à travers hello analyse et la stratégie de gestion des composants de sécurité du centre de sécurité.

> [!NOTE]
> À compter de début juin 2017, centre de sécurité utiliser hello Microsoft Monitoring Agent toocollect et stocker des données. Consultez [Migration de plateforme Azure Security Center](security-center-platform-migration.md) toolearn plus. informations Hello dans cet article représentent les fonctionnalités du centre de sécurité après la transition toohello Microsoft Monitoring Agent.
>
>

## <a name="prerequisites"></a>Composants requis
tooget a démarré avec le centre de sécurité, vous devez disposer d’un tooMicrosoft d’abonnement Azure. Si vous n’avez pas d’abonnement, vous pouvez vous inscrire pour avoir un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).

niveau gratuit de Hello du centre de sécurité est automatiquement activé avec votre abonnement et offre une visibilité en état de la sécurité de vos ressources Azure hello. Il fournit une gestion des stratégies de sécurité de base, des recommandations de sécurité et une intégration avec les produits et services de sécurité des partenaires Azure.

Vous accéder au centre de sécurité à partir de hello [portail Azure](https://azure.microsoft.com/features/azure-portal/). toolearn en savoir plus sur hello portail Azure, consultez hello [documentation portail](https://azure.microsoft.com/documentation/services/azure-portal/).

## <a name="permissions"></a>Autorisations
Dans le centre de sécurité, vous voyez uniquement les informations liées tooan ressource Azure lorsque vous sont assignés rôle hello de propriétaire, collaborateur ou lecteur pour le groupe d’abonnement ou une ressource hello appartenant à une ressource. Consultez [autorisations dans le centre de sécurité Azure](security-center-permissions.md) toolearn plus d’informations sur les rôles et les actions autorisées dans le centre de sécurité.

## <a name="data-collection"></a>Collecte des données
Centre de sécurité collecte des données à partir de votre tooassess de machines virtuelles (VM) leur état de sécurité, fournir des recommandations de sécurité et vous alerter toothreats. Lorsque vous accédez à Azure Security Center pour la première fois, la collecte de données est activée sur toutes les machines virtuelles de votre abonnement. Hello de dispositions de centre de sécurité Microsoft Monitoring Agent sur toutes les existantes pris en charge les machines virtuelles Azure et nouveaux qui sont créés. Consultez [activer la collecte des données](security-center-enable-data-collection.md) toolearn plus sur le fonctionne de la collecte de données.

La collecte de données est recommandée. Si vous utilisez le niveau gratuit de hello du centre de sécurité, vous pouvez désactiver la collecte de données à partir d’ordinateurs virtuels en désactivant la collecte de données dans la stratégie de sécurité hello. Collecte de données est requise pour les abonnements sur le niveau Standard de hello du centre de sécurité. Consultez [tarification du centre de sécurité](security-center-pricing.md) toolearn savoir plus sur hello gratuit et les niveaux de tarification Standard.

Hello suit décrire comment tooaccess et utilisez hello des composants du centre de sécurité. Dans ces étapes, nous vous indiquons comment tooturn désactiver la collecte de données si vous choisissez tooopt out.

> [!NOTE]
> Cet article présente le service de hello à l’aide d’un exemple de déploiement. Il ne s’agit pas d’un guide pas à pas.
>
>

## <a name="access-security-center"></a>Accéder au Centre de sécurité
Dans le portail hello, suivez ces étapes de tooaccess centre de sécurité :

1. Sur hello **Microsoft Azure** menu, sélectionnez **centre de sécurité**.

   ![Menu Azure][1]
2. Si vous accédez à centre de sécurité pour hello première fois, hello **Bienvenue** panneau s’ouvre. Sélectionnez **lancer le centre de sécurité** tooopen hello **centre de sécurité** panneau et tooenable collecte de données.
   ![Écran d’accueil][10]
3. Une fois que vous lancez le centre de sécurité à partir du Panneau de bienvenue hello ou sélectionnez le centre de sécurité à partir du menu de Microsoft Azure hello, hello **centre de sécurité** panneau s’ouvre. Pour un accès facile toohello **centre de sécurité** panneau Bonjour de futures, sélectionnez hello **Pin panneau toodashboard** option (en haut à droite).
   ![Option de PIN panneau toodashboard][2]

## <a name="use-security-center"></a>Utiliser le Centre de sécurité
Vous pouvez configurer des stratégies de sécurité pour vos groupes de ressources et abonnements Azure. Configurons une stratégie de sécurité pour votre abonnement :

1. Sur hello **centre de sécurité** panneau, sélectionnez hello **stratégie** vignette.
2. Sur hello **stratégie de sécurité - définir une stratégie par abonnement** panneau, sélectionnez un abonnement.
3. Sur hello **stratégie de sécurité** panneau, **collecte des données** tooautomatically activé les journaux collecter. Hello, extension de surveillance est configurée sur toutes les machines virtuelles actuelles et nouvelles dans l’abonnement de hello. (Sur le niveau gratuit de hello du centre de sécurité, vous pouvez désactiver la collecte de données en définissant **collecte des données** trop**hors**. Paramètre **collecte des données** trop**hors** empêche le centre de sécurité de l’octroi à d’alertes de sécurité et des recommandations.)
4. Sur hello **stratégie de sécurité** panneau, sélectionnez **stratégie de prévention de**. Cette opération ouvre hello **stratégie de prévention de** panneau.
5. Sur hello **stratégie de prévention de** panneau, activer les recommandations hello que vous souhaitez toosee dans le cadre de votre stratégie de sécurité. Exemples :

   * Paramètre **mises à jour système** trop**sur** toutes les analyses de prise en charge des machines virtuelles pour les mises à jour du système d’exploitation.
   * Paramètre **les vulnérabilités du système d’exploitation** trop**sur** toutes prises en charge tooidentify de machines virtuelles toutes les configurations de système d’exploitation qui peuvent effectuer des analyses hello VM tooattack plus vulnérable.

### <a name="view-recommendations"></a>Afficher les recommandations
1. Retourner toohello **centre de sécurité** panneau et sélectionnez hello **recommandations** vignette. Centre de sécurité analyse régulièrement l’état de la sécurité de vos ressources Azure hello. Lorsque le centre de sécurité identifie les éventuelles failles de sécurité, il affiche des recommandations sur hello **recommandations** panneau.
   ![Recommandations dans Azure Security Center][5]
2. Sélectionnez une recommandation sur hello **recommandations** émettre de panneau tooview plus hello tooresolve action informations et/ou tootake.

### <a name="view-hello-security-state-of-your-resources"></a>Afficher l’état de la sécurité de vos ressources hello
1. Retourner toohello **centre de sécurité** panneau. Hello **prévention** section du tableau de bord hello contient des indicateurs d’état de sécurité hello pour les ordinateurs virtuels, mise en réseau, les données et les applications.
2. Sélectionnez **de calcul** tooview plus d’informations. Hello **de calcul** panneau s’ouvre affichant trois onglets :

  - **Vue d’ensemble** : contient des recommandations relatives aux machines virtuelles et au monitoring.
  - **Machines virtuelles** : répertorie toutes les machines virtuelles et les informations relatives à l’intégrité de leur sécurité.
  - **Services cloud** : liste les rôles web et de travail contrôlés par Security Center.

    ![vignette de l’intégrité des ressources Hello dans le centre de sécurité Azure][6]

3. Sur hello **vue d’ensemble** , sélectionnez une recommandation sous **recommandations de MACHINES virtuelles** tooview plus d’informations ou take action tooconfigure contrôles nécessaires.
4. Sur hello **virtuels** onglet, sélectionnez une machine virtuelle tooview les détails supplémentaires.

### <a name="view-security-alerts"></a>Afficher les alertes de sécurité
1. Retourner toohello **centre de sécurité** panneau et sélectionnez hello **alertes de sécurité** vignette. Hello **alertes de sécurité** panneau s’ouvre et affiche la liste des alertes. Hello analyse du centre de sécurité de vos journaux de sécurité et l’activité réseau génère ces alertes. Des alertes de solutions de partenaires intégrées sont incluses.
   ![Alertes de sécurité dans le Centre de sécurité Azure][7]

   > [!NOTE]
   > Alertes de sécurité sont disponibles uniquement si le niveau Standard hello du centre de sécurité est activé. Une version d’évaluation gratuite de 60 jours de niveau Standard de hello n’est disponible. Consultez [étapes](#next-steps) pour plus d’informations sur la façon dont tooget hello Standard de niveau.
   >
   >
2. Sélectionnez une alerte tooview des informations supplémentaires. Dans cet exemple, nous sélectionnons **Fichier binaire système modifié détecté**. Les panneaux qui fournissent des détails supplémentaires sur l’alerte de hello s’ouvre.
   ![Détails des alertes de sécurité dans Azure Security Center][8]

### <a name="view-hello-health-of-your-partner-solutions"></a>Afficher l’intégrité de hello de vos solutions de partenaire
1. Retourner toohello **centre de sécurité** panneau. Hello **solutions de partenaire** vignette vous permet de contrôler, un coup de œil, hello état d’intégrité de vos solutions de partenaire intégré à votre abonnement Azure.
2. Sélectionnez hello **solutions de partenaire** vignette. Un panneau s’ouvre et affiche une liste de vos solutions de partenaire connecté tooSecurity Center.
   ![solutions de partenaires][9]
3. Sélectionnez une solution de partenaire. Dans cet exemple, nous allons sélectionner hello **QualysVa1** solution.  Un panneau s’ouvre et affiche l’état hello des solutions de partenaire hello et la solution hello les ressources associées. Sélectionnez **console de la Solution** expérience de gestion des partenaires tooopen hello pour cette solution.

## <a name="next-steps"></a>Étapes suivantes
Cet article introduit toohello analyse et la stratégie de gestion des composants de sécurité du centre de sécurité. Maintenant que vous êtes familiarisé avec le centre de sécurité, essayez hello comme suit :

* Configurez une stratégie de sécurité pour votre abonnement Azure. toolearn, voir [définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md).
* Utilisez les recommandations hello dans le centre de sécurité toohelp vous protégez vos ressources Azure. toolearn, voir [gestion des recommandations de sécurité dans le centre de sécurité Azure](security-center-recommendations.md).
* Passez en revue et gérez vos alertes de sécurité actuelles. toolearn, voir [toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md).
- [Sécurité des données Azure Security Center](security-center-data-security.md) : découvrez comment les données sont gérées et protégées dans Security Center.
* En savoir plus sur hello [advanced threat des fonctionnalités de détection](security-center-detection-capabilities.md) fournies avec hello [niveau Standard](security-center-pricing.md) du centre de sécurité. niveau Standard de Hello est disponible gratuitement pour hello 60 premiers jours.
* Si vous avez des questions sur l’utilisation du centre de sécurité, consultez hello [le Forum aux questions sur Azure Security Center](security-center-faq.md).

<!--Image references-->
[1]: ./media/security-center-get-started/azure-menu.png
[2]: ./media/security-center-get-started/security-center-pin.png
[3]: ./media/security-center-get-started/security-policy.png
[4]: ./media/security-center-get-started/prevention-policy.png
[5]: ./media/security-center-get-started/recommendations.png
[6]: ./media/security-center-get-started/resources-health.png
[7]: ./media/security-center-get-started/security-alert.png
[8]: ./media/security-center-get-started/security-alert-detail.png
[9]: ./media/security-center-get-started/partner-solutions.png
[10]: ./media/security-center-get-started/welcome.png
