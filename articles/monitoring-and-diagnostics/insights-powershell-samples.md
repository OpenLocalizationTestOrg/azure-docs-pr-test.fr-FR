---
title: "Exemples de démarrage rapide Azure Monitor PowerShell. | Microsoft Docs"
description: "Utilisez PowerShell pour accéder aux fonctionnalités d’Azure Monitor telles que la mise à l’échelle, les alertes, les webhooks et la recherche dans les journaux d’activité."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 48f064884c2a6d0a55cc58a44169ed03c62de46d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a>Exemples de démarrage rapide Azure Monitor PowerShell
Cet article vous présente des exemples de commandes PowerShell qui vous aideront à accéder rapidement aux fonctions de surveillance Azure Insights. Azure Monitor permet une mise à l'échelle automatique des services cloud, des machines virtuelles et des applications web, et d’envoyer des notifications d'alerte ou d’appeler des URL web basées sur des valeurs de données de télémétrie configurées.

> [!NOTE]
> Azure Monitor est le nouveau nom de ce qui était appelé « Azure Insights » jusqu’au 25 septembre 2016. Toutefois, les espaces de noms et, par conséquent, les commandes suivantes contiennent toujours « insights ».
> 
> 

## <a name="set-up-powershell"></a>Configurer PowerShell
Si vous ne l’avez déjà fait, configurez PowerShell pour s’exécuter sur votre ordinateur. Pour plus d’informations, consultez l’article [Guide pratique pour installer et configurer PowerShell](/powershell/azure/overview).

## <a name="examples-in-this-article"></a>Exemples de cet article
Les exemples de cet article montrent comment utiliser les applets de commande Azure Monitor. Vous pouvez également consulter la liste complète des applets de commande PowerShell Azure Monitor dans la rubrique [Applets de commande Azure Monitor (Insights)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).

## <a name="sign-in-and-use-subscriptions"></a>Se connecter et utiliser des abonnements
Tout d’abord, connectez-vous à votre abonnement Azure.

```PowerShell
Login-AzureRmAccount
```

Vous devez vous identifier. Vos informations de compte, d’ID de locataire et d’ID d’abonnement par défaut s’affichent alors. Toutes les applets de commande Azure fonctionnent dans le cadre de votre abonnement par défaut. Pour afficher la liste des abonnements auxquels vous avez accès, utilisez la commande suivante.

```PowerShell
Get-AzureRmSubscription
```

Pour remplacer votre contexte de travail par un autre abonnement, utilisez la commande suivante.

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a>Récupérer le journal d’activité d’un abonnement
Utilisez l’applet de commande `Get-AzureRmLog` .  Voici quelques exemples courants.

Obtenir les entrées de journal à partir de cette date/heure :

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

Obtenir les entrées de journal entre une plage de dates/heures :

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Obtenir les entrées de journal à partir d'un groupe de ressources spécifique :

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

Obtenir les entrées de journal à partir d'un fournisseur de ressources spécifique entre une plage de dates/heures :

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Obtenir toutes les entrées de journal avec un appelant spécifique :

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

La commande suivante récupère les 1000 derniers événements du journal d'activité :

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

`Get-AzureRmLog` prend en charge de nombreux autres paramètres. Pour plus d'informations, consultez `Get-AzureRmLog` .

> [!NOTE]
> `Get-AzureRmLog` fournit uniquement 15 jours d'historique. Le paramètre **-MaxEvents** vous permet d'interroger les N derniers événements, au-delà de 15 jours. Pour accéder aux événements antérieurs à 15 jours, utilisez l'API REST ou le Kit SDK (exemple de code C# à l'aide du SDK). Si vous n'incluez pas **StartTime**, la valeur par défaut est **EndTime** moins une heure. Si vous n'incluez pas **EndTime**, la valeur par défaut est l'heure actuelle. Toutes les heures sont exprimées en heure UTC.
> 
> 

## <a name="retrieve-alerts-history"></a>Récupérer l'historique des alertes
Pour afficher tous les événements d'alerte, vous pouvez interroger les journaux Azure Resource Manager en utilisant les exemples suivants.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

Pour afficher l'historique d'une règle d'alerte spécifique, vous pouvez utiliser l’applet de commande `Get-AzureRmAlertHistory` , en passant l'ID de ressource de la règle d'alerte.

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

L’applet de commande `Get-AzureRmAlertHistory` prend en charge différents paramètres. Plus d'informations, consultez [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).

## <a name="retrieve-information-on-alert-rules"></a>Récupérer des informations sur les règles d'alerte
Toutes les commandes suivantes s’appliquent à un groupe de ressources nommé « montest ».

