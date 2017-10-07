---
title: alertes aaaUnderstanding dans Analytique de journal Azure | Documents Microsoft
description: "Alertes dans le journal Analytique identifier des informations importantes dans votre référentiel OMS et peuvent proactive vous avertir des problèmes ou appeler des actions tooattempt toocorrect les.  Cet article décrit hello différents types de règles d’alerte et la façon dont elles sont définies."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: bfa0a5aaeca81674e79a6d647f36d937efeeb439
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-alerts-in-log-analytics"></a>Comprendre les alertes dans Log Analytics

Les alertes identifient des informations importantes dans votre référentiel Log Analytics.  Cet article fournit des détails comment des règles d’alerte dans le journal Analytique travail et décrit les différences de hello entre différents types de règles d’alerte.

Pour le processus de création de règles d’alerte de hello, consultez hello suivant des articles :

- Créer des règles d’alerte avec le [portail Azure](log-analytics-alerts-creating.md)
- Créer des règles d’alerte avec le [modèle Resource Manager](../operations-management-suite/operations-management-suite-solutions-resources-searches-alerts.md)
- Créer des règles d’alerte avec l’[API REST](log-analytics-api-alerts.md)


## <a name="alert-rules"></a>Règles d'alerte

Les alertes sont créées par des règles dédiées qui exécutent automatiquement des recherches dans les journaux à intervalles réguliers.  Si des résultats de recherche de journal hello hello correspond aux critères particuliers un enregistrement d’alerte est créé.  règle de Hello permet ensuite d’exécuter automatiquement une ou plusieurs actions tooproactively vous avertir de l’alerte de hello ou appeler un autre processus.  Différents types de règles d’alerte utilisent une logique différente tooperform cette analyse.

![Alertes Log Analytics](media/log-analytics-alerts/overview.png)

Règles d’alerte sont définies en hello les détails suivants :

- **Recherche de journaux**.  requête Hello qui s’exécute chaque fois qu’une règle d’alerte hello se déclenche.  les enregistrements Hello retournés par cette requête est toodetermine utilisé si une alerte est créée.
- **Fenêtre de temps**.  Spécifie la plage de temps hello pour les requêtes hello.  requête de Hello renvoie uniquement les enregistrements qui ont été créés dans cette plage de hello heure actuelle.  Cela peut être toute valeur comprise entre 5 minutes et 24 heures. Par exemple, si hello fenêtre a la valeur too60 minutes et hello requête exécution à 13:15, seuls les enregistrements créés entre 12:15 PM et 1:15 PM est retournée.
- **Fréquence**.  Spécifie la fréquence à laquelle hello requête doit être exécutée. Peut être toute valeur comprise entre 5 minutes et 24 heures. Doit être égal tooor de moins de fenêtre de temps hello.  Si la valeur de hello est supérieure à la fenêtre de temps hello, vous risquez de perte des enregistrements.<br>Par exemple, imaginons une fenêtre de temps de 30 minutes associée à une fréquence de 60 minutes.  Si l’exécution de requête de hello à 1 h 00, il retourne des enregistrements entre 12:30 et 1:00 PM.  Hello prochaine exécution de requête de hello serait est 2:00 quand elle retournerait enregistrements entre 1 h 30 et 2:00.  Les enregistrements créés entre 13 h et 13 h 30 ne seront jamais analysés.
- **Seuil**.  des résultats de recherche de journal hello Hello sont évaluée toodetermine si une alerte doit être créée.  seuil de Hello est différent pour hello différents types de règles d’alerte.

Chaque règle d’alerte Log Analytics appartient à l’un des deux types existants.  Chacun de ces types est décrit en détail dans les sections hello qui suivent.

