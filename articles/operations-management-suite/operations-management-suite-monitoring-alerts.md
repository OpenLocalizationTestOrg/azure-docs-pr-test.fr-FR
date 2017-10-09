---
title: "gestion d’aaaAlert dans les produits de contrôle de Microsoft | Documents Microsoft"
description: "Une alerte indique un problème qui nécessite une attention particulière de la part d’un administrateur.  Cet article décrit les différences de hello dans la façon dont les alertes sont créés et gérés dans System Center Operations Manager (SCOM) et Analytique de journal et fournit les meilleures pratiques pour tirer parti des deux produits de hello pour une stratégie de gestion des alertes hybride."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6572c3f8-78ca-4fa9-8fe1-d0b488590788
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 526a3d92f3b6a5d6dec2f3979a934cc94c13f2e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-alerts-with-microsoft-monitoring"></a>Gestion des alertes à l’aide de Microsoft Monitoring
Une alerte indique un problème qui nécessite une attention particulière de la part d’un administrateur.  Il existe des différences entre System Center Operations Manager (SCOM) et Log Analytics dans Operations Management Suite (OMS) en termes de création, de gestion et d’analyse des alertes et de notification en cas de détection d’un problème critique.

## <a name="alerts-in-operations-manager"></a>Alertes dans Operations Manager
Alertes de SCOM sont générées par des règles individuelles ou des analyses tooindicate un problème spécifique.  Une analyse peut générer une alerte lorsqu’il entre un état d’erreur pendant une règle peut générer une alerte tooindicate certains problèmes critiques qui ne sont pas toohello directement lié, la santé d’un objet managé.  Packs d’administration incluent une variété de flux de travail qui créent des alertes pour l’application hello ou service qu’ils gèrent.  Partie du processus de configuration d’un pack d’administration de hello son paramétrage tooensure que vous ne recevez pas trop d’alertes pour les problèmes que vous n’envisagez pas critique.

![Affichage des alertes SCOM](media/operations-management-suite-monitoring-alerts/scom-alert-view.png)

SCOM fournit une gestion complète des alertes avec les alertes ayant un état qui peut être modifié par les administrateurs lorsqu’ils travaillent problème de hello tooresolve.  En cas de hello est résolu, administrateur de hello définit les tooclosed alerte hello à quel moment il n’apparaît plus dans les vues affichant les alertes actives.  Les alertes générées à partir d’analyses peuvent être résolus automatiquement lors de l’analyse de hello retourne l’état intègre tooa.

![État des alertes](media/operations-management-suite-monitoring-alerts/scom-alert-status.png)

## <a name="alerts-in-log-analytics"></a>Alertes dans Log Analytics
Une alerte dans Log Analytics est créée à partir d’une requête de journal qui s’exécute automatiquement à intervalles réguliers.  Vous pouvez créer une règle d’alerte à partir de n’importe quelle requête de journal.  Si la requête de hello retourne des résultats qui correspondent aux critères de hello que vous spécifiez, une alerte est créée.  Cela peut être une requête spécifique qui crée une alerte si un événement particulier est détecté, ou vous pouvez utiliser une requête plus générale qui recherche tout événement d’erreur liées tooa des application particulière.

Alertes d’Analytique des journaux sont écrits de référentiel d’OMS toohello comme un événement et peuvent être récupérés avec une requête de journal.  Ils n’ont un état comme événements SCOM afin que vous pouvez indiquer quand hello est résolu.

![Alerte OMS](media/operations-management-suite-monitoring-alerts/oms-alert.png)

Lorsque SCOM est utilisé comme source de données pour l’Analytique des journaux, des alertes SCOM sont écrites référentiel OMS de toohello qu’ils sont créés et modifiés.  

![Alerte SCOM](media/operations-management-suite-monitoring-alerts/scom-alert.png)

