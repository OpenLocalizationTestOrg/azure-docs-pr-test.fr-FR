---
title: "utilisation des données dans le journal Analytique aaaAnalyze | Documents Microsoft"
description: "Utilisez le tableau de bord de l’utilisation hello dans le journal Analytique tooview la quantité de données est envoyé service Analytique de journal de toohello et résolution des problèmes grandes quantités de données sont envoyées."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 74d0adcb-4dc2-425e-8b62-c65537cef270
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: magoedte
ms.openlocfilehash: c30373dd6edbe3ff900fbebc865575fee61ce14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-usage-in-log-analytics"></a>Analyser l’utilisation des données dans Log Analytics
Analytique de journal inclut des informations sur le volume hello de données collectées, les ordinateurs envoyé des données de hello et hello différents types de données envoyées.  Hello d’utilisation **l’utilisation du journal Analytique** quantité de hello toosee du tableau de bord de données envoyés de service de journal Analytique toohello. tableau de bord Hello affiche la quantité de données collecté par chaque solution et la quantité de données, vos ordinateurs envoient.

## <a name="understand-hello-usage-dashboard"></a>Comprendre le tableau de bord d’utilisation hello
Hello **l’utilisation du journal Analytique** tableau de bord affiche hello informations suivantes :

- Volume de données
    - Volume de données dans le temps (en fonction de la portée temporelle actuelle)
    - Volume de données par solution
    - Données non associées à un ordinateur
- Ordinateurs
    - Ordinateurs envoyant des données
    - Ordinateurs sans données dans les dernières 24 heures
- Offres
    - Nœuds Insight & Analytics
    - Nœuds d’automatisation et de contrôle
    - Nœuds de sécurité
- Performances
    - Durée des données d’index et toocollect
- Liste de requêtes

![tableau de bord utilisation](./media/log-analytics-usage/usage-dashboard01.png)

### <a name="toowork-with-usage-data"></a>toowork avec les données d’utilisation
1. Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com) à l’aide de votre abonnement Azure.
2. Sur hello **Hub** menu, cliquez sur **davantage de services** et, dans la liste hello des ressources, tapez **Analytique de journal**. Comme vous commencez à taper, hello filtres de la liste en fonction de votre entrée. Cliquez sur **Log Analytics**.  
    ![Hub Azure](./media/log-analytics-usage/hub.png)
3. Hello **Analytique de journal** tableau de bord affiche une liste de vos espaces de travail. Sélectionnez un espace de travail.
4. Bonjour *espace de travail* tableau de bord, cliquez sur **l’utilisation du journal Analytique**.
5. Sur hello **l’utilisation du journal Analytique** tableau de bord, cliquez sur **heure : dernières 24 heures** intervalle de temps toochange hello.  
    ![Intervalle de temps](./media/log-analytics-usage/time.png)
6. Panneaux de catégorie vue hello d’utilisation qui montrent les domaines vous intéressent. Un panneau et cliquez sur un élément qu’il contient tooview décrit plus en détail dans [recherche de journal](log-analytics-log-searches.md).  
    ![Exemple de panneau d’utilisation des données](./media/log-analytics-usage/blade.png)
7. Tableau de bord de recherche de journal hello, examinez les résultats de hello qui sont retournées à partir de la recherche de hello.  
    ![exemple de recherche de journal d’utilisation](./media/log-analytics-usage/usage-log-search.png)

## <a name="create-an-alert-when-data-collection-is-higher-than-expected"></a>Créer une alerte lorsque la collection de données est plus volumineuse que prévu
Cette section décrit comment toocreate une alerte si :
- Le volume de données dépasse une quantité spécifiée.
- Volume de données est prédite tooexceed un montant spécifié.

Les [alertes](log-analytics-alerts-creating.md) Log Analytics utilisent des requêtes de recherche. Hello requête suivante a un résultat lorsqu’il y a plus de 100 Go de données collectées dans hello des dernières 24 heures :

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`

Hello requête suivante utilise un simple toopredict formule plus de 100 Go de données seront envoyées par jour : 

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`

tooalert sur un volume de données différents, modification hello 100 Bonjour nombre toohello Go que vous voulez tooalert sur des requêtes.

