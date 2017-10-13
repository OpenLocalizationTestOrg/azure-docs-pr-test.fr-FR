---
title: "Mise à l’échelle automatique et groupes identiques de machines virtuelles | Microsoft Docs"
description: "En savoir plus sur l’utilisation des ressources de diagnostic et de mise à l’échelle pour mettre à l’échelle automatiquement des machines virtuelles dans un groupe identique."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06ff9d9ae1dd8256f0d22c1a60ed6a85554f1f17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-automatic-scaling-and-virtual-machine-scale-sets"></a>Mise à l’échelle automatique et groupes identiques de machines virtuelles
La mise à l’échelle automatique de machines virtuelles dans un jeu de mise à l’échelle consiste à créer ou à supprimer des machines dans l’ensemble en fonction des exigences de performances. Au fur et à mesure de l’évolution du volume de travail, une application peut nécessiter des ressources supplémentaires afin d’exécuter les tâches de manière efficace.

La mise à l’échelle automatique est un processus automatisé qui allège les contraintes de gestion. En réduisant la surcharge, vous n’avez pas besoin de surveiller en permanence les performances du système ou de décider de la manière de gérer les ressources. La mise à l’échelle est un processus élastique. Des ressources supplémentaires peuvent être ajoutées à mesure que la charge augmente. Lorsque la demande diminue, vous pouvez supprimer des ressources afin de réduire les coûts tout en maintenant les niveaux de performances.

Configurez la mise à l’échelle automatique dans un jeu de mise à l’échelle à l’aide d’un modèle Azure Resource Manager, d’Azure PowerShell ou de l’interface CLI Azure ou du portail Azure.