Afficher toutes les propriétés de la règle d'alerte :

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

Récupérer toutes les alertes d'un groupe de ressources :

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

Récupérer toutes les règles d'alerte définies pour une ressource cible. Par exemple, toutes les règles d'alerte définies sur une machine virtuelle.

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

`Get-AzureRmAlertRule` prend en charge d'autres paramètres. Consultez [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) pour plus d'informations.

## <a name="create-metric-alerts"></a>Créer des alertes de métriques
Vous pouvez utiliser l’applet de commande `Add-AlertRule` pour créer, mettre à jour ou désactiver une règle d'alerte.

Vous pouvez créer des propriétés de messagerie et webhook à l'aide de `New-AzureRmAlertRuleEmail` et `New-AzureRmAlertRuleWebhook`, respectivement. Dans l'applet de commande de la règle d'alerte, affectez ces éléments comme des actions à la propriété **Actions** de la règle d'alerte.

Le tableau suivant décrit les paramètres et les valeurs utilisés pour créer une alerte à l'aide d'une mesure.

| paramètre | value |
| --- | --- |
| Nom |simpletestdiskwrite |
| Emplacement de cette règle d'alerte |Est des États-Unis |
| ResourceGroup |montest |
| TargetResourceId |/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig |
| MetricName de l'alerte créée |\PhysicalDisk \Disk écritures par seconde. Consultez le `Get-MetricDefinitions` applet de commande sur la façon de récupérer les noms exacts des mesures |
| operator |GreaterThan |
| Valeur de seuil (nombre/s pour cette métrique) |1 |
| WindowSize (format hh:mm:ss) |00:05:00 |
| agrégation (statistique de la métrique, qui utilise la valeur Average dans ce cas) |Moyenne |
| courriers électroniques personnalisés (tableau de chaînes) |'foo@example.com','bar@example.com' |
| envoyer un courrier électronique aux propriétaires, contributeurs et lecteurs |-SendToServiceOwners |

Créer un courrier électronique

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

Créer une action Webhook

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

Créer la règle d'alerte sur la mesure CPU% sur une machine virtuelle classique

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

Récupérer la règle d'alerte

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

L'applet de commande Add alert met également à jour la règle, s'il existe une règle d'alerte pour les propriétés spécifiées. Pour désactiver une règle d’alerte, incluez le paramètre **-DisableRule**.

## <a name="get-a-list-of-available-metrics-for-alerts"></a>Obtenir la liste des mesures disponibles pour les alertes
Vous pouvez utiliser l’applet de commande `Get-AzureRmMetricDefinition` pour afficher la liste de toutes les métriques pour une ressource spécifique.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

L'exemple suivant génère une table avec le nom de la mesure et son unité.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Une liste complète des options disponibles pour `Get-AzureRmMetricDefinition` est disponible dans [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).

## <a name="create-and-manage-autoscale-settings"></a>Créer et gérer les paramètres de mise à l'échelle automatique
Une ressource, par exemple une application web, une machine virtuelle, un service cloud ou un groupe de machines virtuelles identiques, ne peut avoir qu’un seul paramètre de mise à l’échelle automatique configuré.
Cependant, chaque paramètre de mise à l'échelle automatique peut avoir plusieurs profils. Par exemple, un pour un profil de mise à l’échelle en fonction des performances et un autre pour un profil basé sur une planification. Chaque profil peut avoir plusieurs règles configurées. Pour plus d’informations sur la mise à l’échelle automatique, voir [Mise à l’échelle automatique d’une application](../cloud-services/cloud-services-how-to-scale.md).

Voici la procédure que nous allons suivre :

1. Créez une ou plusieurs règles.
2. Créez un ou plusieurs profils correspondant aux règles que vous avez créées précédemment pour les profils.
3. Facultatif : créez des notifications de mise à l'échelle automatique en configurant les propriétés de courrier électronique et webhook.
4. Créez un paramètre de mise à l'échelle automatique avec un nom pour la ressource cible en mappant les profils et les notifications que vous avez créés aux étapes précédentes.

Les exemples suivants montrent comment créer un paramètre de mise à l’échelle automatique pour un groupe de machines virtuelles identiques sur un système d’exploitation Windows à l’aide de la métrique d’utilisation du processeur.

Tout d’abord, créez une règle de montée en charge, avec augmentation du nombre d’instances.

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

Créez ensuite une règle de baisse de charge, avec une diminution du nombre d’instances.

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

Puis créez un profil pour les règles.

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

Créez une propriété webhook

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

