---
title: "aaaMicrosoft l’utilisation d’Azure et RateCard API activer Cloudyn tooProvide ITFM pour les clients | Documents Microsoft"
description: "Fournit une perspective unique à partir de la facturation Microsoft Azure partenaire Cloudyn, sur leurs expériences intégration hello API de facturation Azure dans leurs produits.  Ces informations sont particulièrement utiles pour les clients Azure et Cloudyn qui souhaitent utiliser ou essayer les services Cloudyn pour Azure."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: f1397397-7e92-4c20-9862-ab6b93afefb7
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: e221ac8b8feebb725a1cc669c8143ab829621a8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-usage-and-ratecard-apis-enable-cloudyn-tooprovide-itfm-for-customers"></a>L’utilisation de Microsoft Azure et RateCard API activer Cloudyn tooProvide ITFM pour les clients
Cloudyn, un partenaire de développement Microsoft et des principaux fournisseurs de fonctionnalités de gestion de cloud, a été choisi pour une version préliminaire privée hello nouvelle RateCard APIs et l’utilisation des ressources Microsoft Azure.  Hello API d’utilisation fournit des données de consommation Azure de tooestimated accès pour un abonnement. Hello RateCard API fournit des informations de tarification complètes de tous les services Windows Azure, pour les clients non - Enterprise accord EA. Lorsqu’elles sont intégrées conjointement, ces API offrent une base d’informations complète pouvant servir de données d’entrée pour les outils de gestion financière informatique (ITFM), tels que ceux fournis par Cloudyn.

## <a name="introduction"></a>Introduction
Hello dite « multiplication » de données à partir de hello API d’utilisation avec des données à partir de hello RateCard API (prix de l’utilisation [unités] [$unit] = d’utilisation détaillées et de coût) crée hello plus granulaire, précis et fiable informations de facturation disponibles pour Azure aujourd'hui.

![Vue d’ensemble de la gestion financière informatique][1]

Utilisation de ces API fournit des informations clés sur l’utilisation des clients et les coûts, permettant aux comptes de Cloudyn tooanalyze client dans une façon simple et par programmation, tooperform diverses tâches ITFM pour ses clients.