Utilisez les étapes hello décrites dans [créer une règle d’alerte](log-analytics-alerts-creating.md#create-an-alert-rule) toobe informé de la collecte de données est plus élevée que prévu.

Lorsque vous créez l’alerte hello pour la première requête de hello--lorsqu’il existe plus de 100 Go de données dans les 24 heures, définissez le :
- **Nom** trop*volume de données supérieure à 100 Go des dernières 24 heures*
- **Gravité** trop*avertissement*
- **Requête de recherche** trop`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`
- **Fenêtre de temps** trop*24 heures*.
- **Fréquence des alertes** toobe une heure dans la mesure où les données d’utilisation hello met à jour uniquement une fois par heure.
- **Générer une alerte en fonction de** toobe *nombre de résultats*
- **Nombre de résultats** toobe *supérieur à 0*

Utilisez les étapes hello décrites dans [ajouter des actions tooalert règles](log-analytics-alerts-actions.md) configurer une action de courrier électronique, webhook ou runbook pour la règle d’alerte hello.

Lorsque création alerte hello pour requête de deuxième hello, lorsqu’il est prévu qu’il y aura plus de 100 Go de données des dernières 24 heures, définissez le :
- **Nom** trop*volume de données attendu toogreater à 100 Go dans les 24 heures*
- **Gravité** trop*avertissement*
- **Requête de recherche** trop`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`
- **Fenêtre de temps** trop*3 heures*.
- **Fréquence des alertes** toobe une heure dans la mesure où les données d’utilisation hello met à jour uniquement une fois par heure.
- **Générer une alerte en fonction de** toobe *nombre de résultats*
- **Nombre de résultats** toobe *supérieur à 0*

Lorsque vous recevez une alerte, utilisez les étapes de hello Bonjour suivant tootroubleshoot section pourquoi l’utilisation est plus élevée que prévu.

## <a name="troubleshooting-why-usage-is-higher-than-expected"></a>Résolution des problèmes à l’origine d’une utilisation plus importante que prévu
tableau de bord d’utilisation Hello vous aide à tooidentify pourquoi l’utilisation (et donc les coûts) est plus élevé que vous attendez.

Une utilisation plus importante est due à l’un des éléments suivants, voire les deux :
- Plus de données que prévu envoyé tooLog Analytique
- Plus de nœuds que prévu d’envoi de données tooLog Analytique

### <a name="check-if-there-is-more-data-than-expected"></a>Vérifier s’il y a plus de données que prévu 
Il existe deux sections principales de la page de l’utilisation de hello qui aident à identifier la cause hello collecté par la plupart des données toobe.

Hello *volume de données au fil du temps* graphique montre le volume total de hello des données envoyées et ordinateurs hello envoyant hello la plupart des données. graphique de Hello haut hello permet toosee si la croissance de votre utilisation des données globales, reste stable ou décroissant. liste Hello des ordinateurs affiche les ordinateurs de hello 10 envoi hello la plupart des données.

Hello *volume de données par la solution* graphique montre le volume de hello des données envoyées par chaque solution et les solutions hello envoi hello la plupart des données. graphique Hello haut hello affiche le volume total de hello des données envoyées par chaque solution au fil du temps. Ces informations vous permettent de tooidentify si une solution envoie des données, sur hello montant de données, ou moins de données au fil du temps. la liste de solutions Hello montre solutions hello 10 envoi hello la plupart des données. 

Ces deux graphiques affichent toutes les données. Certaines données sont facturables, et les autres données sont libres. toofocus uniquement sur les données qui facturables, modifier la requête hello sur hello recherche page tooinclude `IsBillable=true`.  

![graphiques de volume de données](./media/log-analytics-usage/log-analytics-usage-data-volume.png)

Examinez hello *volume de données au fil du temps* graphique. solutions de hello toosee et types de données qui envoient des hello la plupart des données pour un ordinateur spécifique, cliquez sur nom hello d’ordinateur de hello. Cliquez sur nom hello de hello premier ordinateur dans la liste de hello.

Bonjour suivant capture d’écran, hello *gestion du journal / Perf* type de données envoie hello la plupart des données pour l’ordinateur de hello. 

![volume de données pour un ordinateur](./media/log-analytics-usage/log-analytics-usage-data-volume-computer.png)

Ensuite, revenez toohello *utilisation* tableau de bord et examinez hello *volume de données par la solution* graphique. les ordinateurs de hello toosee envoi hello la plupart des données d’une solution, cliquez sur nom hello de solution hello dans la liste de hello. Cliquez sur nom hello de solution de première hello dans la liste de hello. 

Bonjour suivant capture d’écran, il confirme que hello *acmetomcat* ordinateur envoie hello la plupart des données pour la solution de gestion des journaux de hello.

![volume de données pour une solution](./media/log-analytics-usage/log-analytics-usage-data-volume-solution.png)

Si nécessaire, effectuer des analyses supplémentaires tooidentify des volumes importants au sein d’un type de données ou de la solution. Les exemples de requêtes incluent :

+ une solution de **sécurité**
  - `Type=SecurityEvent | measure count() by EventID`
+ une solution de **gestion des journaux**
  - `Type=Usage Solution=LogManagement IsBillable=true | measure count() by DataType`
+ le type de données **Perf**
  - `Type=Perf | measure count() by CounterPath`
  - `Type=Perf | measure count() by CounterName`
+ le type de données **Event**
  - `Type=Event | measure count() by EventID`
  - `Type=Event | measure count() by EventLog, EventLevelName`
+ le type de données **Syslog**
  - `Type=Syslog | measure count() by Facility, SeverityLevel`
  - `Type=Syslog | measure count() by ProcessName`
+ le type de données **AzureDiagnostics**
  - `Type=AzureDiagnostics | measure count() by ResourceProvider, ResourceId`

Utilisez hello étapes tooreduce hello volume de journaux collecté suivant :

| Source du volume de données important | Comment volume de données tooreduce |
| -------------------------- | ------------------------- |
| Événements de sécurité            | Sélectionnez [les événements de sécurité courants ou minimaux](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/). <br> Modifier les événements de hello sécurité d’audit stratégie toocollect uniquement si nécessaire. En particulier, passez en revue les événements toocollect hello nécessaire pour <br> - [plateforme de filtrage de l’audit](https://technet.microsoft.com/library/dd772749(WS.10).aspx) <br> - [registre de l’audit](https://docs.microsoft.com/windows/device-security/auditing/audit-registry)<br> - [système de fichiers de l’audit](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system)<br> - [objet de noyau d’audit](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object)<br> - [manipulation du descripteur de l’audit](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation)<br> - [stockage amovible de l’audit](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage) |
| Compteurs de performances       | Modifiez la [configuration du compteur de performances](log-analytics-data-sources-performance-counters.md) de façon à : <br> -Réduire la fréquence de hello de collection <br> - Réduire le nombre de compteurs de performance |
| Journaux d’événements                 | Modifiez la [configuration du journal d’événements](log-analytics-data-sources-windows-events.md) de façon à : <br> -Réduire le nombre de hello des journaux des événements collectés <br> - Collecter uniquement les niveaux d’événement requis Par exemple, ne collectez pas les événements de niveau *Informations*. |
| syslog                     | Modifiez la [configuration du syslog](log-analytics-data-sources-syslog.md) de façon à : <br> -Réduire le nombre hello des installations collectées <br> - Collecter uniquement les niveaux d’événement requis Par exemple, ne collectez pas les événements de niveau *Informations* et *Débogage*. |
| AzureDiagnostics           | Modifiez la collection de journaux de ressources pour : <br> -Réduire le nombre de hello de ressources envoi des journaux tooLog Analytique <br> - Collecter uniquement les journaux nécessaires |
| Données de la solution à partir d’ordinateurs que vous n’avez pas besoin de solution de hello | Utilisez [solution ciblant](../operations-management-suite/operations-management-suite-solution-targeting.md) données toocollect uniquement des groupes d’ordinateurs requis. |

### <a name="check-if-there-are-more-nodes-than-expected"></a>Vérifier s’il y a plus de nœuds que prévu
Si vous êtes sur hello *par nœud (OMS)* tarification, puis que vous êtes facturé en fonction hello les nombre de nœuds et les solutions que vous utilisez. Vous pouvez voir combien de nœuds de chaque offre est utilisés dans hello *offres* section du tableau de bord d’utilisation hello.

![tableau de bord utilisation](./media/log-analytics-usage/log-analytics-usage-offerings.png)

Cliquez sur **afficher tous les...**  tooview hello la liste complète des ordinateurs envoyant des données pour l’offre de sélectionné hello.

Utilisez [solution ciblant](../operations-management-suite/operations-management-suite-solution-targeting.md) données toocollect uniquement des groupes d’ordinateurs requis.


## <a name="next-steps"></a>Étapes suivantes
* Consultez [connecter recherche Analytique de journal](log-analytics-log-searches.md) toolearn comment toouse hello recherche language. Vous pouvez utiliser des requêtes recherche tooperform des analyses supplémentaires sur les données d’utilisation hello.
* Utilisez les étapes hello décrites dans [créer une règle d’alerte](log-analytics-alerts-creating.md#create-an-alert-rule) toobe averti lorsqu’un critère de recherche est remplie.
* Utilisez [solution ciblant](../operations-management-suite/operations-management-suite-solution-targeting.md) données toocollect uniquement des groupes d’ordinateurs requis
* Sélectionnez [les événements de sécurité courants ou minimaux](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/).
* Modifier la [configuration du compteur de performances](log-analytics-data-sources-performance-counters.md)
* Modifier la [configuration du journal d’événements](log-analytics-data-sources-windows-events.md)
* Modifier la [configuration du syslog](log-analytics-data-sources-syslog.md)
