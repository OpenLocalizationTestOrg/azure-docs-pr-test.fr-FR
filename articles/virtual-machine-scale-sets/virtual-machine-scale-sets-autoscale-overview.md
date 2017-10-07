---
title: "machine virtuelle et mise à l’échelle aaaAutomatic échelle jeux | Documents Microsoft"
description: "En savoir plus sur l’utilisation de machines virtuelles de mise à l’échelle ressources tooautomatically mise à l’échelle et de diagnostic dans un ensemble d’échelle."
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
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a>La mise à l’échelle automatique du toouse et machines virtuelles identiques
La mise à l’échelle automatique des ordinateurs virtuels dans un ensemble d’échelle est la création de hello ou suppression d’ordinateurs Bonjour définir comme nécessaires toomatch les exigences de performances. Au fur et à mesure du volume hello de travail, une application peut nécessiter des ressources supplémentaires tooenable il tooeffectively effectuer des tâches.

La mise à l’échelle automatique est un processus automatisé qui allège les contraintes de gestion. Par la réduction de la charge, vous ne devez toocontinually surveiller les performances système ou décider comment toomanage ressources. La mise à l’échelle est un processus élastique. Plus de ressources peuvent être ajoutés en tant que charge hello augmente. Et, en tant que la demande diminue, les ressources peuvent être supprimé toominimize coûts et maintenir les niveaux de performances.

Configurer la mise à l’échelle automatique sur une échelle définie à l’aide d’un modèle Azure Resource Manager, Azure PowerShell, CLI d’Azure ou hello portail Azure.

