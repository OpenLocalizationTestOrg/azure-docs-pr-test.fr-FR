---
title: "aaaAssess des applications de Service Fabric à l’aide de l’Analytique de journal hello portail Azure | Documents Microsoft"
description: "Vous pouvez utiliser la solution de Service Fabric hello dans Analytique de journal à l’aide de risque de hello hello tooassess portail Azure et de l’intégrité de vos applications de Service Fabric, micro-services, les nœuds et les clusters."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a>Évaluer des applications de Service Fabric et micro-services avec hello portail Azure

> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](log-analytics-service-fabric-azure-resource-manager.md)
> * [PowerShell](log-analytics-service-fabric.md)
>
>

![Symbole Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

Cet article décrit comment toouse hello solution de l’infrastructure de Service dans le journal Analytique toohelp identifier et résoudre les problèmes sur votre cluster Service Fabric.

Hello solution d’infrastructure de Service utilise des données de Diagnostics Windows Azure à partir de vos machines virtuelles de l’infrastructure Service, collecte des données de vos tables WAD d’Azure. Log Analytics lit ensuite les événements d’infrastructure Service Fabric, notamment les **événements de service fiable**, les **événements d’acteurs**, les **événements opérationnels** et les **événements ETW personnalisés**. Avec hello solution du tableau de bord, vous êtes tooview en mesure de détecter les problèmes importants et les événements pertinents dans votre environnement de Service Fabric.

tooget solution de hello en main, vous devez tooconnect votre espace de travail Analytique des journaux de tooa cluster Service Fabric. Voici trois scénarios tooconsider :

1. Si vous n’avez pas déployé votre cluster Service Fabric, utilisez les étapes de hello dans ***déployer un espace de travail Analytique des journaux de Cluster Service Fabric connecté tooa*** toodeploy un nouveau cluster et de le configurer tooreport tooLog Analytique.
2. Si vous avez besoin des compteurs de performance toocollect à partir de votre toouse hôtes autres solutions OMS, telles que la sécurité sur votre Cluster Service Fabric, suivez les étapes de hello dans ***déployer un espace de travail Analytique des journaux de tooa Cluster Service Fabric connecté avec l’Extension de machine virtuelle installé.***
3. Si vous avez déjà déployé votre cluster Service Fabric et que vous souhaitez tooconnect il tooLog Analytique, suivez les étapes de hello dans ***Ajout d’un tooLog de compte de stockage existant Analytique.***

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a>Déployer un espace de travail de Cluster Service Fabric connecté tooa Analytique de journal.
Ce modèle hello suivant :

1. Déploie un espace de travail Azure Service Fabric cluster déjà connecté tooa Analytique de journal. Vous avez hello option toocreate d’un espace de travail lors du déploiement de modèle de hello, ou nom d’entrée hello d’espace de travail Analytique de journal déjà existant.
2. Ajoute un espace de travail hello le stockage des diagnostics compte toohello Analytique de journal.
3. Permet la solution de Service Fabric hello dans votre espace de travail Analytique de journal.

[![Déployer tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)

Une fois que vous sélectionnez hello déployer bouton ci-dessus, hello Azure portail s’ouvre et affiche les paramètres pour vous tooedit. Si vous entrez un nouveau nom d’espace de travail Analytique des journaux, être toocreate assurer un groupe de ressources :

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

Acceptez les conditions juridiques hello et cliquez sur **créer** déploiement de hello toostart. Une fois le déploiement de hello est terminé, vous devez voir le nouvel espace de travail hello et cluster créé et hello WADServiceFabric * WADETWEvent, WADWindowsEventLogs et événements tables ajoutées :

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a>Déployer un espace de travail de Cluster Service Fabric connecté tooa Analytique de journal avec l’Extension de machine virtuelle installé.

Ce modèle hello suivant :

1. Déploie un espace de travail Azure Service Fabric cluster déjà connecté tooa Analytique de journal. Vous pouvez créer un espace de travail ou utiliser un espace de travail existant.
2. Ajoute un espace de travail hello le stockage des diagnostics comptes toohello Analytique de journal.
3. Permet la solution de Service Fabric hello dans l’espace de travail hello Analytique de journal.
4. Installe l’extension de l’agent MMA hello dans l’échelle de chaque ordinateur virtuel défini dans votre cluster Service Fabric. Agent hello MMA est installé, vous êtes tooview en mesure de performances sur vos nœuds.

[![Déployer tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)

Suivant hello les mêmes étapes ci-dessus, les paramètres d’entrée hello nécessaires et déclencher un déploiement. Une fois encore, vous devez voir l’espace de travail hello, le cluster et tables WAD créés toutes les :

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a>Affichage des données de performances

tooview des données de performances à partir de vos nœuds :


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- Lancer l’espace de travail hello Analytique de journal à partir de hello portail Azure.
  ![Service Fabric](./media/log-analytics-service-fabric/6.png)
- Accédez tooSettings sur le volet gauche de hello, puis sélectionnez les données >> compteurs de Performance Windows >> « Ajouter hello sélectionné les compteurs de performance » : ![Service Fabric](./media/log-analytics-service-fabric/7.png)
- Dans la recherche de journal, utilisez hello suivant toodelve de requêtes dans les métriques clés sur vos nœuds :

    a. Comparaison hello utilisation moyenne du processeur sur tous les nœuds de votre dernière toosee une heure hello, les nœuds qui rencontrent des problèmes et à quel intervalle de temps, un nœud avait un pic d’activité :

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    b. Examinez des graphiques en courbes similaires pour la mémoire disponible sur chaque nœud avec cette requête :

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    tooview une liste de tous les nœuds, présentant les valeur moyenne de hello exact pour mégaoctets disponibles pour chaque nœud, utilisez cette requête :

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    c. Dans les cas de hello que vous souhaitez toodrill vers le bas dans un nœud spécifique en examinant la moyenne de toutes les heures hello, minimale, maximale et 75-centile utilisation du processeur, vous êtes en mesure de toodo en à l’aide de cette requête (remplacez le champ de l’ordinateur) :

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

En savoir plus sur les métriques de performances dans le journal Analytique à hello [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).


## <a name="adding-an-existing-storage-account-toolog-analytics"></a>Ajout d’un tooLog de compte de stockage existant Analytique

Ce modèle ajoute simplement votre stockage comptes tooa nouveau ou existant Analytique de journal espace de travail existant.

[![Déployer tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)

> [!NOTE]
> Dans la sélection d’un groupe de ressources, si vous travaillez avec un espace de travail Analytique de journal déjà existant, sélectionnez « Utiliser l’existante » et recherchez le groupe de ressources hello contenant l’espace de travail hello Analytique de journal. Dans le cas contraire, créez-en un.
> ![Service Fabric](./media/log-analytics-service-fabric/8.png)
>
>

Une fois que ce modèle a été déployé, vous serez en mesure de toosee hello stockage compte connecté tooyour Analytique de journal espace de travail. Dans ce cas, j’ai ajouté un plus stockage compte toohello Exchange espace de travail que j’ai créé ci-dessus.
![Service Fabric](./media/log-analytics-service-fabric/9.png)

## <a name="view-service-fabric-events"></a>Afficher les événements Service Fabric

Une fois que les déploiements de hello sont terminées et hello solution d’infrastructure de Service a été activée dans votre espace de travail, sélectionnez hello **Service Fabric** vignette dans le tableau de bord de Service Fabric hello Analytique de journal toolaunch portail hello. tableau de bord Hello inclut des colonnes de hello Bonjour tableau suivant. Chaque colonne répertorie les événements de 10 supérieure de hello en mettant en correspondance de nombre que les critères de la colonne pour hello spécifié de plage de temps. Vous pouvez exécuter une recherche de journal qui fournit l’intégralité de la liste hello en cliquant sur **afficher tous les** à hello droite en bas de chaque colonne, ou en cliquant sur en-tête de colonne hello.

| **Événement Service Fabric** | **description** |
| --- | --- |
| Problèmes notables |Affichage des problèmes tels que RunAsyncFailures RunAsynCancellations et des pannes de nœud. |
| Événements opérationnels |Événements opérationnels notables, tels que les déploiements et mises à niveau d’application. |
| Événements de service fiable |Événements de service fiable notables, comme Runasyncinvocations. |
| Événements des acteurs |Événements d’acteur notables générés par vos microservices, notamment les exceptions levées par une méthode d’acteur, les activations et désactivations d’acteur, etc. |
| Événements d’application |Tous les événements ETW personnalisés générés par vos applications. |

![Tableau de bord Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Tableau de bord Service Fabric](./media/log-analytics-service-fabric/sf4.png)

Hello tableau suivant montre les méthodes de collecte de données et d’autres détails sur la façon dont les données sont collectées pour Service Fabric.

| plateforme | Agent direct | Agent Operations Manager | Azure Storage | Operations Manager requis ? | Données de l’agent Operations Manager envoyées via un groupe d’administration | fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |  |  | &#8226; |  |  |10 minutes |

> [!NOTE]
> Vous pouvez modifier l’étendue de hello de ces événements Bonjour solution d’infrastructure de Service en cliquant sur **les données basées sur les 7 derniers jours** haut hello du tableau de bord hello. Vous pouvez également afficher les événements générés dans hello sept derniers jours, un jour ou six heures. Vous pouvez également sélectionner **personnalisé** toospecify une plage de dates personnalisée.
>
>

## <a name="next-steps"></a>Étapes suivantes

* Utilisez [recherches de journal dans le journal Analytique](log-analytics-log-searches.md) tooview détaillées des données d’événement Service Fabric.
