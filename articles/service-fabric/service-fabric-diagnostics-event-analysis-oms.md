---
title: "aaaAzure analyse des événements Service Fabric avec OMS | Documents Microsoft"
description: "Découvrez l’analyse et la visualisation d’événements à l’aide d’OMS pour la surveillance et le diagnostic de clusters Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 526519293e70982c95e31241465b87f190096f74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-oms"></a>Analyse et visualisation d’événements avec OMS

Operations Management Suite (OMS) est une collection de services de gestion qui vous aident à la surveillance et de diagnostic pour les applications et les services hébergés dans le cloud de hello. tooget une vue plus détaillée d’OMS et elle offre, lisez [What ' s OMS ?](../operations-management-suite/operations-management-suite-overview.md)

## <a name="log-analytics-and-hello-oms-workspace"></a>Ouvrez une session Analytique et hello espace de travail OMS

Log Analytics collecte des données à partir de ressources gérées, notamment un agent ou une table de stockage Azure, et les conserve dans un référentiel central. les données de salutation peuvent ensuite être utilisé pour l’analyse, la génération d’alertes et la visualisation ou davantage d’exportation. Log Analytics prend en charge les événements, les données de performances ou toute autre donnée personnalisée.

Lors de la configuration d’OMS, vous aurez accès tooa spécifiques *espace de travail OMS*, à partir d’où les données peuvent être interrogées ou affichées dans les tableaux de bord.

Une fois que les données reçues par Analytique de journal, OMS dispose de plusieurs *Solutions de gestion* qui sont des solutions préconfigurées toomonitor les données entrantes, les scénarios tooseveral personnalisé. Ceux-ci incluent un *Service Fabric Analytique* solution et un *conteneurs* solution hello celles les plus pertinents deux toodiagnostics et analyse lors de l’utilisation des clusters Service Fabric. Il existe plusieurs autres qui méritent d’exploration et permet également de OMS pour créer des solutions personnalisées, vous pouvez en savoir plus sur hello [ici](../operations-management-suite/operations-management-suite-solutions.md). Chaque solution que vous choisissez toouse pour un cluster est configuré dans hello même espace de travail OMS, en même temps que le journal Analytique. Autoriser les espaces de travail pour les tableaux de bord personnalisés et de visualisation des données, et les modifications toohello données toocollect, traiter et analyser.

## <a name="setting-up-an-oms-workspace-with-hello-service-fabric-solution"></a>Configuration d’un espace de travail OMS avec hello Solution d’infrastructure de Service

Il est recommandé que vous incluez hello Solution d’infrastructure de Service dans votre espace de travail OMS, car il fournit un tableau de bord utile qui affiche hello différents canaux de journal entrants à partir de niveau de plate-forme et l’application hello et hello, tooquery en mesure de l’infrastructure de Service spécifique journaux. Voici une Solution de l’infrastructure de Service relativement simple aspect, avec une seule application sur hello cluster :

![Solution SF OMS](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-solution.png)

Il existe deux façons tooprovision et configurer un espace de travail OMS, via un modèle de gestionnaire de ressources ou directement à partir d’Azure Marketplace. Utilisez les ancienne hello lorsque vous déployez un cluster et hello ce dernier si vous disposez déjà d’un cluster déployé avec Diagnostics est activée.

### <a name="deploying-oms-using-a-resource-management-template"></a>Déploiement d’OMS à l’aide du modèle Resource Management

Cela se produit au stade de la création de cluster hello - lorsque le déploiement d’un cluster à l’aide d’un modèle de gestionnaire de ressources, le modèle de hello peut permet également de créer un nouvel espace de travail OMS, ajouter hello Service Fabric Solution tooit et le configurer tooread des données à partir du stockage approprié de hello tables.

>[!NOTE]
>Pour cette toowork, Diagnostics a toobe activé pour tooexist de tables de stockage Azure hello pour OMS / Analytique de journal tooread plus d’informations dans à partir de.

Vous trouverez [ici](https://azure.microsoft.com/resources/templates/service-fabric-oms/) un exemple de modèle que vous pouvez utiliser et modifier conformément à l’exigence, et qui effectue les actions mentionnées ci-dessus. Dans le cas de hello que vous souhaitez que le caractère facultatif de plus, il existe quelques autres modèles qui vous donnent les différentes options, selon où les processus hello, vous pouvez être de la configuration d’un espace de travail OMS - qu’ils sont accessibles à [Service Fabric et OMS modèles](https://azure.microsoft.com/resources/templates/?term=service+fabric+OMS).

### <a name="deploying-oms-using-through-azure-marketplace"></a>Déploiement d’OMS à l’aide de la Place de marché Azure

Si vous préférez tooadd un espace de travail OMS après avoir déployé un cluster, rendez-vous sur tooAzure Marketplace et recherchez *« Analytique de l’infrastructure de Service »*. Il ne doit exister qu’une ressource qui s’affiche, dans la catégorie de « Analyse + gestion » hello, illustré ci-dessous :

![SF Analytics OMS dans la Place de marché](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-analytics.png)

Si vous cliquez sur **Créer**, vous devez spécifier un espace de travail OMS. Cliquez sur **Sélectionner un espace de travail**, puis sur **Créer un espace de travail**. Remplir les entrées de hello requis : hello seule condition requise ici est qu’abonnement hello pourquoi l’infrastructure de Service de cluster et hello espace de travail OMS doit être hello identiques. Une fois vos entrées validées, votre espace de travail OMS est déployé en quelques minutes. Pendant qu’il termine le déploiement, la création de hello du Panneau de solution de Service Fabric hello toujours reste ouverte. Vérifiez que hello même espace de travail s’affiche sous *espace de travail OMS* puis appuyez sur **créer** au bas de hello, tooadd hello toohello espace de travail solution Service Fabric.

## <a name="using-hello-oms-agent"></a>À l’aide de hello Agent OMS

Il est recommandé de toouse EventFlow et diagnostics Windows AZURE en tant que solutions d’agrégation, car elles permettent une toodiagnostics approche modulaire plus et l’analyse. Par exemple, si vous souhaitez toochange votre sorties à partir de EventFlow, il ne requiert aucune instrumentation réel tooyour modification, simplement un fichier de configuration tooyour modification simple. Si, toutefois, vous décidez de tooinvest à l’aide d’OMS et acceptez l’utiliser pour l’analyse des événements de toocontinue (n’a pas toobe hello uniquement de la plateforme que vous utilisez, mais plutôt qu’elle sera au moins une des plateformes de hello), nous recommandons que vous explorez configuration hello [</C0>agentOMS<spanclass="notranslate">](../log-analytics/log-analytics-windows-agents.md).</span> Vous devez également utiliser l’agent OMS de hello lors du déploiement de cluster tooyour de conteneurs, comme indiqué ci-dessous.

processus Hello pour cette opération est relativement simple, étant donné que vous suffit de l’agent de hello tooadd comme modèle de gestionnaire de ressources tooyour extension, une échelle de machines virtuelles s’assurer qu’il est installé sur chacun des nœuds de votre. Vous trouverez un exemple de modèle de gestionnaire de ressources qui déploie l’espace de travail OMS hello avec hello solution d’infrastructure de Service (comme ci-dessus) et ajoute des nœuds de tooyour agent hello pour les clusters exécutant [Windows](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Windows) ou [Linux](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Linux).

avantages Hello sont les suivants de hello :

* Données plus complètes sur le côté de compteurs et les métriques de performances hello
* Tooconfigure facilement les données collectées à partir de hello de cluster et apporter des modifications tooit sans avoir à redéployer vos applications ou cluster hello, étant donné que modifie les paramètres de l’agent de hello toohello peuvent être effectuées à partir de l’espace de travail OMS hello et seront uniquement réinitialiser l’agent de hello automatiquement. tooconfigure hello OMS agent toopick des compteurs de performance spécifiques, espace de travail accédez toohello **Accueil > Paramètres > données > compteurs de Performance Windows** et extraire les données hello vous aimeriez toosee collectée
* Données s’affiche plus rapidement que son toobe stockée avant d’être récupéré par OMS / Analytique de journal
* La surveillance des conteneurs est beaucoup plus facile, car elle peut sélectionner les journaux Docker (stdout, stderror) et les statistiques (indicateurs de performance au niveau des conteneurs et des nœuds).

Hello principal ici est que dans la mesure où il s’agit d’un agent, il sera déployé sur votre cluster en même temps que toutes vos applications, il y aura des performances de toohello un impact minimal de vos applications sur un cluster de hello.

## <a name="monitoring-containers"></a>Surveillance des conteneurs

Lorsque vous déployez un cluster de conteneurs tooa Service Fabric, il est recommandé que hello cluster a été configuré avec l’agent OMS de hello et que cette solution de conteneurs hello a été ajoutée tooenable d’espace de travail OMS tooyour analyse et de diagnostics. Voici les conteneurs hello solution ressemble à un espace de travail :

![Tableau de bord OMS de base](./media/service-fabric-diagnostics-event-analysis-oms/oms-containers-dashboard.png)

l’agent de Hello Active la collecte de hello de plusieurs journaux spécifiques des conteneurs qui peuvent être interrogées dans OMS ou utilisé toovisualized des indicateurs de performance. types de journaux Hello collectés sont :

* ContainerInventory : affiche des informations sur les images, le nom et l’emplacement du conteneur
* ContainerImageInventory : informations sur les images déployées, ID ou tailles compris
* ContainerLog : journaux d’erreurs spécifiques, journaux de docker (stdout, etc.) et autres entrées
* ContainerServiceLog : les commandes de démon docker qui ont été exécutées
* Performances : les compteurs de performances, y compris le conteneur de processeur, mémoire, le trafic réseau, les e/s disque et des mesures personnalisées à partir de hello hébergent des ordinateurs

Cet article traite des tooset requis de hello étapes d’analyse pour votre cluster de conteneur. toolearn plus d’informations sur les solutions de conteneurs d’OMS, consultez leurs [documentation](../log-analytics/log-analytics-containers.md).

tooset des hello solution conteneur dans votre espace de travail, assurez-vous que vous avez hello OMS agent est déployé sur les nœuds de votre cluster en suivant les étapes de hello mentionnés ci-dessus. Une fois que le cluster de hello est prêt, déployez un tooit du conteneur. N’oubliez pas que hello première fois une image de conteneur est déployé tooa cluster, il accepte plusieurs images de hello toodownload minutes en fonction de sa taille.

Dans Azure Marketplace, recherchez *conteneurs* et créez une ressource de conteneurs (sous hello analyse + gestion catégorie).

![Ajout de la solution Conteneurs](./media/service-fabric-diagnostics-event-analysis-oms/containers-solution.png)

À l’étape de la création de hello, il demande un espace de travail OMS. Sélectionnez hello qui a été créé avec un déploiement hello ci-dessus. Cette étape ajoute une solution de conteneurs au sein de votre espace de travail OMS et est automatiquement détectée par l’agent OMS de hello déployé par le modèle de hello. démarre l’agent de Hello collecte des données sur les processus de conteneurs hello dans hello cluster et moins de 15 minutes ou par conséquent, vous devez voir solution hello allument avec des données, comme image hello du tableau de bord hello ci-dessus.


## <a name="next-steps"></a>Étapes suivantes

Explorer hello suivant toocustomize d’outils et les options OMS qu'a besoin d’un espace de travail tooyour :

* Pour les clusters sur site, OMS offre une passerelle qui peut être utilisé toosend données tooOMS (transférer Proxy HTTP). En savoir plus sur ce [connexion des ordinateurs sans tooOMS de l’accès Internet à l’aide de hello OMS passerelle](../log-analytics/log-analytics-oms-gateway.md)
* Configurer OMS tooset [automatisée d’alerte](../log-analytics/log-analytics-alerts.md) tooaid détecter et de diagnostics
* Obtenir être familiarisé avec hello [recherche et interrogation de journal](../log-analytics/log-analytics-log-searches.md) fonctionnalités proposées dans le cadre de l’Analytique des journaux