Hello [solution de gestion des alertes](http://technet.microsoft.com/library/mt484092.aspx) fournit un résumé des alertes actives et plusieurs requêtes courantes tooretrieve différents ensembles d’alertes.  Cette analyse de vos alertes est plus efficace qu’un rapport dans SCOM.  Vous pouvez Explorer à partir des données de toodetailed résumés hello et créer des requêtes ad hoc tooretrieve différents ensembles d’alertes.

![solution de gestion des alertes](media/operations-management-suite-monitoring-alerts/alert-management.png)

## <a name="notifications"></a>Notifications
Notifications dans SCOM vous envoient un message ou du texte dans tooalerts de réponse qui correspondent aux critères particuliers.  Vous pouvez créer des abonnements de notification différents qui ont différentes personnes avertis en fonction de critères tels que l’objet hello surveillé, hello gravité d’alerte de hello, type hello du problème détecté ou hello heure du jour.

Plusieurs abonnements peuvent être tooimplement utilisé une stratégie de la notification d’exécution pour un grand nombre de packs d’administration.

![Alertes SCOM](media/operations-management-suite-monitoring-alerts/alerts-overview-scom.png)

Log Analytics peut vous informer par e-mail qu’une alerte a été créée en définissant une action de notification par courrier électronique sur chaque [règle d’alerte](http://technet.microsoft.com/library/mt614775.aspx).  Il n’a pas de possibilité de hello Hello de SCOM s’abonner à des alertes de toomultiple avec une seule règle.  Vous devez également toocreate vos propres règles d’alerte comme OMS ne fournit pas tous préconfigurés.

![Alertes Log Analytics](media/operations-management-suite-monitoring-alerts/alerts-overview-oms.png)

Vous ne peut pas gérer complètement alertes SCOM dans Analytique de journal cependant étant donné que vous pouvez uniquement modifier Bonjour Console opérateur.  Toutefois, Log Analytics est utile dans le cadre d’un processus de gestion des alertes pour proposer des outils d’analyse, dont SCOM à lui seul ne dispose pas.

## <a name="alert-remediation"></a>Correction des alertes
[Mise à jour](http://technet.microsoft.com/library/mt614775.aspx) fait référence le problème d’hello correct tooan tentative tooautomatically identifié par une alerte.

SCOM vous permet de toorun les Diagnostics et récupérations dans le moniteur de tooa de réponse entrant un fonctionnement anormal.  Cela produit analyse simultanées toohello création d’alerte de hello.  Diagnostics et récupérations sont généralement implémentées en tant que script qui s’exécute sur l’agent de hello.  Un toogather de tentatives de diagnostic plus d’informations sur hello détecté le problème pendant une récupération tente de problème de hello toocorrect.

Analytique de journal vous permet de toostart un [runbook Azure Automation](https://azure.microsoft.com/documentation/services/automation/) ou appeler un webhook dans l’alerte de réponse tooa Analytique de journal.  Les runbooks peuvent comporter une logique complexe implémentée dans PowerShell.  script de Hello s’exécute dans Azure et accéder aux ressources Azure et les ressources externes disponibles à partir du cloud de hello.  Azure Automation a hello capacité tooexecute runbook sur un serveur dans votre centre de données local, mais cette fonctionnalité n’est pas disponible actuellement lors du démarrage de runbook de hello dans les alertes de réponse tooLog Analytique.

Les récupérations dans SCOM et les procédures opérationnelles dans OMS peut contenir des scripts PowerShell, mais les récupérations sont toocreate plus difficile et gérer, car ils doivent être contenus dans un Pack d’administration.  Les runbooks sont stockés dans Azure Automation qui fournit des fonctionnalités permettant de les créer, les tester et les gérer.

Si vous utilisez SCOM comme source de données pour l’Analytique des journaux, vous pouvez créer une alerte d’Analytique de journal à l’aide d’un tooretrieve de requête de journal SCOM alertes stockées dans hello référentiel OMS.  Cela vous permettrait toorun un runbook Azure Automation dans l’alerte SCOM tooa de réponse.  Bien entendu, étant donné que hello runbook s’exécute dans Azure, cela n’est pas une stratégie viable pour les récupérations de problèmes de localement.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus de détails hello de [alertes dans System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh212913.aspx).

