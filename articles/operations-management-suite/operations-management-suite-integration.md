---
title: aaaIntegrating avec Operations Management Suite (OMS) | Documents Microsoft
description: "En outre toousing hello des fonctionnalités standards d’OMS, vous pouvez l’intégrer avec d’autres tooprovide de gestion des applications et services un environnement de gestion hybride, tooprovide gestion personnalisée des scénarios uniques tooyour environnement ou tooprovide personnalisé expérience de gestion pour vos clients.  Cet article fournit une vue d’ensemble de vos différentes options permettant d’intégrer à OMS et des liens tooarticles fournissant des informations techniques détaillées."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fc5f3a8a-77f7-4103-bd7e-744c15ffcca7
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: dce752dcdc6c725bbafd49db4a5055750487ecf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-operations-management-suite-oms"></a>Intégration avec Operations Management Suite (OMS)
Operations Management Suite est une solution de gestion informatique basée sur le cloud de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et dans le cloud.  En outre toousing hello des fonctionnalités standards d’OMS, vous pouvez l’intégrer avec d’autres tooprovide de gestion des applications et services un environnement de gestion hybride, tooprovide gestion personnalisée des scénarios uniques tooyour environnement ou tooprovide personnalisé expérience de gestion pour vos clients.  Cet article fournit une vue d’ensemble de vos différentes options permettant d’intégrer à OMS de services et des liens de tooarticles en fournissant des informations techniques détaillées. 

## <a name="log-analytics"></a>Log Analytics
Les données de gestion collectées par Log Analytics sont stockées dans le référentiel OMS, qui est hébergé dans Azure.  Toutes les données stockées dans le référentiel de hello est disponible dans les recherches de journal qui procurent une analyse rapide de très grandes quantités de données.  Vos exigences d’intégration peuvent être référentiel de hello toopopulate avec les données de tooextract dans hello référentiel tooprovide une nouvelle visualisation ou de nouvelles données, ce qui la rend disponible pour l’analyse, ou toointegrate avec un autre outil de gestion.

Chaque élément de données dans le référentiel de hello est stocké en tant qu’enregistrement.  Lorsque vous remplissez référentiel de hello, vous devez fournir aux utilisateurs avec le type d’enregistrement hello votre solution utilise et une description de ses propriétés.  Lorsque vous récupérez des données, vous avez besoin de ces informations sur les données de salutation avec lequel vous travaillez.

![Remplissage du référentiel OMS de hello](media/operations-management-suite-integration/repository.png)

### <a name="populate-hello-log-analytics-repository"></a>Remplir le référentiel d’Analytique de journal hello
Il existe plusieurs méthodes pour remplir le référentiel OMS de hello.  Hello méthode que vous utilisez dépend de facteurs tels qu’où se trouve la source de données hello, format hello des données de salutation et les clients que vous devez toosupport.  Une fois que les données sont stockées dans le référentiel de hello, il ne fait aucune différence comment il a été collecté.

Hello sections suivantes décrivent hello différentes options pour le remplissage de référentiel OMS de hello.

#### <a name="connected-sources-and-data-sources"></a>Sources de données et sources connectées
Sources connectées sont des emplacements de hello où les données peuvent être récupérées pour le référentiel d’OMS hello.  Sources de données et les Solutions s’exécutent sur des Sources connectées et définissent les données hello spécifiques qui sont collectées.  Si votre application écrit tooone de données de ces sources de données, vous pouvez le collecter en configurant la source de données hello.  Par exemple, si votre application crée un événement Syslog, puis ils peuvent être collectées par la source de données hello Syslog sur un agent Linux.

* [Sources de données dans Log Analytics](../log-analytics/log-analytics-data-sources.md)

#### <a name="solutions"></a>Solutions
Solutions étendent les fonctionnalités de hello d’OMS.  Une solution peut collecter des données à partir de la source de connectée hello ou il peut effectuer une analyse sur les enregistrements déjà collectées dans le référentiel de hello.  Chaque solution fournie par Microsoft a un article individuel qui fournit des détails de hello sur les données de salutation qu’il collecte.

* [Solutions dans Log Analytics](../log-analytics/log-analytics-add-solutions.md)

#### <a name="http-data-collector-api"></a>API Collecte de données HTTP
Hello API du collecteur de données journal Analytique HTTP est une API REST qui vous permet de référentiel de tooadd JSON données toohello Analytique de journal.  Vous pouvez tirer parti de cette API lorsque vous possédez une application qui ne fournit des données via un des hello d’autres sources de données ou les solutions.  Il peut être le référentiel de hello toopopulate utilisé à partir de n’importe quel client peut appeler les API hello et ne repose pas sur la planification de la collecte d’une source de données ou une solution hello.

* [API Collecte de données HTTP Log Analytics](../log-analytics/log-analytics-data-collector-api.md)

### <a name="retrieve-data-from-hello-log-analytics-repository"></a>Récupérer des données d’espace de stockage hello Analytique de journal
Il existe plusieurs méthodes pour récupérer des données à partir du référentiel d’OMS hello.  Vous pouvez les données de tooretrieve les utilisateurs à l’aide de la console OMS de hello et leur fournir différents types de visualisations et analyse.  Vous pouvez également récupérer des données de salutation à partir d’un processus externe, par exemple une autre solution de gestion.

