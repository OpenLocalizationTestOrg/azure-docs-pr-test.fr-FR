---
title: "aaaCollect et analyser les journaux des événements Windows dans l’Analytique des journaux OMS | Documents Microsoft"
description: "Journaux des événements Windows sont un des hello plus courantes des sources de données utilisés par le journal Analytique.  Cet article décrit comment collection tooconfigure de journaux des événements Windows et les détails des enregistrements de hello créent dans le référentiel d’OMS hello."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: ee52f564-995b-450f-a6ba-0d7b1dac3f32
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: c05648af39258443f22fd11e1d751b5ccec8c391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-event-log-data-sources-in-log-analytics"></a>Sources de données de journal d’événements Windows dans Log Analytics
Journaux des événements Windows sont un des plus courants de hello [des sources de données](log-analytics-data-sources.md) pour la collecte des données à l’aide d’agents Windows depuis de nombreuses applications écrivent toohello journal des événements Windows.  Vous pouvez collecter des événements à partir des journaux standards tels que les applications et système dans Ajout toospecifying des journaux personnalisés créés par les applications, vous devez toomonitor.

![Événements Windows](media/log-analytics-data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a>Configuration des journaux d’événements Windows
Configurer les journaux des événements de Windows hello [menu données de paramètres de journal Analytique](log-analytics-data-sources.md#configuring-data-sources).

Analytique de journal collecte uniquement les événements à partir des journaux des événements Windows hello qui sont spécifiés dans les paramètres de hello.  Vous pouvez ajouter un journal des événements en tapant nom hello du journal de hello et en cliquant sur  **+** .  Pour chaque journal, uniquement les événements hello dont les niveaux de gravité hello sélectionné sont collectés.  Vérifiez les niveaux de gravité hello pour hello particulier journal que toocollect.  Impossible d’indiquer des critères supplémentaires toofilter événements.

Lorsque vous tapez le nom de hello d’un journal des événements, Analytique de journal fournit des suggestions de noms de journal des événements communs. Si le journal hello tooadd n’apparaît pas dans la liste de hello, vous pouvez l’ajouter en tapant le nom complet de hello du journal de hello. Vous trouverez le nom complet de hello du journal de hello à l’aide de l’Observateur d’événements. Dans l’Observateur d’événements, ouvrez hello *propriétés* page hello journal et copie hello chaîne hello *nom complet* champ.

![Configurer les événements Windows](media/log-analytics-data-sources-windows-events/configure.png)

## <a name="data-collection"></a>Collecte des données
Analytique de journal collecte chaque événement qui correspond à une gravité sélectionné à partir d’un journal des événements analysé comme événement de hello est créé.  l’agent Hello enregistre sa place dans chaque journal des événements qu’il collecte à partir de.  Si l’agent de hello est mis hors connexion pendant une période de temps, puis Analytique de journal collecte les événements à partir de l’endroit où il s’était arrêté, même si ces événements ont été créés lors de l’agent de hello est hors connexion.  Il est possible pour ces toonot événements collectés si le journal des événements hello encapsule avec des événements non perçus remplacées pendant que l’agent de hello est hors connexion.

>[!NOTE]
>Log Analytics ne collecte pas les événements d’audit créés par SQL Server à partir de la source *MSSQLSERVER* avec l’ID d’événement 18453 qui contient les mots clés - *Classic* ou *Audit Success* et le mot clé *0xa0000000000000*.
>

## <a name="windows-event-records-properties"></a>Propriétés des enregistrements d’événements Windows
Les enregistrements d’événement Windows ont un type de **événement** et ont des propriétés de hello Bonjour tableau suivant :

| Propriété | Description |
|:--- |:--- |
| Ordinateur |Nom de l’ordinateur hello hello événements ont été collectée à partir de. |
| EventCategory |Catégorie d’événement de hello. |
| EventData |Toutes les données d'événement au format brut. |
| EventID |Nombre d’événements de hello. |
| EventLevel |Gravité d’événement hello sous forme numérique. |
| EventLevelName |Gravité d’événement hello sous forme de texte. |
| EventLog |Nom du journal des événements hello hello événements ont été collectée à partir de. |
| ParameterXml |Valeurs des paramètres d'événement au format XML. |
| ManagementGroupName |Nom du groupe d’administration hello pour les agents de System Center Operations Manager.  Pour les autres agents, cette valeur est AOI-<workspace ID> |
| RenderedDescription |Description de l'événement avec les valeurs de paramètres |
| Source |Source d’événement de hello. |
| SourceSystem |Type d’événement hello de l’agent a été collecté à partir de. <br> Ops Manager – Agent Windows, connexion directe ou géré par Operations Manager <br> Linux – Tous les agents Linux  <br> AzureStorage – Diagnostics Azure |
| TimeGenerated |Événement de hello de date et d’heure a été créé dans Windows. |
| Nom d’utilisateur |Nom d’utilisateur du compte hello qui a consigné hello événement. |

## <a name="log-searches-with-windows-events"></a>Recherches de journaux avec des événements Windows
Hello tableau suivant fournit des exemples de recherches de journal qui extrait des enregistrements d’événements Windows.

| Interroger | Description |
|:--- |:--- |
| Type=Event |Tous les événements Windows. |
| Type=Event EventLevelName=error |Tous les événements Windows avec la gravité de l'erreur. |
| Type=Event &#124; Measure count() by Source |Nombre d’événements Windows par source. |
| Type=Event EventLevelName=error &#124; Measure count() by Source |Nombre d’événements d’erreur Windows par source. |


>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis hello ci-dessus requêtes modifierait toohello suivant.
>
>| Interroger | Description |
|:---|:---|
| Événement |Tous les événements Windows. |
| Événement &#124; où valeur EventLevelName == « erreur » |Tous les événements Windows avec la gravité de l'erreur. |
| Événement &#124; résumer count() par source |Nombre d’événements Windows par source. |
| Événement &#124; où valeur EventLevelName == « erreur » &#124; résumer count() par source |Nombre d’événements d’erreur Windows par source. |


## <a name="next-steps"></a>Étapes suivantes
* Configurer le journal Analytique toocollect autres [des sources de données](log-analytics-data-sources.md) pour l’analyse.
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles.  
* Utilisez [les champs personnalisés](log-analytics-custom-fields.md) tooparse les enregistrements d’événement hello dans des champs individuels.
* Configurez la [collecte des compteurs de performances](log-analytics-data-sources-performance-counters.md) à partir de vos agents Windows.
