---
title: "Guide de démarrage rapide d’Azure Security Center | Microsoft Docs"
description: "Cet article vous aide à prendre rapidement en main Azure Security Center en vous guidant à travers les composants de surveillance de sécurité et de gestion des stratégies de sécurité et vers les étapes suivantes."
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
ms.openlocfilehash: 392c814b7d3ff6b4f0f7850a51960576775e0307
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-center-quick-start-guide"></a>Guide de démarrage rapide du Centre de sécurité Azure
Cet article vous aide à prendre rapidement en main Azure Security Center en vous guidant à travers les composants de surveillance de sécurité et de gestion des stratégies de sécurité d’Azure Security Center.

> [!NOTE]
> Depuis début juin 2017, Security Center utilise Microsoft Monitoring Agent pour collecter et stocker des données. Pour plus d’informations, consultez l’article [Migration de plateforme Azure Security Center](security-center-platform-migration.md). Les informations contenues dans cet article représentent les fonctionnalités de Security Center après la transition vers Microsoft Monitoring Agent.
>
>

## <a name="prerequisites"></a>Composants requis
Pour utiliser le Centre de sécurité, vous devez disposer d’un abonnement à Microsoft Azure. Si vous n’avez pas d’abonnement, vous pouvez vous inscrire pour avoir un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).

Le niveau Gratuit d’Azure Security Center est activé automatiquement avec votre abonnement et offre une visibilité de l’état de sécurité de vos ressources Azure. Il fournit une gestion des stratégies de sécurité de base, des recommandations de sécurité et une intégration avec les produits et services de sécurité des partenaires Azure.

