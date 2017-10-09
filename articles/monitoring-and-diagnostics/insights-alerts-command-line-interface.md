---
title: les alertes pour les services Azure - inter-plateformes CLI aaaCreate | Documents Microsoft
description: "Déclencher des messages électroniques, les notifications, les URL de sites Web d’appel (webhooks) ou automation lorsque les conditions hello spécifiées sont remplies."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a>Créer des alertes de métrique dans Azure Monitor pour les services Azure - Interface CLI multiplateforme
> [!div class="op_single_selector"]
> * [Portail](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [INTERFACE DE LIGNE DE COMMANDE](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Vue d'ensemble
Cet article vous explique comment tooset des alertes de métrique Azure à l’aide de hello inter-plateformes Interface de ligne de commande (CLI).

> [!NOTE]
> Moniteur de Azure est hello nouveau nom pour ce qui a été appelé « Azure Insights » jusqu'à 25 septembre 2016. Toutefois, les espaces de noms hello et, par conséquent, les commandes hello ci-dessous encore contient insights » l’hello ».
>
>

Vous pouvez recevoir une alerte en fonction de métriques de surveillance pour vos services Azure ou d'événements sur ces derniers.

* **Valeurs de mesure** - hello déclencheurs d’alerte lorsque la valeur de hello d’une métrique spécifique dépasse un seuil que vous affectez dans les deux sens. Autrement dit, elle déclenche à la fois lorsque hello condition est tout d’abord remplie et puis par la suite que lorsque la condition est n’est plus remplie.    
* **Événements du journal d’activité** : une alerte peut se déclencher sur *chaque* événement ou seulement quand un certain événement se produit. toolearn plus d’informations sur les alertes de journal d’activité [cliquez ici](monitoring-activity-log-alerts.md)

Vous pouvez configurer un hello métrique toodo alerte suivant lorsqu’il déclenche :

* envoyer l’administrateur de service de messagerie des notifications toohello et coadministrateurs
* envoyer des e-mails tooadditional que vous spécifiez.
* appeler un webhook
* Démarrer l’exécution d’un runbook Azure (uniquement à partir de hello portail Azure pour l’instant)

Vous pouvez configurer et obtenir des informations sur les règles d’alerte de métrique via

* [Portail Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [interface de ligne de commande (CLI)](insights-alerts-command-line-interface.md)
* [API REST Azure Monitor](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Vous pouvez toujours recevoir aide pour les commandes en tapant une commande et la mise - aide à la fin de hello. Par exemple :

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a>Créer des règles d’alerte à l’aide de hello CLI
1. Effectuer des conditions préalables de hello et tooAzure de connexion. Consultez les [exemples d’interface de ligne de commande Azure Monitor](insights-cli-samples.md). En bref, installez hello CLI et exécutez les commandes. Ils vous aider à connecté, afficher les abonnements que vous utilisez et vous toorun Azure analyse les commandes prepare.

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. les règles existantes toolist sur un groupe de ressources, utiliser hello suivant du formulaire **azure insights alertes règle liste** *[options] &lt;le groupe de ressources&gt;*

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. toocreate une règle, vous avez besoin de toohave plusieurs informations importantes tout d’abord.
  * Hello **ID de ressource** pour la ressource de hello souhaité tooset une alerte pour
  * Hello **définitions de métrique** disponibles pour cette ressource

     Une façon tooget hello ID de ressource est toouse hello portail Azure. En supposant que la ressource de hello a déjà été créé, sélectionnez-le dans le portail de hello. Puis, dans le panneau suivant de hello, sélectionnez *propriétés* sous hello *paramètres* section. Hello *ID de ressource* est un champ dans le panneau suivant de hello. Une autre méthode consiste à toouse hello [Explorateur de ressources Azure](https://resources.azure.com/).

     Voici un exemple d’ID de ressource d’une application web

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     tooget une liste de métriques disponibles de hello et les unités de ces métriques pour le précédent exemple de ressource hello, hello utilisez CLI commande suivante :  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     *PT1M* est granularité hello de mesure de hello disponible (intervalles de 1 minute). L’utilisation de différentes précisions vous offre différentes options de métriques.
4. toocreate une règle d’alerte basée sur une mesure, utilisez une commande de hello suivant du formulaire :

    **azure insights alerts rule metric set***[options] &lt;ruleName&gt;&lt;location&gt;&lt;resourceGroup&gt;&lt;windowSize&gt;&lt;operator&gt;&lt;threshold&gt;&lt;targetResourceId&gt;&lt;metricName&gt;&lt;timeAggregationOperator&gt;*

    Hello suivant exemple configure une alerte sur une ressource de site web. Hello alerte se déclenche chaque fois qu’il reçoit toujours tout le trafic de 5 minutes, et à nouveau lorsqu’elle ne reçoit aucun trafic pendant 5 minutes.

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. toocreate webhook ou envoyer par courrier électronique lors du déclenche d’une alerte de métriques, créez d’abord par courrier électronique hello et/ou le webhooks. Puis créer règle de hello immédiatement par la suite. Vous ne pouvez pas associer webhook ou des messages électroniques avec déjà créé des règles à l’aide de hello CLI.

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. Vous pouvez vérifier que vos alertes ont été correctement créées en examinant une règle en particulier.

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. règles de toodelete, utilisez une commande sous forme de hello :

    **insights alerts rule delete** [options] &lt;resourceGroup&gt;&lt;ruleName&gt;

    Ces commandes suppriment les règles hello créés précédemment dans cet article.

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a>Étapes suivantes
* [Obtenir une vue d’ensemble de la surveillance Azure](monitoring-overview.md) y compris les types d’informations, vous pouvez collecter et analyser hello.
* Découvrez plus en détail la [configuration des webhooks dans les alertes](insights-webhooks-alerts.md).
* Découvrez plus d’informations sur la [configuration des alertes sur les événements de journal d’activité](monitoring-activity-log-alerts.md).
* Découvrez plus en détails les [runbooks Azure Automation](../automation/automation-starting-a-runbook.md).
* Obtenir un [vue d’ensemble de la collecte des journaux de diagnostic](monitoring-overview-of-diagnostic-logs.md) toocollect détaillée des métriques de haute fréquence sur votre service.
* Obtenir un [vue d’ensemble de la collecte de métriques](insights-how-to-customize-monitoring.md) toomake que votre service est disponible et réactive.
