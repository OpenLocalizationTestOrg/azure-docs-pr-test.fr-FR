---
title: aaaCreate des alertes pour les services Azure - PowerShell | Documents Microsoft
description: "Déclencher des messages électroniques, les notifications, les URL de sites Web d’appel (webhooks) ou automation lorsque les conditions hello spécifiées sont remplies."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a>Création d’alertes de métrique dans Azure Monitor pour les services Azure - PowerShell
> [!div class="op_single_selector"]
> * [Portail](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [INTERFACE DE LIGNE DE COMMANDE](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Vue d'ensemble
Cet article vous explique comment tooset haut Azure mesure les alertes à l’aide de PowerShell.  

Vous pouvez recevoir une alerte en fonction de métriques de surveillance pour vos services Azure ou d'événements sur ces derniers.

* **Valeurs de mesure** - hello déclencheurs d’alerte lorsque la valeur de hello d’une métrique spécifique dépasse un seuil que vous affectez dans les deux sens. Autrement dit, elle déclenche à la fois lorsque hello condition est tout d’abord remplie et puis par la suite que lorsque la condition est n’est plus remplie.    
* **Événements du journal d’activité** : une alerte peut se déclencher sur *chaque* événement ou seulement quand un certain événement se produit. toolearn plus d’informations sur les alertes de journal d’activité [cliquez ici](monitoring-activity-log-alerts.md)

Vous pouvez configurer un hello métrique toodo alerte suivant lorsqu’il déclenche :

* envoyer l’administrateur de service de messagerie des notifications toohello et coadministrateurs
* envoyer des e-mails tooadditional que vous spécifiez.
* appeler un webhook
* Démarrer l’exécution d’un runbook Azure (uniquement à partir de hello portail Azure)

Vous pouvez configurer et obtenir des informations sur les règles d’alerte avec

* [Portail Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [interface de ligne de commande (CLI)](insights-alerts-command-line-interface.md)
* [API REST Azure Monitor](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Pour plus d’informations, vous pouvez toujours taper ```Get-Help``` et puis hello commande PowerShell que vous voulez de l’aide.

## <a name="create-alert-rules-in-powershell"></a>Créer des règles d’alerte dans PowerShell
1. Ouvrez une session dans tooAzure.   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. Obtenir la liste des abonnements de hello vous disposez. Vérifiez que vous travaillez avec abonnement hello. Dans le cas contraire, définissez-le toohello droite à l’aide de la sortie de hello de `Get-AzureRmSubscription`.

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. les règles existantes toolist sur un groupe de ressources, utilisez hello de commande suivante :

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. toocreate une règle, vous avez besoin de toohave plusieurs informations importantes tout d’abord.

  * Hello **ID de ressource** pour la ressource de hello souhaité tooset une alerte pour
  * Hello **définitions de métrique** disponibles pour cette ressource

     Une façon tooget hello ID de ressource est toouse hello portail Azure. En supposant que la ressource de hello a déjà été créé, sélectionnez-le dans le portail de hello. Puis, dans le panneau suivant de hello, sélectionnez *propriétés* sous hello *paramètres* section. **ID de ressource** est un champ dans le panneau suivant de hello. Une autre méthode consiste à toouse hello [Explorateur de ressources Azure](https://resources.azure.com/).

     Voici un exemple d’ID de ressource d’une application web

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     Vous pouvez utiliser `Get-AzureRmMetricDefinition` liste de hello tooview de toutes les définitions de métrique pour une ressource spécifique.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     Hello exemple suivant génère une table avec mesure de hello nom et le hello unité pour cette métrique.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     La liste complète des options disponibles pour Get-AzureRmMetricDefinition s’obtient en exécutant la commande Get-MetricDefinitions.
5. Hello suivant exemple configure une alerte sur une ressource de site web. Hello alerte se déclenche chaque fois qu’il reçoit toujours tout le trafic de 5 minutes, et à nouveau lorsqu’elle ne reçoit aucun trafic pendant 5 minutes.

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. toocreate webhook ou envoyer par courrier électronique lorsqu’une alerte se déclenche, créez d’abord par courrier électronique hello et/ou le webhooks. Créer immédiatement les règle hello par la suite avec hello - balise Actions et comme indiqué dans hello l’exemple suivant. Vous ne pouvez pas associer un webhook ou des messages électroniques à des règles déjà créées à l’aide de PowerShell.

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. tooverify que vos alertes ont été créés correctement en examinant les règles individuelles hello.

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. Supprimez vos alertes. Ces commandes suppriment les règles hello créés précédemment dans cet article.

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a>Étapes suivantes
* [Obtenir une vue d’ensemble de la surveillance Azure](monitoring-overview.md) y compris les types d’informations, vous pouvez collecter et analyser hello.
* Découvrez plus en détail la [configuration des webhooks dans les alertes](insights-webhooks-alerts.md).
* Découvrez plus d’informations sur la [configuration des alertes sur les événements de journal d’activité](monitoring-activity-log-alerts.md).
* Découvrez plus en détails les [runbooks Azure Automation](../automation/automation-starting-a-runbook.md).
* Obtenir un [vue d’ensemble de la collecte des journaux de diagnostic](monitoring-overview-of-diagnostic-logs.md) toocollect détaillée des métriques de haute fréquence sur votre service.
* Obtenir un [vue d’ensemble de la collecte de métriques](insights-how-to-customize-monitoring.md) toomake que votre service est disponible et réactive.