Le Centre de sécurité est accessible à partir du [portail Azure](https://azure.microsoft.com/features/azure-portal/). Pour en savoir plus sur le portail Azure, consultez la [documentation relative au portail](https://azure.microsoft.com/documentation/services/azure-portal/).

## <a name="permissions"></a>Autorisations
Dans Security Center, vous ne voyez les informations relatives à une ressource Azure que lorsque vous avez reçu le rôle de propriétaire, de collaborateur ou de lecteur pour l’abonnement ou le groupe de ressources auquel appartient la ressource. Pour plus d’informations sur les rôles et les actions autorisées dans Security Center, consultez l’article [Permissions in Azure Security Center (Autorisations dans Azure Security Center)](security-center-permissions.md).

## <a name="data-collection"></a>Collecte des données
Azure Security Center collecte les données de vos machines virtuelles afin d’évaluer l’état de leur sécurité, de fournir des recommandations en matière de sécurité et de vous avertir des menaces. Lorsque vous accédez à Azure Security Center pour la première fois, la collecte de données est activée sur toutes les machines virtuelles de votre abonnement. Security Center approvisionne Microsoft Monitoring Agent sur toutes les machines virtuelles Azure prises en charge existantes et sur toutes celles nouvellement créées. Consultez [Activer la collecte de données](security-center-enable-data-collection.md) pour en savoir plus sur le fonctionnement de la collecte de données.

La collecte de données est recommandée. Si vous utilisez le niveau Gratuit de Security Center, vous pouvez désactiver la collecte de données sur les machines virtuelles dans la stratégie de sécurité. La collecte de données est obligatoire pour les abonnements Security Center du niveau Standard. Consultez [Tarification de Security Center](security-center-pricing.md) pour en savoir plus sur les niveaux tarifaires Gratuit et Standard.

Les étapes suivantes décrivent comment accéder aux composants d’Azure Security Center et les utiliser. Dans ces étapes, nous vous montrons comment désactiver la collecte des données si vous la refusez.

> [!NOTE]
> Cet article présente le service à l’aide d’un exemple de déploiement. Il ne s’agit pas d’un guide pas à pas.
>
>

## <a name="access-security-center"></a>Accéder au Centre de sécurité
Dans le portail, procédez comme suit pour accéder au Centre de sécurité :

1. Dans le menu **Microsoft Azure**, sélectionnez **Security Center**.

   ![Menu Azure][1]
2. Si vous accédez à Azure Security Center pour la première fois, le panneau **Bienvenue** s’ouvre. Sélectionnez **Lancer Security Center** pour ouvrir le panneau **Security Center** et activer la collecte des données.
   ![Écran d’accueil][10]
3. Après avoir démarré Azure Security Center à partir du panneau Bienvenue ou sélectionné Azure Security Center dans le menu Microsoft Azure, le panneau **Security Center** s’ouvre. Pour accéder facilement au panneau **Security Center** à l’avenir, sélectionnez l’option **Épingler le panneau au tableau de bord** (en haut à droite).
   ![Option Épingler le panneau au tableau de bord][2]

## <a name="use-security-center"></a>Utiliser le Centre de sécurité
Vous pouvez configurer des stratégies de sécurité pour vos groupes de ressources et abonnements Azure. Configurons une stratégie de sécurité pour votre abonnement :

1. Cliquez sur la mosaïque **Stratégie** dans le panneau **Security Center**.
2. Dans le panneau **Stratégie de sécurité - Définir la stratégie par abonnement**, sélectionnez un abonnement.
3. Dans le panneau **Stratégie de sécurité**, l’option **Collecte des données** est activée pour la collecte automatique des journaux. L’extension de la surveillance est approvisionnée sur toutes les machines virtuelles actuelles et nouvelles dans l’abonnement. (Dans le niveau Gratuit de Security Center, vous pouvez désactiver la collecte de données en définissant **Collecte des données** sur **Désactivée**. Le fait de **désactiver** la **collecte de données** empêche Security Center de vous fournir des recommandations et des alertes en matière de sécurité.)
4. Sur le panneau **Stratégie de sécurité**, sélectionnez **Stratégie de prévention**. Cette opération ouvre le panneau **Stratégie de prévention**.
5. Sur le panneau **Stratégie de prévention**, activez les recommandations que vous souhaitez voir dans le cadre de votre stratégie de sécurité. Exemples :

   * **L’activation** de l’option **Mises à jour du système** permet d’analyser toutes les machines virtuelles prises en charge pour y détecter des mises à jour de système d’exploitation manquantes.
   * **L’activation** de l’option **Vulnérabilités du système d’exploitation** permet d’analyser toutes les machines virtuelles prises en charge afin d’identifier toute configuration du système d’exploitation risquant de rendre la machine virtuelle plus vulnérable aux attaques.

### <a name="view-recommendations"></a>Afficher les recommandations
1. Retournez dans le panneau **Security Center** et sélectionnez la vignette **Recommandations**. Le Centre de sécurité analyse l’état de sécurité de vos ressources Azure à intervalles réguliers. Lorsque Security Center identifie des failles de sécurité potentielles, il affiche des recommandations sur le panneau **Recommandations**.
   ![Recommandations dans Azure Security Center][5]
2. Sélectionnez une recommandation sur le panneau **Recommandations** pour visualiser plus d’informations et/ou prendre des mesures afin de résoudre le problème.

### <a name="view-the-security-state-of-your-resources"></a>Afficher l’état de sécurité de vos ressources
1. Retournez au panneau **Centre de sécurité** . La section **Prévention** du tableau de bord contient des indicateurs de l’état de sécurité pour les machines virtuelles, la mise en réseau, les données et les applications.
2. Sélectionnez **Compute** pour afficher plus d’informations. Le panneau **Compute** s’ouvre affichant trois onglets :

  - **Vue d’ensemble** : contient des recommandations relatives aux machines virtuelles et au monitoring.
  - **Machines virtuelles** : répertorie toutes les machines virtuelles et les informations relatives à l’intégrité de leur sécurité.
  - **Services cloud** : liste les rôles web et de travail contrôlés par Security Center.

    ![La mosaïque d’intégrité des ressources dans le Centre de sécurité Azure][6]

3. Dans l’onglet **Vue d’ensemble**, sélectionnez une recommandation sous **RECOMMANDATIONS POUR MACHINES VIRTUELLES** afin d’afficher des informations supplémentaires et/ou de configurer les contrôles nécessaires.
4. Dans l’onglet **Machines virtuelles**, sélectionnez une machine virtuelle pour afficher des détails supplémentaires.

### <a name="view-security-alerts"></a>Afficher les alertes de sécurité
1. Retournez dans le panneau **Security Center** et sélectionnez la mosaïque **Alertes de sécurité**. Le panneau **Alertes de sécurité** s’ouvre et affiche la liste des alertes. Les alertes sont générées par l’analyse de vos journaux de sécurité et de l’activité réseau par Azure Security Center. Des alertes de solutions de partenaires intégrées sont incluses.
   ![Alertes de sécurité dans le Centre de sécurité Azure][7]

   > [!NOTE]
   > Les alertes de sécurité sont seulement disponibles si le niveau Standard d’Azure Security Center est activé. Un essai gratuit de 60 jours du niveau Standard est disponible. Pour plus d’informations sur la façon d’obtenir le niveau Standard, consultez [Étapes suivantes](#next-steps).
   >
   >
2. Sélectionnez une alerte pour afficher des informations supplémentaires. Dans cet exemple, nous sélectionnons **Fichier binaire système modifié détecté**. Les panneaux contenant des informations supplémentaires sur l’alerte s’ouvrent.
   ![Détails des alertes de sécurité dans Azure Security Center][8]

### <a name="view-the-health-of-your-partner-solutions"></a>Afficher l’intégrité de vos solutions de partenaires
1. Retournez au panneau **Centre de sécurité** . La mosaïque **Solutions de partenaires** permet de surveiller en un coup d’œil l’état d’intégrité de vos solutions de partenaires intégrées à votre abonnement Azure.
2. Sélectionnez la vignette **Solutions de partenaires** . Un panneau s’ouvre et affiche la liste de vos solutions de partenaires connectées à Azure Security Center.
   ![solutions de partenaires][9]
3. Sélectionnez une solution de partenaire. Dans cet exemple, sélectionnons la solution **QualysVa1**.  Un panneau s'ouvre et affiche l’état de la solution partenaire et des ressources associées à cette solution. Sélectionnez **Console de solution** afin d’ouvrir l’expérience de gestion du partenaire pour cette solution.

## <a name="next-steps"></a>Étapes suivantes
Cet article vous a présenté les composants de surveillance de sécurité et de gestion des stratégies de sécurité dans Azure Security Center. Maintenant que vous êtes familiarisé avec Azure Security Center, procédez comme suit :

* Configurez une stratégie de sécurité pour votre abonnement Azure. Pour en savoir plus, consultez [Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md).
* Suivez les recommandations d’Azure Security Center pour protéger vos ressources Azure. Pour en savoir plus, consultez [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md).
* Passez en revue et gérez vos alertes de sécurité actuelles. Pour en savoir plus, consultez [Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md).
- [Sécurité des données Azure Security Center](security-center-data-security.md) : découvrez comment les données sont gérées et protégées dans Security Center.
* Apprenez-en plus sur les [fonctionnalités avancées de détection des menaces](security-center-detection-capabilities.md) fournies avec le [niveau Standard](security-center-pricing.md) d’Azure Security Center. Le niveau Standard est gratuit les 60 premiers jours.
* Si vous avez des questions sur l’utilisation d’Azure Security Center, consultez le [FAQ d’Azure Security Center](security-center-faq.md).

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