## <a name="set-up-scaling-by-using-resource-manager-templates"></a>Configurer la mise à l’échelle à l’aide de modèles Resource Manager
Au lieu de déployer et de gérer chaque ressource de votre application séparément, utilisez un modèle qui déploie toutes les ressources en une seule opération coordonnée. Dans le modèle de hello, ressources d’application sont définis, et les paramètres de déploiement sont spécifiés pour différents environnements. modèle de Hello se compose de JSON et les expressions que vous pouvez utiliser les valeurs tooconstruct pour votre déploiement. toolearn plus, observez [les modèles de programmation Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Dans le modèle de hello, vous spécifiez d’élément de capacité hello :

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

Capacité identifie nombre hello d’ordinateurs virtuels dans le jeu de hello. Vous pouvez modifier manuellement la capacité de hello en déployant un modèle avec une valeur différente. Si vous déployez une capacité de hello modèle tooonly modification, vous pouvez inclure uniquement les élément de référence (SKU) hello avec une capacité hello mis à jour.

Hello la capacité de votre ensemble d’échelle peut être automatiquement ajustée en utilisant une combinaison de hello **autoscaleSettings** ressource et hello l’extension de diagnostics.

### <a name="configure-hello-azure-diagnostics-extension"></a>Configurer l’extension des Diagnostics Windows Azure hello
Mise à l’échelle automatique peut être faite uniquement si la collecte de métriques est réussie sur chaque ordinateur virtuel dans un ensemble d’échelle hello. Hello Extension des Diagnostics Azure fournit des fonctionnalités d’analyse et de diagnostics hello qui répond aux besoins de collection hello métriques de ressources de mise à l’échelle hello. Vous pouvez installer l’extension de hello en tant que partie du modèle de gestionnaire de ressources hello.

Cet exemple montre les variables hello qui sont utilisées dans l’extension de diagnostics hello modèle tooconfigure hello :

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

Les paramètres sont fournis lorsque le modèle de hello est déployé. Dans cet exemple, le nom hello hello du compte de stockage (stockage des données) et le hello, nom de l’ensemble d’échelle hello (où les données sont collectées) sont fournies. Également dans cet exemple de Windows Server, uniquement les compteurs de performance nombre de threads hello sont collectées. Tous les hello des compteurs de performance disponibles dans Windows ou Linux peut être des informations de diagnostic toocollect utilisé et peut être inclus dans la configuration de l’extension hello.

Cet exemple montre la définition de hello d’extension de hello dans le modèle de hello :

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

Lors de l’extension de diagnostics hello s’exécute, les données de salutation stockées et collectées dans une table, hello compte de stockage que vous spécifiez. Bonjour **WADPerformanceCounters** table, vous pouvez rechercher les données de salutation collectée :

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a>Configurer les ressources d’autoScaleSettings hello
ressources d’autoscaleSettings Hello utilise des informations de hello de hello diagnostics extension toodecide si le nombre de hello tooincrease ou d’une réduction des ordinateurs virtuels de l’échelle de hello défini.

Cet exemple montre une configuration hello de ressource de hello dans le modèle de hello :

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

Dans l’exemple hello ci-dessus, les deux règles sont créées pour définir les actions de mise à l’échelle automatique hello. première règle de Hello définit l’action de montée en puissance parallèle hello et seconde hello définit hello montée en puissance en action. Ces valeurs sont fournies dans les règles de hello :

| Règle | Description |
| ---- | ----------- |
| metricName        | Cette valeur est hello identique au compteur de performance hello que vous défini dans la variable de wadperfcounter hello pour l’extension de diagnostics hello. Dans l’exemple hello ci-dessus, le compteur nombre de threads de hello est utilisé.    |
| metricResourceUri | Cette valeur est l’identificateur de ressource de hello de hello machines virtuelles identiques. Cet identificateur contient hello nom hello du groupe de ressources, hello nom du fournisseur de ressources hello et nom hello de hello échelle ensemble tooscale. |
| timeGrain         | Cette valeur est la granularité hello des métriques de hello sont collectés. Bonjour précédent exemple, les données sont collectées sur un intervalle d’une minute. Cette valeur est utilisée avec timeWindow. |
| statistic         | Cette valeur détermine comment les métriques de hello sont hello tooaccommodate combinée automatique d’action de mise à l’échelle. Hello les valeurs possibles sont : moyenne, Min, Max. |
| timeWindow        | Cette valeur est la plage de hello de temps dans laquelle les données d’instance sont collectées. Elle doit être comprise entre 5 minutes et 12 heures. |
| timeAggregation   | Cette valeur détermine l’association de données hello collectées au fil du temps. valeur par défaut de Hello est moyenne. Hello les valeurs possibles sont : moyenne, Minimum, Maximum, dernier, Total, le nombre. |
| operator          | Cette valeur est un opérateur hello toocompare utilisé hello métrique données et hello du seuil. Hello les valeurs possibles sont : Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual. |
| threshold         | Cette valeur est hello qui déclenche l’action de mise à l’échelle hello. Être tooprovide vraiment une différence suffisante entre les valeurs de seuil hello pour hello **montée en puissance parallèle** et **dans l’échelle** actions. Si vous définissez des mêmes valeurs pour les deux actions hello, système de hello anticipe modification constante, ce qui empêche son implémentation d’une action de mise à l’échelle. Par exemple, définir les deux threads too600 Bonjour précédent exemple ne fonctionne pas. |
| direction         | Cette valeur détermine l’action hello qui est effectuée lorsque la valeur de seuil hello est atteint. les valeurs possibles de Hello sont augmentent ou diminuent. |
| type              | Cette valeur est de type hello d’action qui doit se produire et doit avoir la valeur tooChangeCount. |
| value             | Cette valeur est le nombre de hello d’ordinateurs virtuels qui sont ajoutés tooor supprimé de l’ensemble d’échelle hello. Cette valeur doit être définie sur 1 ou supérieur. |
| cooldown          | Cette valeur est hello toowait de temps depuis la dernière action de mise à l’échelle hello avant l’action suivante de hello se produit. Elle doit être comprise entre une minute et une semaine. |

En fonction de compteur de performance hello, vous utilisez, certains éléments hello dans la configuration du modèle hello sont utilisées différemment. Bonjour précédent exemple, compteur de performances hello est le nombre de threads, valeur de seuil hello 650 pour une action de montée en puissance parallèle et valeur de seuil hello 550 pour l’action de mise à l’échelle hello. Si vous utilisez un compteur de % temps processeur, valeur de seuil hello a la valeur pourcentage de toohello d’utilisation du processeur qui détermine une action de mise à l’échelle.

Lorsqu’une action de mise à l’échelle est déclenchée, comme une charge élevée, hello la capacité d’ensemble de hello est augmentée en fonction de la valeur hello dans le modèle de hello. Par exemple, dans une échelle de définie où la capacité de hello too3 et et hello échelle action a la valeur too1 :

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

Lorsque hello actuel charge causes hello thread moyenne des toogo nombre au-dessus du seuil de hello de 650 :

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

A **montée en puissance parallèle** action est déclenchée que causes hello capacité de hello ensemble toobe est augmentée d’une unité :

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

résultat de Hello est qu'un ordinateur virtuel est ajouté à un ensemble d’échelle toohello :

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

Si le nombre moyen de hello de threads sur les ordinateurs hello reste plus de 600, un autre ordinateur est ajouté après une période de ralentissement de cinq minutes, toohello ensemble. Si le nombre de threads moyenne hello reste ci-dessous 550, capacité hello de hello ensemble d’échelle est réduite d’une unité et un ordinateur est supprimé de hello.

## <a name="set-up-scaling-using-azure-powershell"></a>Configuration de mise à l’échelle à l’aide d’Azure PowerShell

les exemples de toosee d’utilisation de tooset PowerShell d’échelle, examinez [Azure PowerShell d’analyse rapide démarrer exemples](../monitoring-and-diagnostics/insights-powershell-samples.md).

## <a name="set-up-scaling-using-azure-cli"></a>Configuration de mise à l’échelle à l’aide de l’interface de ligne de commande Azure

les exemples de toosee d’utilisation de tooset CLI d’Azure d’échelle, examinez [CLI de Cross-platform Azure analyse rapide démarrer exemples](../monitoring-and-diagnostics/insights-cli-samples.md).

## <a name="set-up-scaling-using-hello-azure-portal"></a>Configurer la mise à l’échelle à l’aide de hello portail Azure

toosee un exemple d’utilisation hello Azure tooset portail de l’échelle automatique, recherchez à [créer un ensemble de l’échelle de machines virtuelles à l’aide de hello Azure portal](virtual-machine-scale-sets-portal-create.md).

## <a name="investigate-scaling-actions"></a>Examiner les actions de mise à l’échelle

* **Portail Azure**  
Vous pouvez en obtenir une quantité limitée d’informations à l’aide du portail de hello.

* **Azure Resource Explorer**  
Cet outil est hello meilleur pour Explorer l’état actuel de hello de votre ensemble d’échelle. Suivez ce chemin d’accès, et vous devez voir vue d’instance hello de montée en puissance hello définie que vous avez créé :  
**Abonnements &gt; {votre abonnement} &gt; resourceGroups &gt; {votre groupe de ressources} &gt; fournisseurs &gt; Microsoft.Compute &gt; virtualMachineScaleSets &gt; {votre groupe identique} &gt; virtualMachines**

* **Azure PowerShell**  
Utilisez cette commande tooget certaines informations :

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* Se connecter toohello jumpbox virtuels comme vous le feriez pour n’importe quel autre ordinateur et vous pouvez ensuite accéder à distance virtuels hello dans toomonitor hello échelle ensemble des processus individuels.

## <a name="next-steps"></a>Étapes suivantes
* Examinez [redimensionner automatiquement les ordinateurs dans un ensemble d’échelle de Machine virtuelle](virtual-machine-scale-sets-windows-autoscale.md) toosee un exemple de comment toocreate une ensemble d’échelle de la mise à l’échelle automatique configurée.

* Découvrez des exemples de fonctionnalités de surveillance Azure Monitor dans les [exemples de démarrage rapide d’Azure Monitor PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md)

* En savoir plus sur les fonctionnalités de notification de [utiliser échelle actions toosend par courrier électronique et webhook des notifications d’alerte dans le moniteur de Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).

* En savoir plus sur la façon de trop[toosend par courrier électronique et webhook des notifications d’alerte de les journaux d’audit d’utilisation dans le moniteur de Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

* En savoir plus sur les [scénarios avancés de mise à l’échelle automatique](virtual-machine-scale-sets-advanced-autoscale.md).
