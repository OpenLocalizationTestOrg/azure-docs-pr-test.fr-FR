---
title: "exemples de démarrage rapide de PowerShell d’analyse aaaAzure. | Microsoft Docs"
description: "Utilisez PowerShell tooaccess les fonctionnalités de moniteur de Windows Azure telles que la mise à l’échelle, les alertes, webhooks et recherche les journaux d’activité."
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
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a>Exemples de démarrage rapide Azure Monitor PowerShell
Cet article explique les exemples de toohelp de commandes PowerShell vous accéder aux fonctionnalités du moniteur de Windows Azure. Moniteur de Azure vous permet de tooAutoScale Services de cloud computing, Machines virtuelles et les applications Web et toosend des notifications d’alerte ou des URL web appel en fonction des valeurs de données de télémétrie configuré.

> [!NOTE]
> Moniteur de Azure est hello nouveau nom pour ce qui a été appelé « Azure Insights » jusqu'à 25 septembre 2016. Toutefois, les espaces de noms hello et par conséquent hello suit toujours les commandes contient insights » l’hello ».
> 
> 

## <a name="set-up-powershell"></a>Configurer PowerShell
Si vous n’avez pas encore, définir toorun PowerShell sur votre ordinateur. Pour plus d’informations, consultez [comment tooInstall et configurer les PowerShell](/powershell/azure/overview).

## <a name="examples-in-this-article"></a>Exemples de cet article
exemples de Hello dans l’article de hello illustrent comment vous pouvez utiliser les applets de commande de moniteur de Windows Azure. Vous pouvez également examiner hello intégralité de la liste des applets de commande PowerShell d’analyse Azure à [applets de commande Azure moniteur (Insights)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).

## <a name="sign-in-and-use-subscriptions"></a>Se connecter et utiliser des abonnements
Tout d’abord, ouvrez une session dans tooyour abonnement Azure.

```PowerShell
Login-AzureRmAccount
```

Cela vous toosign dans. Vos informations de compte, d’ID de locataire et d’ID d’abonnement par défaut s’affichent alors. Tous les hello des applets de commande Azure fonctionnent dans le contexte de hello de votre abonnement par défaut. liste de hello tooview des abonnements que vous avez accès à, utilisez hello commande suivante.

```PowerShell
Get-AzureRmSubscription
```

toochange votre travail contexte tooa autre abonnement, hello utilisez commande suivante.

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a>Récupérer le journal d’activité d’un abonnement
Hello d’utilisation `Get-AzureRmLog` applet de commande.  Hello Voici des exemples courants.

Obtenir les entrées de journal à partir de cette toopresent date/heure :

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

Hello récupère hello 1000 derniers événements hello journal d’activité de commande suivante :

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

`Get-AzureRmLog` prend en charge de nombreux autres paramètres. Consultez hello `Get-AzureRmLog` référence pour plus d’informations.

> [!NOTE]
> `Get-AzureRmLog` fournit uniquement 15 jours d'historique. À l’aide de hello **- MaxEvents** paramètre vous permet de tooquery hello dernière N événements, au-delà de 15 jours. événements tooaccess plus de 15 jours, utilisez hello API REST ou le Kit de développement logiciel (exemple c# à l’aide du Kit de développement logiciel de hello). Si vous n’incluez pas **StartTime**, la valeur par défaut hello **EndTime** moins d’une heure. Si vous n’incluez pas **EndTime**, valeur par défaut de hello est l’heure actuelle. Toutes les heures sont exprimées en heure UTC.
> 
> 

## <a name="retrieve-alerts-history"></a>Récupérer l'historique des alertes
tooview tous les événements d’alerte, vous pouvez interroger hello journaux Azure Resource Manager à l’aide de hello exemple suivant.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

règle de l’historique de hello tooview pour une alerte spécifique, vous pouvez utiliser hello `Get-AzureRmAlertHistory` applet de commande, en passant un ID de ressource hello de règle d’alerte hello.

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

Hello `Get-AzureRmAlertHistory` applet de commande prend en charge les différents paramètres. Plus d'informations, consultez [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).

## <a name="retrieve-information-on-alert-rules"></a>Récupérer des informations sur les règles d'alerte
Tous les hello suivant les commandes agissent sur un groupe de ressources nommé « montest ».