#### <a name="log-searches"></a>Recherches dans les journaux
Toutes les données stockées dans le référentiel d’OMS hello est disponible via les recherches de journal.  Les utilisateurs peuvent effectuer leur propre analyse ad hoc dans la console OMS hello ou créer un tableau de bord avec une visualisation pour une recherche de journal particulière.  Les solutions peuvent contenir des vues personnalisées avec des visualisations basées sur les recherches prédéfinies.  Vous pouvez utiliser les données de tooaccess de API de recherche de journal de hello dans le référentiel d’OMS hello à partir d’un outil externe de l’application ou de gestion.  

* [Recherches de journal dans Log Analytics](../log-analytics/log-analytics-log-searches.md)
* [API REST Recherche de journal Log Analytics](../log-analytics/log-analytics-log-search-api.md)
* [Applets de commande Log Analytics](https://msdn.microsoft.com/library/mt188224.aspx)

#### <a name="custom-views"></a>Vues personnalisées
Hello Concepteur de vues vous permet de toocreate des vues personnalisées dans la console OMS hello qui fournissent aux utilisateurs la visualisation et l’analyse des données hello dans votre solution.  Chaque vue inclut une vignette qui s’affiche sur la page principale de hello de console de hello et n’importe quel nombre de parties de visualisation qui sont basées sur les recherches de journal que vous définissez.

* [Concepteur de vues Log Analytics](../log-analytics/log-analytics-view-designer.md)

#### <a name="power-bi"></a>Power BI
Analytique de journal peut automatiquement exporter des données à partir du référentiel d’OMS hello dans Power BI afin de vous pouvez tirer parti de ses visualisations et les outils d’analyse.  Il effectue cette exportation selon une planification pour les données de salutation soient toodate. 

* [Exporter les données de journal Analytique tooPower BI](../log-analytics/log-analytics-powerbi.md)

## <a name="automation"></a>Automatisation
OMS peut automatiser traite les données toocollected tooreact ou tooperform autres fonctions de gestion.  Il peut collecter des données à partir de votre application et l’insérer dans le référentiel OMS de hello, ou vous pouvez automatiser correction hello d’un problème connu dans toodata réponse trouvée dans le référentiel de hello. 

![Automatisation](media/operations-management-suite-integration/automate.png)

### <a name="runbooks"></a>Runbooks
Procédures opérationnelles dans Azure Automation, exécuter des scripts PowerShell et les flux de travail Bonjour cloud Azure.  Vous pouvez utiliser les ressources toomanage dans Azure ou autres ressources qui sont accessibles à partir du cloud de hello.  Les runbooks peuvent également être exécutés dans un centre de données local à l’aide de Runbook Worker hybride.  Vous pouvez démarrer un runbook à partir de hello portail Azure ou de processus externes à l’aide d’un nombre de méthodes telles que PowerShell ou hello API Automation.

* [Démarrage d’un Runbook dans Azure Automation](../automation/automation-starting-a-runbook.md)
* [Applets de commande Azure Automation](https://msdn.microsoft.com/library/dn690262.aspx)
* [API REST Automation](https://msdn.microsoft.com/library/mt662285.aspx)
* [Automation .NET](https://msdn.microsoft.com//library/mt465763.aspx)

### <a name="alerts"></a>Alertes
Règles d’alerte d’exécuter automatiquement selon la planification de tooa des recherches de journaux.  Si les résultats de hello correspondent particulier critères hello résultant peut démarrer un runbook dans Azure Automation ou l’alerte appeler un webhook qui permet de démarrer un processus externe.  Les deux de ces réponses peuvent inclure des détails d’alerte hello y compris les données hello renvoyées par la recherche de journal hello.

* [Alertes dans Log Analytics](../log-analytics/log-analytics-alerts.md)
* [API Alerte Log Analytics](../log-analytics/log-analytics-api-alerts.md)

## <a name="backup-and-site-recovery"></a>Sauvegarde et Site Recovery
Sauvegarde et récupération de Site Azure fournissent des services pour protéger vos données d’entreprise et de garantir la disponibilité de hello des serveurs et des applications.  Vous pouvez exploiter ces tooperform services des scénarios tels que fournissant les services de sauvegarde de votre application ou en lançant un basculement d’un ordinateur virtuel.

* [Applets de commande Sauvegarde Azure](https://msdn.microsoft.com/library/mt619253.aspx)
* [API REST Azure Site Recovery](https://msdn.microsoft.com/library/azure/mt750497.aspx)
* [Applets de commande Azure Site Recovery](https://msdn.microsoft.com/library/mt637930.aspx)

## <a name="custom-solutions"></a>Solutions personnalisées
Vous pouvez encapsuler la logique d’intégration dans une solution personnalisée de toorun dans votre espace de travail ou dans l’espace de travail du client.  Votre solution peut inclure une des méthodes d’intégration hello dans cet article dans Ajout tooother ressources tooprovide un scénario de gestion complète.  ressources Hello dans la solution de hello sont empaquetés telles que lors de la solution de hello est supprimée, toutes les ressources hello qu’il a créées sont supprimées de l’espace de travail OMS hello et un abonnement Azure.

Par exemple, votre solution peut inclure une automatisation runbook toogather et traitent les données et puis remplissez référentiel d’Analytique de journal hello à l’aide de hello API du collecteur de données HTTP.  Vous pouvez également inclure une vue personnalisée qui présente et analyse les données hello collectée.  

* Création de solutions personnalisées (bientôt disponible)    

## <a name="next-steps"></a>Étapes suivantes
* Hello de référence [OMS SDK](operations-management-suite-sdk.md) pour des informations techniques sur l’automatisation des services OMS.  