## <a name="integrating-cloudyn-with-hello-ratecard-and-usage-apis"></a>Intégration Cloudyn avec hello RateCard et utilisation d’API
Hello RateCard API nécessite plusieurs paramètres d’entrée, tels que les informations de région, devise et paramètres régionaux--mais hello plus important qu’un est OfferDurableID, qui spécifie le type hello du client de hello offre Azure utilise (paiement à l’utilisation, hérité 6 et 12 mois à l’engagement les plans, MSDN offre, MPN offres promotionnelles et autres). Hello OfferDurableID se trouvent dans hello [l’utilisation d’Azure et du portail de facturation](https://account.windowsazure.com/Subscriptions), sous hello « ID d’offre « pourquoi l’abonnement indiqué.

Lors de l’enregistrement pour [Cloudyn pour Azure](https://www.cloudyn.com/microsoft-azure/) services, les clients peuvent ajouter leur code OfferDurableID, ce qui permet de Cloudyn toopull les informations de tarification appropriées via hello RateCard API.  Trouver des informations sur les différents types de hello d’offres peuvent un hello [détails de l’offre Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) page.

![Vue d’ensemble du moteur de gestion financière informatique Cloudyn][2]

Utilise Cloudyn que deux hello RateCard APIs et l’utilisation dans Ajout toohello API de performances de site Azure, toocreate des couches supplémentaires de visualisation, analytique, alertes, reporting, coût de gestion et conseils, en fournissant des clients Azure fiable outil d’ITFM cloud.

## <a name="cloudyn-itfm-use-cases-enabled-by-usage-and-ratecard-api-integration"></a>Cas d’utilisation ITFM Cloudyn autorisés par l’intégration des API Usage et RateCard
Les cas d’utilisation ITFM Cloudyn courants qui sont autorisés par l’intégration des API Usage et RateCard sont les suivants :

* **Analyse du coût des** -permet de cloud coûte toobe ventilée tooany natif identifiant la dimension (fournisseur, service, compte, région, etc.). Hello l’utilisation d’Azure et RateCard APIs transformer en une tâche facile, en fournissant la décomposition des hello plus granulaire des données d’utilisation et de coût par compte, qui est ensuite regroupée et filtré par Cloudyn présentée toohello utilisateur, sous forme de graphique ou tabulaire.

![Graphique en secteurs de l’analyse des coûts][3]

* **Coût d’Allocation 360** -Active finance et hello de toouncover de responsables informatique réel coûtent de répartition, les pilotes et les tendances de leur déploiement dans le cloud. Il permet plus aux responsables tooeasily les frais de déploiement associés avec des unités commerciales, les services, les régions et plus d’informations, en fournissant des analyses normalisés dans les coûts de nuage et de faciliter les rétrofacturations d’entreprise et showbacks. Hello l’utilisation d’Azure et RateCard APIs servent coût d’allocation moteur d’entrée tooCloudyn, qui complète hello API en définissant des méthodes et logique métier pour allouer les ressources non marquées ou untaggable.

![Graphique à 360° de l’affectation des coûts][4]

* **Rentabilité** -fournit des recommandations de redimensionnement pour les machines virtuelles sous-utilisées, ce qui réduit les dépenses hello client sur les ordinateurs dépassant ou surconfigurés. Pour ce faire, Cloudyn examine les métriques d’unité centrale et de RAM des machines virtuelles (par le biais de l’API Performance), les heures d’exécution (à l’aide de l’API Usage) et les coûts (au moyen de l’API RateCard). Cloudyn fournit des recommandations de redimensionnement en fonction des ressources du processeur ou mémoire vive sous-utilisés (performances), puis calcule les économies estimées en multipliant le delta de prix hello (RateCard) entre les machines virtuelles de hello en hello heure-utilisation réelle (utilisation) de hello ordinateur sous-exploités.

![Redimensionnement rentable][5]

* **Recommandations en matière de portage de cloud** : fournit des conseils d’ordre financier sur le portage de cloud. Il examine les coûts actuels de l’utilisateur de ressources de cloud qui sont déployés sur les fournisseurs de cloud principal et il compare le coût toohello du déploiement d’un équivalent sur Azure. Il fournit ensuite granulaire par ressources, financièrement basée portage tooAzure de recommandations. Après avoir évalué les déploiement équivalent hello requis sur Azure (basé sur les préférences utilisateur et les mesures de performances), Cloudyn utilise le coût de hello tooevaluate hello RateCard API de déploiement d’équivalent hello sur Azure.
* **Les rapports de performances** -activé par l’API des performances d’Azure, ces rapports fournissent un ensemble de fonctionnalités à partir de l’utilisation du processeur et mémoire RAM toooptimization recommandations. Voici un exemple de rapport sur l’utilisation des instances, qui présente une répartition des instances par utilisation moyenne de l’unité centrale.

![Rapports de performances][6]

* **Gestionnaire des catégories** -une fonctionnalité puissante de Cloudyn qui apporte de ressources de cloud toounorganized l’ordre. Il fournit des utilisateurs hello liberté toocreate leurs propres catégories uniques (tags) de mesure et de création de rapports qui est conformément aux pratiques efficaces. En outre, les utilisateurs peuvent facilement réguler et catégoriser le balisage incohérent (fautes de frappe et autres anomalies) et détecter automatiquement les ressources non balisées afin de garantir la précision de l’affectation des coûts.

![Gestionnaire de catégories][7]

## <a name="video"></a>Vidéo
Voici une courte vidéo qui montre comment un client Azure permettre utiliser Cloudyn pour Azure et hello API de facturation Azure, insights toogain à partir de leurs données de consommation de Azure.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Cloudyn-Provides-Cloud-ITFM-Tools-Via-Microsoft-Azure-APIs/player]
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* Démarrer un libre [Cloudyn pour Azure](https://www.cloudyn.com/microsoft-azure/) toosee d’évaluation, l’obtention de coût transparence des rapports personnalisés et analytique pour votre déploiement de cloud de Microsoft Azure.
* Consultez [obtenir votre consommation de ressources Microsoft Azure](billing-usage-rate-card-overview.md) pour une vue d’ensemble de l’utilisation des ressources Azure de hello et RateCard APIs.
* Extraire hello [référence d’API REST de facturation Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) pour plus d’informations sur les deux API qui font partie de jeu hello des API fournies par hello Azure Resource Manager.
* Si vous souhaitez que toodive directement dans l’exemple de code hello, découvrez nos exemples de Code API de facturation Microsoft Azure sur [exemples de Code Azure](https://azure.microsoft.com/documentation/samples/?term=billing).

## <a name="learn-more"></a>En savoir plus
* toolearn en savoir plus sur les offres de contrat d’entreprise de Microsoft Azure (EA), visitez [Azure de gestionnaire de licences pour hello entreprise](https://azure.microsoft.com/pricing/enterprise-agreement/)
* Consultez hello [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md) toolearn article plus hello Azure Resource Manager.
* Pour plus d’informations sur suite hello d’outils toohelp nécessaire dans la compréhension du cloud dépenses, reportez-vous trop Gartner article [Guide de marché pour les outils de l’informatique financières Management (ITFM)](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

<!--Image references-->
[1]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Overview.png
[2]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Engine-Overview.png
[3]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Analysis-Pie-Chart.png
[4]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Allocation-360-Chart.png
[5]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Effective-Sizing.png
[6]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Performance-Reports.png
[7]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Category-Manager.png
