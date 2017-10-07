---
title: "aaaOverview de métriques dans Microsoft Azure | Documents Microsoft"
description: "Vue d’ensemble des mesures et de leur utilisation dans Microsoft Azure"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 405ec51c-0946-4ec9-b535-60f65c4a5bd1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: johnkem
ms.openlocfilehash: 2b97f51e0554dae95a929241ae1f0e25e5c215ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Vue d’ensemble des mesures dans Microsoft Azure
Cet article décrit les mesures dans Microsoft Azure, leurs avantages et comment toostart leur utilisation.  

## <a name="what-are-metrics"></a>Quelles sont les mesures ?
Moniteur de Azure vous permet de tooconsume télémétrie toogain visibilité des performances de hello et de l’intégrité de vos charges de travail sur Azure. type le plus important de données de télémétrie Azure Hello est métriques hello (également appelés des compteurs de performances) est émis par les ressources Azure plus. Moniteur de Azure fournit plusieurs façons tooconfigure et consomment ces mesures de surveillance et de dépannage.

## <a name="what-can-you-do-with-metrics"></a>Que pouvez-vous faire avec les mesures ?
Métriques sont une source précieuse de télémétrie et vous hello toodo tâches suivantes :

* **Suivre les performances de hello** de votre ressource (par exemple, une application virtuelle, site Web ou logique) en traçant ses mesures sur un graphique de portail et l’épinglage de ce tableau de bord tooa graphique.
* **Soyez averti d’un problème** qu’impacts hello les performances de votre ressource lorsqu’une métrique dépasse un certain seuil.
* **Configurer des actions automatisées**, telles que la mise à l’échelle automatique d’une ressource ou le déclenchement d’un runbook lorsqu’une mesure dépasse un certain seuil.
* **Effectuer des analyses avancées** ou créer des rapports sur les tendances de performances ou d’utilisation de vos ressources.
* **Archive** hello l’historique des performances ou l’intégrité de votre ressource **pour la conformité ou de l’audit** à des fins.

## <a name="what-are-hello-characteristics-of-metrics"></a>Quelles sont les caractéristiques de hello de métriques ?
Mesures ont hello suivant caractéristiques :

* Toutes les mesures ont **une fréquence d’une minute**. Vous recevez une valeur métrique de toutes les minutes à partir de votre ressource, pratiquement visibilité en temps réel dans l’état de hello et l’intégrité de votre ressource.
* Les mesures sont **disponibles immédiatement**. Vous ne devez tooopt dans ou configurer les diagnostics supplémentaires.
* Vous pouvez accéder à **30 jours d’historique** pour chaque mesure. Vous pouvez rapidement consulter hello récente et mensuelles les tendances des performances de hello ou l’intégrité de votre ressource.

Vous pouvez également :

* Configurer une métrique **alerte action automatisée de règle qui envoie une notification ou prend** lorsque métrique de hello dépasse le seuil hello que vous avez définie. Mise à l’échelle est une action automatisée spéciale qui permet de vous tooscale les requêtes entrantes de toomeet votre ressource ou la charge sur votre site Web ou les ressources informatiques. Vous pouvez configurer un paramètre de règle tooscale ou selon une mesure de dépasser un seuil d’échelle automatique.

* **Itinéraire** tous les analytique instantanée tooenable métriques Application Insights ou Analytique des journaux (OMS), la recherche et la génération d’alertes personnalisées sur les données de métriques de vos ressources. Vous pouvez également transmettre en continu métriques tooan concentrateur d’événements, ce qui vous toothen d’acheminer les tooAzure Analytique de flux de données ou les applications toocustom pour l’analyse de quasiment en temps réel. Vous pouvez paramétrer la diffusion vers un hub d’événements à l’aide des paramètres de diagnostic.

* **Archiver les métriques toostorage** pour la conservation à longue terme ou les utiliser pour la création de rapports en mode hors connexion. Vous pouvez acheminer votre tooAzure métriques stockage d’objets Blob lorsque vous configurez les paramètres de diagnostic pour votre ressource.

* Découvrir facilement, l’accès, et **afficher toutes les métriques** via le portail Azure lorsque vous sélectionnez une ressource et tracer les métriques hello sur un graphique de hello.

* **Consommer** métriques hello via hello nouvelles API REST d’analyse Azure.

