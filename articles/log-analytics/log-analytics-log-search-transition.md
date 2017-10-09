---
title: "aide-mémoire aaaAzure Analytique de journal requête langage | Documents Microsoft"
description: "Cet article fournit une assistance sur la transition toohello nouveau langage de requête Analytique de journal si vous êtes déjà familiarisé avec le langage de hérité hello."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 8b4ee3d0b5e1ec8a9f95a09e0ad9835615ad1342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transitioning-tooazure-log-analytics-new-query-language"></a>Transition tooAzure Analytique de journal nouveau langage de requête

> [!NOTE]
> Vous pouvez en savoir plus sur hello Analytique de journal nouveau langage de requête et obtenir hello procédure tooupgrade votre espace de travail à la mise à niveau votre [recherche de journal de toonew espace de travail Analytique des journaux Azure](log-analytics-log-search-upgrade.md).

Cet article fournit une assistance sur la transition toohello nouveau langage de requête Analytique de journal si vous êtes déjà familiarisé avec le langage de hérité hello.

## <a name="language-converter"></a>Convertisseur de langage

Si vous êtes familiarisé avec le langage de requête Analytique de journal hello hérité, hello simple toocreate hello même requête dans un nouveau langage de hello est toouse hello convertisseur de langage qui est installé dans le portail de recherche de journal hello lorsque votre espace de travail est converti.  À l’aide du convertisseur de hello est aussi simple que la saisie d’une requête héritée dans la zone de texte hello et puis en cliquant sur **convertir**.  Vous pouvez cliquer sur requête hello bouton toorun hello ou copier et coller toouse ailleurs.

![Convertisseur de langage](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="cheat-sheet"></a>Aide-mémoire

Hello tableau suivant fournit une comparaison entre un large éventail de requêtes courantes tooequivalent commandes entre le langage de requête nouveaux et existants hello dans Azure journal Analytique.

| Description | Ancien | new |
|:--|:--|:--|
| Rechercher dans toutes les tables      | error | search "error"  (non respect de la casse) |
| Sélectionnez les données d’une table | Type=Event |  Événement |
|                        | Type=Event &#124; select Source, EventLog, EventID | Event &#124; project Source, EventLog, EventID |
|                        | Type=Event &#124; top 100 | Event &#124; take 100 |
| Comparaison de chaînes      | Type=Event Computer=srv01.contoso.com   | Event &#124; where Computer == "srv01.contoso.com" |
|                        | Type=Event Computer=contains("contoso") | Event &#124; where Computer contains "contoso" (non respect de la casse)<br>Event &#124; where Computer contains_cs "Contoso" (respect de la casse) |
|                        | Type=Event Computer=RegEx("@contoso@")  | Event &#124; where Computer matches regex ".*contoso*" |
| Comparaison de dates        | Type=Event TimeGenerated > NOW-1DAYS | Event &#124; where TimeGenerated > ago(1d) |
|                        | Type=Event TimeGenerated>2017-05-01 TimeGenerated<2017-05-31 | Event &#124; where TimeGenerated between (datetime(2017-05-01) .. datetime(2017-05-31)) |
| Comparaison booléenne     | Type=Heartbeat IsGatewayInstalled=false  | Heartbeat | where IsGatewayInstalled == false |
| Trier                   | Type=Event &#124; sort Computer asc, EventLog desc, EventLevelName asc | Event \| sort by Computer asc, EventLog desc, EventLevelName asc |
| Différencier               | Type=Event &#124; dedup Computer \| select Computer | Event &#124; summarize by Computer, EventLog |
| Étendre des colonnes         | Type=Perf CounterName="% Processor Time" &#124; EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION | Perf &#124; where CounterName == "% Processor Time" \| extend Utilization = iff(CounterValue > 50, "HIGH", "LOW") |
| Agrégation            | Type=Event &#124; measure count() as Count by Computer | Event &#124; summarize Count = count() by Computer |
|                                | Type=Perf ObjectName=Processor CounterName="% Processor Time" &#124; measure avg(CounterValue) by Computer interval 5minute | Perf &#124; where ObjectName=="Processor" and CounterName=="% Processor Time" &#124; summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min) |
| Agrégation avec limite | Type=Event &#124; measure count() by Computer &#124; top 10 | Event &#124; summarize AggregatedValue = count() by Computer &#124; limit 10 |
| Union                  | Type=Event or Type=Syslog | union Event, Syslog |
| Join                   | Type=NetworkMonitoring &#124; join inner AgentIP (Type=Heartbeat) ComputerIP | NetworkMonitoring &#124; join kind=inner (search Type == "Heartbeat") on $left.AgentIP == $right.ComputerIP |



## <a name="next-steps"></a>Étapes suivantes
- Extraire un [didacticiel sur l’écriture de requêtes](https://go.microsoft.com/fwlink/?linkid=856078) à l’aide du nouveau langage de requête hello.
- Consultez toohello [référence du langage de requête](https://go.microsoft.com/fwlink/?linkid=856079) pour plus d’informations sur toutes les commandes, d’opérateurs et fonctions pour le nouveau langage de requête hello.  