Créez la propriété de notification pour le paramètre de mise à l'échelle automatique, y compris les propriétés de courrier électronique et webhook que vous avez créées précédemment.

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

Enfin, créez le paramètre de mise à l'échelle automatique pour ajouter le profil que vous avez créé précédemment.

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

Pour plus d’informations sur la gestion des paramètres de mise à l’échelle automatique, voir [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).

## <a name="autoscale-history"></a>Historique de la mise à l'échelle automatique
L'exemple suivant vous montre comment consulter les dernières mises à l'échelle automatiques et les derniers événements d'alerte. Utilisez la recherche du journal d’activité pour afficher l'historique de mise à l'échelle automatique.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

Vous pouvez utiliser l’applet de commande `Get-AzureRmAutoScaleHistory` pour récupérer l’historique de mise à l’échelle automatique.

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

Pour plus d’informations, voir [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).

### <a name="view-details-for-an-autoscale-setting"></a>Afficher les détails d'un paramètre de mise à l'échelle automatique
Vous pouvez utiliser l’applet de commande `Get-Autoscalesetting` pour récupérer des informations supplémentaires sur le paramètre de mise à l’échelle automatique.

L'exemple suivant affiche des détails concernant tous les paramètres de mise à l'échelle automatique dans le groupe de ressources ’myrg1’.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

L'exemple suivant affiche des détails concernant tous les paramètres de mise à l'échelle automatique dans le groupe de ressources ’myrg1’, et en particulier le paramètre de mise à l'échelle automatique nommé ’MyScaleVMSSSetting’.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a>Supprimer un paramètre de mise à l'échelle automatique
Vous pouvez utiliser l’applet de commande `Remove-Autoscalesetting` pour supprimer un paramètre de mise à l’échelle automatique.

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a>Gérer les profils de journal pour le journal d’activité
Vous pouvez créer un *profil de journal* et exporter des données de votre journal d’activité vers un compte de stockage, puis configurer la rétention de données pour celui-ci. Si vous le souhaitez, vous pouvez aussi transmettre en continu les données vers votre hub d'événements. Notez que cette fonctionnalité est actuellement en version préliminaire et vous ne pouvez créer qu'un seul profil de journal par abonnement. Vous pouvez utiliser les applets de commande suivantes avec votre abonnement actuel pour créer et gérer des profils de journal. Vous pouvez également choisir un abonnement spécifique. Bien que PowerShell utilise par défaut l’abonnement actif, vous pouvez toujours modifier ce paramètre avec `Set-AzureRmContext`. Vous pouvez configurer le journal d’activité afin d’acheminer les données vers n'importe quel compte de stockage ou un hub d'événements au sein de cet abonnement. Les données sont écrites en tant que fichiers blob au format JSON.

### <a name="get-a-log-profile"></a>Obtenir un profil de journal
Pour extraire vos profils de journal existants, utilisez l’applet de commande `Get-AzureRmLogProfile` .

### <a name="add-a-log-profile-without-data-retention"></a>Ajouter un profil de journal sans conservation des données
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Supprimer un profil de journal
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a>Ajouter un profil de journal avec conservation des données
Vous pouvez spécifier la propriété **-RetentionInDays** en indiquant le nombre de jours (sous la forme d’un entier positif) durant lequel les données seront conservées.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a>Ajouter un profil de journal avec conservation des données et hub d'événements
En plus du routage de vos données vers un compte de stockage, vous pouvez également transmettre en continu ces données vers un hub d'événements. Notez que dans cette version préliminaire, la configuration du compte de stockage est obligatoire mais la configuration du hub d'événements est facultative.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a>Configuration des journaux de diagnostic
De nombreux services Azure fournissent des journaux et des télémétries supplémentaires qui peuvent être configurés pour enregistrer des données dans votre compte de stockage Azure, les envoyer à Event Hubs et/ou les envoyer à un espace de travail Log Analytics OMS. Cette opération ne peut être effectuée qu’au niveau d’une ressource, et le compte de stockage ou l’Event Hub doit être présent dans la même région que la ressource cible où les paramètres de diagnostic sont configurés.

### <a name="get-diagnostic-setting"></a>Obtenir le paramètre de diagnostic
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

Désactiver le paramètre de diagnostic

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

Activer le paramètre de diagnostic sans conservation

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

Activer le paramètre de diagnostic avec conservation

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Activer un paramètre diagnostic avec conservation pour une catégorie de journal spécifique

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Activer le paramètre de diagnostic pour Event Hubs

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

Activer le paramètre de diagnostic pour OMS

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