- **[Nombre de résultats](#number-of-results-alert-rules)**. Alerte créée lorsque les enregistrements des numéros hello retournée par la recherche de journal hello dépasse un nombre spécifié.
- **[Mesure métrique](#metric-measurement-alert-rules)**.  Alerte créée pour chaque objet dans les résultats de hello de recherche de journal hello avec des valeurs qui dépassent le seuil spécifié.

différences de Hello entre les types de règle d’alerte sont les suivantes.

- **Nombre de résultats** une règle d’alerte crée toujours un certain alerte unique **mesure métrique** règle d’alerte crée une alerte pour chaque objet qui dépasse le seuil de hello.
- **Nombre de résultats** règles d’alerte de créent une alerte lorsque le seuil de hello est dépassé une seule fois. **Mesure métrique** les règles d’alerte peuvent créer une alerte lorsque le seuil de hello est dépassé un certain nombre de fois sur un intervalle de temps spécifique.

## <a name="number-of-results-alert-rules"></a>Règles d’alerte Nombre de résultats
**Nombre de résultats** règles d’alerte de créent une alerte lorsque le nombre hello d’enregistrements renvoyés par la requête de recherche hello dépassé hello spécifié.

### <a name="threshold"></a>Seuil
seuil de Hello pour un **nombre de résultats** règle d’alerte est simplement supérieur ou inférieur à une valeur particulière.  Si le nombre de hello d’enregistrements renvoyés par la recherche de journal hello correspond à ce critère, une alerte est créée.

### <a name="scenarios"></a>Scénarios

#### <a name="events"></a>Événements
Ce type de règle d’alerte est idéal pour la gestion des événements, par exemple les journaux des événements Windows, les journaux Syslog et les journaux personnalisés.  Vous souhaiterez toocreate une alerte lorsqu’un événement d’erreur particulier est créé ou lorsque plusieurs événements d’erreur sont créées dans une fenêtre de temps spécifique.

tooalert sur un seul événement, le nombre de hello de toogreater de résultats à 0 et fréquence de hello et minutes de too5 de fenêtre de temps défini.  Qui exécute la requête de hello chaque 5 minutes et la vérification occurrence hello d’un événement unique qui a été créé depuis la dernière exécution de la dernière requête de hello time hello.  Une fréquence plus longue peut retarder l’heure hello entre hello cours d’événement collectées et alerte hello en cours de création.

Certaines applications peuvent consigner une erreur occasionnelle qui ne doit pas nécessairement déclencher une alerte.  Par exemple, application hello peut à nouveau processus hello qui a créé l’événement d’erreur hello et puis lors de prochaine hello.  Dans ce cas, ne peut-être pas souhaité alerte de hello toocreate, sauf si plusieurs événements sont créés dans une fenêtre de temps spécifique.  

Dans certains cas, vous souhaiterez toocreate une alerte en absence de hello d’un événement.  Par exemple, un processus peut ouvrir une session tooindicate événements standard qui fonctionne correctement.  S’il ne consigne pas un de ces événements dans une fenêtre de temps spécifique, une alerte doit être créée.  Dans ce cas vous définiriez seuil de hello trop**inférieur à 1**.

#### <a name="performance-alerts"></a>Alertes de performances
[Les données de performances](log-analytics-data-sources-performance-counters.md) est stocké en tant qu’enregistrements Bonjour tooevents similaires du référentiel OMS.  Si vous souhaitez tooalert lorsqu’un compteur de performance dépasse un seuil donné, ce seuil doit être inclus dans la requête de hello.

Par exemple, si vous souhaitiez tooalert lorsque hello processeur dépasse 90 %, vous pouvez utiliser une requête comme hello suivant avec seuil hello pour la règle d’alerte hello **supérieur à 0**.

    Type=Perf ObjectName=Processor CounterName="% Processor Time" CounterValue>90

Si vous souhaitiez tooalert lorsque le processeur de hello moyenne à plus de 90 % pour une fenêtre de temps spécifique, vous utiliseriez une requête à l’aide de hello [mesurer commande](log-analytics-search-reference.md#commands) à hello qui suit avec seuil hello pour la règle d’alerte hello **supérieur à 0** .

    Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer | where AggregatedValue>90

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis hello ci-dessus requêtes modifierait toohello suivantes :`Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" and CounterValue>90`
> `Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" | summarize avg(CounterValue) by Computer | where CounterValue>90`


## <a name="metric-measurement-alert-rules"></a>Règles d’alerte Mesure métrique

>[!NOTE]
> Les règles d’alerte relatives aux mesures de métrique sont actuellement en préversion publique.

Les règles d’alerte **Mesure métrique** créent une alerte pour chaque objet d’une requête dont la valeur dépasse un seuil spécifié.  Ils ont hello suivant des différences de **nombre de résultats** règles d’alerte.

#### <a name="log-search"></a>Recherche dans les journaux
Vous pouvez utiliser une requête pour un **nombre de résultats** règle d’alerte, il existe des requêtes de hello exigences spécifiques pour une règle d’alerte de mesure métrique.  Il doit inclure un [mesurer commande](log-analytics-search-reference.md#commands) toogroup les résultats de hello sur un champ particulier. Cette commande doit inclure hello suivant d’éléments.

- **Fonction d’agrégation**.  Détermine le calcul de hello est effectuée et potentiellement un tooaggregate champ numérique.  Par exemple, **count()** retournera nombre hello d’enregistrements dans la requête de hello, **avg(CounterValue)** retournera moyenne hello du champ de CounterValue hello intervalle de salutation.
- **Champ de groupe**.  Un enregistrement avec une valeur agrégée est créé pour chaque instance de ce champ, et une alerte peut être générée pour chacun.  Par exemple, si vous souhaitiez toogenerate une alerte pour chaque ordinateur, vous utiliseriez **par ordinateur**.   
- **Intervalle**.  Définit l’intervalle de temps hello pendant laquelle les données de salutation sont agrégées.  Par exemple, si vous avez spécifié **5 minutes**, un enregistrement doit être créé pour chaque instance du champ de groupe hello agrégé à intervalles de 5 minutes sur la fenêtre de temps hello spécifié pour l’alerte de hello.

#### <a name="threshold"></a>Seuil
seuil de Hello pour les règles d’alerte mesure métrique est défini par une valeur d’agrégat et un certain nombre de violations.  Si n’importe quel point de données de recherche de journal hello dépasse cette valeur, elle est considérée comme une violation.  Si le nombre de failles dans n’importe quel objet dans les résultats de hello hello dépasse hello spécifié la valeur, une alerte est créée pour cet objet.

#### <a name="example"></a>Exemple
Prenons le scénario suivant : vous souhaitez créer une alerte si le taux d’utilisation du processeur d’un ordinateur dépasse 90 % à trois reprises en l’espace de 30 minutes.  Vous devez créer une règle d’alerte avec hello les détails suivants.  

**Requête :** Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer Interval 5minute<br>
**Fenêtre de temps :** 30 minutes<br>
**Fréquence des alertes :** 5 minutes<br>
**Valeur d’agrégation :** supérieure à 90<br>
**Déclencher une alerte en fonction de :** Nombre total de violations supérieur à 5<br>

requête de Hello créerait une valeur moyenne pour chaque ordinateur à des intervalles de 5 minutes.  Cette requête doit être exécutée toutes les 5 minutes pour les données collectées sur hello cours des 30 dernières minutes.  Des exemples de données sont indiqués ci-dessous pour trois ordinateurs.

![Résultats de l’exemple de requête](media/log-analytics-alerts/metrics-measurement-sample-graph.png)

Dans cet exemple, séparer les alertes sont créés pour srv02 et srv03, dans la mesure où ils de violation du seuil de 90 % de hello 3 fois via la fenêtre de temps hello.  Si hello **déclencher une alerte en fonction de :** ont été modifiées trop**consécutif** ensuite une alerte doit être créée uniquement pour srv03, car il en violation de seuil hello pour 3 échantillons consécutifs.

## <a name="alert-records"></a>Enregistrements d’alerte
Les enregistrements d’alerte créés par des règles d’alerte dans Log Analytics ont pour **Type** **Alert** et pour **SourceSystem** **OMS**.  Elles ont des propriétés de hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| Type |*Alert* |
| SourceSystem |*OMS* |
| *Object*  | [Alertes de mesure métrique](#metric-measurement-alert-rules) auront une propriété pour le champ de groupe hello.  Par exemple, si les groupes de recherche de journal hello sur ordinateur, hello alerte enregistrement avec ont un champ de l’ordinateur par nom hello de hello en tant que valeur de hello.
| AlertName |Nom de l’alerte de hello. |
| AlertSeverity |Niveau de gravité d’alerte de hello. |
| LinkToSearchResults |Lier la recherche de journal d’Analytique tooLog qui retourne des enregistrements de hello dans la requête hello créé hello alerte. |
| Interroger |Texte de requête hello qui a été exécuté. |
| QueryExecutionEndTime |Fin de la plage de temps hello pour les requêtes hello. |
| QueryExecutionStartTime |Début de la plage de temps hello pour les requêtes hello. |
| ThresholdOperator | Opérateur qui a été utilisé par la règle d’alerte hello. |
| ThresholdValue | Valeur qui a été utilisé par la règle d’alerte hello. |
| TimeGenerated |Création de l’alerte hello date et heure. |

Autres types d’enregistrements d’alerte créées par hello [solution de gestion des alertes](log-analytics-solution-alert-management.md) et par [Power BI exporte](log-analytics-powerbi.md).  Ces enregistrements ont tous pour **Type** **Alert**, mais se distinguent par leur propriété **SourceSystem**.


## <a name="next-steps"></a>Étapes suivantes
* Installer hello [solution de gestion des alertes](log-analytics-solution-alert-management.md) tooanalyze alertes générées Analytique de journal, ainsi que les alertes collectées à partir de System Center Operations Manager.
* Approfondissez vos connaissances sur les [recherches dans les journaux](log-analytics-log-searches.md) pouvant générer des alertes.
* Effectuez une procédure pas à pas pour [configurer un webhook](log-analytics-alerts-webhooks.md) avec une règle d’alerte.  
* Découvrez comment toowrite [runbooks dans Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate les problèmes identifiés par des alertes.