## <a name="set-up-scaling-by-using-resource-manager-templates"></a>Configurer la mise à l’échelle à l’aide de modèles Resource Manager
Au lieu de déployer et de gérer chaque ressource de votre application séparément, utilisez un modèle qui déploie toutes les ressources en une seule opération coordonnée. Dans le modèle, les ressources d’application sont définies et les paramètres de déploiement sont spécifiés pour différents environnements. Le modèle se compose d’un JSON et d’expressions que vous pouvez utiliser pour construire des valeurs pour votre déploiement. Pour en savoir plus, voir [Créer des modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Dans le modèle, vous indiquez l’élément de capacité :

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

La capacité correspond au nombre de machines virtuelles dans le jeu. Vous pouvez modifier manuellement la capacité en déployant un modèle avec une valeur différente. Si vous déployez un modèle simplement pour modifier la capacité, vous pouvez inclure uniquement l’élément SKU avec la capacité mise à jour.

La capacité du groupe identique peut être ajustée automatiquement en combinant la ressource **autoscaleSettings** et l’extension Diagnostics.

### <a name="configure-the-azure-diagnostics-extension"></a>Configurer l’extension Azure Diagnostics
La mise à l’échelle automatique peut uniquement être réalisée si la collecte de mesures est réussie sur chaque machine virtuelle du jeu de mise à l’échelle. L’extension Azure Diagnostics offre des capacités de surveillance et de diagnostic qui répondent aux besoins en matière de collecte de mesures de la ressource de mise à l’échelle. Vous pouvez installer l’extension en tant que partie du modèle Resource Manager.

Cet exemple montre les variables utilisées dans le modèle pour configurer l’extension de diagnostic :

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

Les paramètres sont fournis lorsque le modèle est déployé. Dans cet exemple, le nom du compte de stockage (où sont stockées les données) et le nom du groupe identique (à partir duquel les données sont collectées) sont fournis. Également dans cet exemple de Windows Server, seul le compteur de performances Nombre de threads est collecté. Tous les compteurs de performances disponibles dans Windows ou Linux peuvent être utilisés pour collecter des informations de diagnostic et peuvent être inclus dans la configuration de l’extension.

Cet exemple illustre la définition de l’extension dans le modèle :

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "Microsoft.Insights.VMDiagnosticsSettings",
      "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
          "storageAccount": "[variables('diagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
          "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

Lorsque l’extension de diagnostic s’exécute, les données sont stockées et collectées dans une table, dans le compte de stockage que vous spécifiez. La table **WADPerformanceCounters** regroupe les données collectées :

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-the-autoscalesettings-resource"></a>Configurer la ressource autoScaleSettings
La ressource autoscaleSettings utilise les informations collectées à partir de l’extension Diagnostics pour décider d’augmenter ou de réduire le nombre de machines virtuelles dans l’ensemble d’échelle.

Cet exemple illustre la configuration de la ressource dans le modèle :

```json
{
  "type": "Microsoft.Insights/autoscaleSettings",
  "apiVersion": "2015-04-01",
  "name": "[concat(parameters('resourcePrefix'),'as1')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
  ],
  "properties": {
    "enabled": true,
    "name": "[concat(parameters('resourcePrefix'),'as1')]",
    "profiles": [
      {
        "name": "Profile1",
        "capacity": {
          "minimum": "1",
          "maximum": "10",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

Dans l’exemple ci-dessus, deux règles sont créées afin de définir les actions de mise à l’échelle automatique. La première règle définit l’action d’augmentation de l’échelle, et la deuxième l’action de réduction de l’échelle. Ces valeurs sont fournies dans les règles :

| Règle | Description |
| ---- | ----------- |
| metricName        | Cette valeur est celle du compteur de performances que vous avez défini dans la variable wadperfcounter pour l’extension Diagnostics. Dans l’exemple ci-dessus, le compteur du nombre de threads est utilisé.    |
| metricResourceUri | Cette valeur est l’identificateur de ressource du groupe de machines virtuelles identiques. Cet identificateur contient le nom du groupe de ressources, le nom du fournisseur de ressources et le nom du jeu de mise à l’échelle à mettre à l’échelle. |
| timeGrain         | Cette valeur est la granularité des mesures collectées. Dans l’exemple ci-dessus, les données sont collectées sur un intervalle d’une minute. Cette valeur est utilisée avec timeWindow. |
| statistic         | Cette valeur détermine la façon dont les mesures sont combinées pour prendre en charge l’action de mise à l’échelle automatique. Les valeurs possibles sont : Moyenne, Min, Max. |
| timeWindow        | Cette valeur est la plage de temps pendant laquelle les données d’instance sont collectées. Elle doit être comprise entre 5 minutes et 12 heures. |
| timeAggregation   | Cette valeur détermine la façon dont les données collectées doivent être combinées au fil du temps. La valeur par défaut est Average. Les valeurs possibles sont : Moyenne, Minimum, Maximum, Dernier, Total, Nombre. |
| operator          | Cette valeur est l’opérateur utilisé pour comparer les données de mesure et le seuil. Les valeurs possibles sont : est égal à -Equals), différent de (NotEquals), supérieur à (GreaterThan), égal ou supérieur à (GreaterThanOrEqual), Inférieur à (LessThan), Inférieur ou égal à (LessThanOrEqual). |
| threshold         | Cette valeur est celle qui déclenche l’action de mise à l’échelle. Veillez à définir un écart suffisant entre les valeurs seuil que vous définissez respectivement pour l’action d’**augmentation de l’échelle** et l’action de **réduction de l’échelle**. Si vous définissez des valeurs identiques, le système anticipe un changement constant qui l’empêche d’implémenter une action de mise à l’échelle. Par exemple, la définition des deux valeurs sur 600 threads dans l’exemple précédent ne fonctionne pas. |
| direction         | Cette valeur détermine l’opération qui est effectuée lorsque la valeur de seuil est atteinte. Les valeurs possibles sont Augmenter ou Diminuer. |
| Type              | Cette valeur est le type d’action qui doit se produire. Elle doit être définie sur ChangeCount. |
| value             | Cette valeur indique le nombre de machines virtuelles qui sont ajoutées ou supprimées dans le groupe identique. Cette valeur doit être définie sur 1 ou supérieur. |
| cooldown          | Cette valeur est la durée d’attente depuis la dernière opération de mise à l’échelle avant que l’action suivante se produise. Elle doit être comprise entre une minute et une semaine. |

En fonction du compteur de performance que vous utilisez, certains éléments de la configuration du modèle sont utilisés différemment. Dans l’exemple précédent, le compteur de performances est Nombre de threads, la valeur de seuil est 650 pour une action d’augmentation de l’échelle, et 550 pour une action de réduction de l’échelle. Si vous utilisez un compteur tel que le pourcentage de temps processeur, la valeur de seuil est définie sur le pourcentage d’utilisation du processeur qui détermine une action de mise à l’échelle.

Lorsqu’une action de mise à l’échelle est déclenchée (une charge élevée, par exemple), la capacité de l’ensemble est augmentée en fonction de la valeur spécifiée dans le modèle. Par exemple, dans un jeu de mise à l’échelle où la capacité est définie sur 3 et la valeur d’action de mise à l’échelle est définie sur 1 :

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

Lorsque la charge actuelle fait passer le nombre moyen de threads au-dessus du seuil de 650 :

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

Une action **d’augmentation d’échelle** est déclenchée, ce qui a pour effet d’augmenter d’une unité la capacité de l’ensemble :

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

Une machine virtuelle est alors ajoutée au groupe identique :

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

Après une période de refroidissement de cinq minutes, si le nombre moyen de threads sur les machines est toujours supérieur à 600, une autre machine est ajoutée au jeu. Si le nombre moyen de threads reste inférieur à 550, la capacité du jeu de mise à l’échelle est diminuée d’une unité et une machine est supprimée du jeu.

## <a name="set-up-scaling-using-azure-powershell"></a>Configuration de mise à l’échelle à l’aide d’Azure PowerShell

Pour voir des exemples d’utilisation de PowerShell pour configurer la mise à l’échelle automatique, consultez les [exemples de démarrage rapide d’Azure Monitor PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md).

## <a name="set-up-scaling-using-azure-cli"></a>Configuration de mise à l’échelle à l’aide de l’interface de ligne de commande Azure

Pour voir des exemples d’utilisation de l’interface CLI d’Azure pour configurer la mise à l’échelle automatique, consultez les [exemples de démarrage rapide de l’interface CLI multiplateforme d’Azure Monitor](../monitoring-and-diagnostics/insights-cli-samples.md).

## <a name="set-up-scaling-using-the-azure-portal"></a>Configuration de mise à l’échelle à l’aide du portail Azure

Pour voir un exemple d’utilisation du portail Azure pour configurer la mise à l’échelle automatique, consultez [Création d’un jeu de mise à l’échelle de machine virtuelle à l’aide du portail Azure](virtual-machine-scale-sets-portal-create.md).

## <a name="investigate-scaling-actions"></a>Examiner les actions de mise à l’échelle

* **Portail Azure**  
Vous pouvez obtenir une quantité limitée d’informations par le biais du portail.

* **Azure Resource Explorer**  
Cet outil est le meilleur qui soit pour déterminer l’état actuel de votre groupe identique. Suivez ce chemin d’accès. Vous devriez voir la vue de l’instance du groupe à échelle identique que vous avez créée :  
**Abonnements > {votre abonnement} > resourceGroups > {votre groupe de ressources} > fournisseurs > Microsoft.Compute > virtualMachineScaleSets > {votre groupe identique} > virtualMachines**

* **Azure PowerShell**  
Utilisez cette commande pour obtenir des informations :

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* Connectez-vous à la machine virtuelle jumpbox comme vous le feriez pour n’importe quel autre ordinateur et vous pouvez ensuite accéder à distance aux machines virtuelles du groupe à échelle identique pour surveiller les processus individuels.

## <a name="next-steps"></a>Étapes suivantes
* Pour voir un exemple montrant comment créer un jeu de mise à l’échelle avec une mise à l’échelle automatique configurée, voir [Mise à l’échelle automatique des machines dans un jeu de mise à l’échelle de machine virtuelle](virtual-machine-scale-sets-windows-autoscale.md) .

* Découvrez des exemples de fonctionnalités de surveillance Azure Monitor dans les [exemples de démarrage rapide d’Azure Monitor PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md)

* Pour en savoir plus sur les fonctionnalités de notification, consultez [Utilisation d’actions de mise à l’échelle automatique pour envoyer des notifications d’alerte webhook et par courrier électronique dans Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).

* Découvrez comment [utiliser les journaux d’audit pour envoyer des notifications d’alerte webhook et par courrier électronique dans Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

* En savoir plus sur les [scénarios avancés de mise à l’échelle automatique](virtual-machine-scale-sets-advanced-autoscale.md).