* **Requête** mesures à l’aide de hello applets de commande PowerShell ou hello Cross-Platform REST API.

  ![Acheminement des mesures dans Azure Monitor](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-hello-portal"></a>Accéder aux métriques via le portail de hello
Voici un bref aperçu de comment toocreate un graphique de mesure à l’aide de hello portail Azure.

### <a name="tooview-metrics-after-creating-a-resource"></a>métriques de tooview après la création d’une ressource
1. Ouvrez hello portail Azure.
2. Créez un site Azure App Service.
3. Après avoir créé un site Web, accédez à toohello **vue d’ensemble** panneau du site Web de hello.
4. Vous pouvez afficher les nouvelles mesures sous forme de vignette **Surveillance**. Vous pouvez ensuite modifier hello vignette et sélectionner des mesures plus.

   ![Mesures sur une ressource dans Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="tooaccess-all-metrics-in-a-single-place"></a>tooaccess toutes les métriques dans un emplacement unique
1. Ouvrez hello portail Azure.
2. Accédez toohello nouvelle **moniteur** onglet et puis et sélectionnez hello **métriques** option situés sous celui-ci.
3. Sélectionnez votre abonnement, le groupe de ressources et le nom hello de ressource de hello à partir de la liste déroulante de hello.
4. Afficher la liste des mesures disponibles hello. Sélectionnez ensuite la métrique hello vous intéressez et tracez.
5. Vous pouvez épingler toohello le tableau de bord en cliquant sur le code confidentiel de hello sur le coin supérieur droit de hello.

   ![Accéder à toutes les mesures dans Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> Vous pouvez accéder aux mesures à partir de machines virtuelles (basées sur Azure Resource Manager) et aux groupes de machines virtuelles identiques sans aucune installation de diagnostic supplémentaire. Ces nouvelles mesures au niveau hôte sont disponibles pour les instances Windows et Linux. Ces mesures ne sont pas toobe confondue avec hello métriques au niveau du système d’exploitation invité que vous avez toowhen access que vous activez les Diagnostics de Azure sur vos machines virtuelles ou les machines virtuelles identiques. toolearn savoir plus sur la configuration des Diagnostics, consultez [Nouveautés de Microsoft Azure Diagnostics](../azure-diagnostics.md).
>
>

## <a name="access-metrics-via-hello-rest-api"></a>Accéder aux métriques via l’API REST de hello
Métriques Azure est accessible via hello API d’analyse Azure. Il existe deux API qui vous aident à découvrir et accéder aux mesures :

* Hello d’utilisation [définitions de métrique d’analyse Azure API REST](https://msdn.microsoft.com/library/mt743621.aspx) tooaccess hello la liste des métriques qui sont disponibles pour un service.
* Hello d’utilisation [API REST de Azure moniteur métriques](https://msdn.microsoft.com/library/mt743622.aspx) tooaccess hello des données de métriques réel.

> [!NOTE]
> Cet article traite des métriques hello via hello [nouvelle API pour les mesures](https://msdn.microsoft.com/library/dn931930.aspx) pour les ressources Azure. version de l’API Hello pour les définitions métriques nouvelle API hello est 2016-03-01 et version hello pour les métriques API est 2016-09-01. métriques et des définitions de métrique hérité hello est accessible par hello API version 2014-04-01.
>
>

Pour une procédure pas à pas plus détaillées à l’aide de hello API REST de moniteur Azure, consultez [API REST de Azure moniteur procédure pas à pas](monitoring-rest-api-walkthrough.md).

## <a name="export-metrics"></a>Exporter mesures
Vous pouvez accéder toohello **paramètres de diagnostic** panneau sous hello **moniteur** options d’exportation hello onglet et d’affichage pour les mesures. Vous pouvez sélectionner des mesures (et les journaux de diagnostic) toobe routé tooBlob stockage, les concentrateurs d’événements tooAzure ou tooOMS pour les scénarios d’utilisation qui ont été mentionnés précédemment dans cet article.

 ![Options d’exportation pour les mesures dans Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview3.png)

Vous pouvez configurer cela au moyen de modèles Resource Manager, de [PowerShell](insights-powershell-samples.md), de [l’interface de ligne de commande Azure](insights-cli-samples.md) ou des [API REST](https://msdn.microsoft.com/library/dn931943.aspx).

## <a name="take-action-on-metrics"></a>Effectuer une opération sur les mesures
les notifications tooreceive ou entreprendre automatisée des actions sur les données de mesure, vous pouvez configurer des règles d’alerte ou des paramètres de mise à l’échelle.

### <a name="configure-alert-rules"></a>Configuration des règles d'alerte
Vous pouvez configurer des règles d’alerte sur les mesures. Ces règles d’alerte peuvent vérifier si une mesure a atteint un certain seuil. Ils peuvent ensuite être averti par courrier électronique ou déclencher un webhook qui peut être utilisé toorun tout script personnalisé. Vous pouvez également utiliser les intégrations d’un produit tiers tooconfigure hello webhook.

 ![Mesures et règles d’alerte dans Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a>Mise à l’échelle automatique de vos ressources Azure
Certaines ressources Azure prend en charge hello mise à l’échelle ou de plusieurs instances toohandle vos charges de travail. Mise à l’échelle s’applique tooApp Service (Web applications), machines virtuelles identiques et les Services de cloud computing Azure classique. Vous pouvez configurer tooscale de règles de mise à l’échelle ou lorsque certaine une mesure qui a un impact sur votre charge de travail dépasse un seuil que vous spécifiez. Pour plus d'informations, consultez la rubrique [Présentation de la mise à l’échelle automatique](monitoring-overview-autoscale.md).

 ![Mesures et règles de mise à l’échelle automatique dans Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a>Découvrez les services et mesures pris en charge
Azure Monitor est une nouvelle infrastructure de mesures. Il prend en charge hello suivant des services Azure Bonjour Azure portal et hello nouvelle version de hello API d’analyse Azure :

* Machines virtuelles (basées sur Azure Resource Manager)
* jeux de mise à l’échelle de machine virtuelle
* Batch
* Espace de noms Event Hubs
* Espace de noms Service Bus (référence SKU premium uniquement)
* SQL Database (version 12)
* Pool élastique SQL
* Sites web
* Batteries de serveurs web
* Logic Apps
* IoT Hubs
* Cache Redis
* Réseau : Passerelles d’application
* Search

Vous pouvez afficher une liste détaillée de tous les services hello pris en charge et leurs mesures au [métriques moniteur Azure--les mesures prises en charge par le type de ressource](monitoring-supported-metrics.md).

## <a name="next-steps"></a>Étapes suivantes
Consultez les liens toohello tout au long de cet article. De plus, consultez :  

* [Mesures courantes pour la mise à l’échelle automatique](insights-autoscale-common-metrics.md)
* [Comment les règles d’alerte toocreate](insights-alerts-portal.md)
* [Analyser les journaux du stockage Azure avec Log Analytics](../log-analytics/log-analytics-azure-storage.md)