Afficher toutes les propriétés de hello de règle d’alerte hello :

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
Vous pouvez utiliser hello `Add-AlertRule` toocreate de l’applet de commande, mettre à jour ou désactiver une règle d’alerte.

Vous pouvez créer des propriétés de messagerie et webhook à l'aide de `New-AzureRmAlertRuleEmail` et `New-AzureRmAlertRuleWebhook`, respectivement. Dans l’applet de commande de règle d’alerte hello attribuer en tant qu’actions toohello **Actions** propriété Hello règle d’alerte.

Hello tableau suivant décrit les paramètres hello et valeurs utilisé toocreate une alerte à l’aide d’une métrique.

| paramètre | value |
| --- | --- |
| Nom |simpletestdiskwrite |
| Emplacement de cette règle d'alerte |Est des États-Unis |
| ResourceGroup |montest |
| TargetResourceId |/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig |
| MetricName d’alerte de hello est créé |\PhysicalDisk \Disk écritures par seconde. Consultez hello `Get-MetricDefinitions` applet de commande sur comment tooretrieve hello des noms de métrique exactes |
| operator |GreaterThan |
| Valeur de seuil (nombre/s pour cette métrique) |1 |
| WindowSize (format hh:mm:ss) |00:05:00 |
| agrégation (statistique de mesure hello, qui utilise le nombre moyen de, dans ce cas) |Moyenne |
| courriers électroniques personnalisés (tableau de chaînes) |'foo@example.com','bar@example.com' |
| envoyer par courrier électronique tooowners, les collaborateurs et les lecteurs |-SendToServiceOwners |

Créer un courrier électronique

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

Créer une action Webhook

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

Créer une règle d’alerte hello sur métrique de % processeur hello sur une machine virtuelle classique

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

Récupérer la règle d’alerte hello

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

applet de commande alerte Hello ajouter met également à jour les règles de hello si une règle d’alerte existe déjà pour hello propriété. toodisable une règle d’alerte, incluez le paramètre hello **- DisableRule**.

## <a name="get-a-list-of-available-metrics-for-alerts"></a>Obtenir la liste des mesures disponibles pour les alertes
Vous pouvez utiliser hello `Get-AzureRmMetricDefinition` applet de commande tooview hello parmi toutes les métriques pour une ressource spécifique.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

Hello exemple suivant génère une table avec mesure de hello nom et le hello unité pour celle-ci.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Une liste complète des options disponibles pour `Get-AzureRmMetricDefinition` est disponible dans [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).

## <a name="create-and-manage-autoscale-settings"></a>Créer et gérer les paramètres de mise à l'échelle automatique
Une ressource, par exemple une application web, une machine virtuelle, un service cloud ou un groupe de machines virtuelles identiques, ne peut avoir qu’un seul paramètre de mise à l’échelle automatique configuré.
Cependant, chaque paramètre de mise à l'échelle automatique peut avoir plusieurs profils. Par exemple, un pour un profil de mise à l’échelle en fonction des performances et un autre pour un profil basé sur une planification. Chaque profil peut avoir plusieurs règles configurées. Pour plus d’informations sur l’échelle automatique, consultez [comment tooAutoscale une Application](../cloud-services/cloud-services-how-to-scale.md).

Voici les étapes hello que nous allons utiliser :

1. Créez une ou plusieurs règles.
2. Créer des profils hello du mappage des règles que vous avez créé précédemment toohello profils.
3. Facultatif : créez des notifications de mise à l'échelle automatique en configurant les propriétés de courrier électronique et webhook.
4. Créez un paramètre de mise à l’échelle avec un nom de la ressource cible de hello en mappant les profils hello et les notifications que vous avez créé dans les étapes précédentes hello.

Hello exemples suivants montrent comment vous pouvez créer un paramètre d’échelle automatique pour un ensemble d’échelle de Machine virtuelle pour un système d’exploitation de Windows basé l’aide de métriques d’utilisation du processeur de hello.

Tout d’abord, créez une règle tooscale à la sortie, avec une augmentation de nombre d’instance.

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

Ensuite, créez une règle tooscale dans, avec une diminution du nombre instance.

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

Ensuite, créez un profil pour les règles de hello.

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

Créez une propriété webhook

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

Créer une propriété de notification de hello pour le paramètre de mise à l’échelle hello, notamment le courrier électronique et hello webhook que vous avez créé précédemment.

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

Enfin, créez hello échelle tooadd hello profil de paramètre que vous avez créé précédemment.

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

Pour plus d’informations sur la gestion des paramètres de mise à l’échelle automatique, voir [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).

## <a name="autoscale-history"></a>Historique de la mise à l'échelle automatique
Hello exemple suivant vous montre comment vous pouvez afficher les événements de mise à l’échelle et alerte récents. Utilisez hello journal recherche tooview hello échelle historique de l’activité.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

Vous pouvez utiliser hello `Get-AzureRmAutoScaleHistory` tooretrieve de l’applet de commande l’historique de mise à l’échelle.

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

Pour plus d’informations, voir [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).

### <a name="view-details-for-an-autoscale-setting"></a>Afficher les détails d'un paramètre de mise à l'échelle automatique
Vous pouvez utiliser hello `Get-Autoscalesetting` tooretrieve de l’applet de commande plus d’informations sur la configuration de mise à l’échelle hello.

Hello exemple suivant donne des détails sur tous les paramètres de mise à l’échelle dans le groupe de ressources hello 'myrg1'.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

Bonjour exemple suivant affiche les détails de tous les paramètres de mise à l’échelle dans le groupe de ressources hello 'myrg1' et spécifiquement hello nommé 'MyScaleVMSSSetting' de paramètre de mise à l’échelle.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a>Supprimer un paramètre de mise à l'échelle automatique
Vous pouvez utiliser hello `Remove-Autoscalesetting` toodelete de l’applet de commande un paramètre de mise à l’échelle.

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a>Gérer les profils de journal pour le journal d’activité
Vous pouvez créer un *connecter profil* et exporter des données à partir de votre compte de stockage tooa journal des activités et vous peuvent configurer la rétention des données pour qu’il. Si vous le souhaitez, vous pouvez également transmettre en continu hello données tooyour concentrateur d’événements. Notez que cette fonctionnalité est actuellement en version préliminaire et vous ne pouvez créer qu'un seul profil de journal par abonnement. Vous pouvez utiliser hello suivant d’applets de commande avec votre toocreate d’abonnement en cours et gérer les profils de journal. Vous pouvez également choisir un abonnement spécifique. Bien que PowerShell par défaut toohello abonnement, vous pouvez toujours modifier que l’utilisation `Set-AzureRmContext`. Vous pouvez configurer le compte de stockage d’activité journal tooroute données tooany ou concentrateur d’événements au sein de cet abonnement. Les données sont écrites en tant que fichiers blob au format JSON.

### <a name="get-a-log-profile"></a>Obtenir un profil de journal
toofetch vos profils journal existant, utilisez hello `Get-AzureRmLogProfile` applet de commande.

### <a name="add-a-log-profile-without-data-retention"></a>Ajouter un profil de journal sans conservation des données
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Supprimer un profil de journal
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a>Ajouter un profil de journal avec conservation des données
Vous pouvez spécifier hello **- RetentionInDays** propriété hello nombre de jours, comme un entier positif, où les données de salutation sont conservées.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a>Ajouter un profil de journal avec conservation des données et hub d'événements
Dans Ajout toorouting votre compte toostorage de données, vous pouvez également diffuser en continu tooan concentrateur d’événements. Notez que dans cette version préliminaire release et hello configuration de compte de stockage est obligatoire mais configuration du Hub d’événements est facultative.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a>Configuration des journaux de diagnostic
Plusieurs services Azure fournissent des journaux supplémentaires et télémétrie qui peut être des données toosave configuré dans votre compte Azure Storage, envoyer tooEvent concentrateurs et/ou envoyés d’espace de travail Analytique des journaux OMS tooan. Cette opération ne peut être effectuée qu’à un niveau de la ressource et le concentrateur de compte ou l’événement de stockage hello doit être présent dans hello même région en tant que ressource de hello cible où hello diagnostics est défini.

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
