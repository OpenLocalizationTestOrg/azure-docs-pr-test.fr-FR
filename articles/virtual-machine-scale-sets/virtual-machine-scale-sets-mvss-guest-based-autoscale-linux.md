---
title: "Utiliser la mise à l’échelle automatique Azure avec des mesures invitées dans un modèle de groupe identique Linux | Microsoft Docs"
description: "Découvrez comment tooautoscale à l’aide des métriques d’invité dans un modèle d’ensemble d’échelle de Machine virtuelle Linux"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: na
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: negat
ms.openlocfilehash: 7afbef943a5f15c7a72dcf7114f46d521c504424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a>Mise à l’échelle automatique en utilisant des mesures invitées dans un modèle de groupe identique Linux

Il existe deux types de mesures dans Azure qui sont rassemblées à partir d’ordinateurs virtuels et mettre à l’échelle des jeux : certains proviennent de hello héberger l’ordinateur virtuel et d’autres proviennent de machine virtuelle invitée la hello. Mesures d’ordinateur hôte ne nécessitent pas le programme d’installation supplémentaire, car ils sont collectés par l’hôte hello machine virtuelle, tandis que les métriques invité nécessitent tooinstall hello [extension des Diagnostics Windows Azure](../virtual-machines/windows/extensions-diagnostics-template.md) ou hello [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) Bonjour ordinateur virtuel invité. Une raison toouse invité mesures courantes au lieu de mesures d’ordinateur hôte est que les métriques invité offrent un plus large éventail de mesures que les mesures de l’hôte. Les mesures de consommation de la mémoire, notamment, ne sont disponibles que via les mesures invitées. mesures d’ordinateur hôte Hello pris en charge sont répertoriés [ici](../monitoring-and-diagnostics/monitoring-supported-metrics.md), et les métriques invité couramment utilisés sont répertoriés [ici](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md). Cet article explique comment toomodify hello [échelle viable minimale définie modèle](./virtual-machine-scale-sets-mvss-start.md) toouse les règles de mise à l’échelle en fonction de mesures d’invité pour Linux identiques.

## <a name="change-hello-template-definition"></a>Modifier la définition de modèle hello

Notre modèle de jeu minimale viable peut être consulté [ici](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), et de notre modèle de déploiement de mise à l’échelle de hello Linux avec mise à l’échelle basée sur invité peut être consulté [ici](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json). Examinons hello diff utilisé toocreate ce modèle (`git diff minimum-viable-scale-set existing-vnet`) élément par élément :

Ajoutons tout d’abord les paramètres de `storageAccountName` et `storageAccountSasToken`. agent de diagnostics Hello stockera les données de mesure dans un [table](../cosmos-db/table-storage-how-to-use-dotnet.md) dans ce compte de stockage. À compter de l’Agent de Diagnostics Linux version 3.0 de hello, à l’aide d’une clé d’accès de stockage n’est plus pris en charge. Nous devons utiliser un [jeton SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "storageAccountName": {
+      "type": "string"
+    },
+    "storageAccountSasToken": {
+      "type": "securestring"
     }
   },
```

Ensuite, nous modifions l’ensemble d’échelle hello `extensionProfile` extension de diagnostics tooinclude hello. Dans cette configuration, nous spécifier les ID de mise à l’échelle hello jeu toocollect les métriques à partir de la ressource hello, ainsi que hello compte de stockage et les métriques SAS toouse jeton toostore hello. Nous avons également de spécifier la fréquence à laquelle les métriques de hello sont agrégés (dans ce cas, toutes les minutes) et le tootrack métriques (dans ce cas mémoire utilisée pour cent). Pour plus d’informations sur cette configuration et les mesures autres que le pourcentage de mémoire utilisée, consultez [cette documentation](../virtual-machines/linux/diagnostic-extension.md).

```diff
                 }
               }
             ]
+          },
+          "extensionProfile": {
+            "extensions": [
+              {
+                "name": "LinuxDiagnosticExtension",
+                "properties": {
+                  "publisher": "Microsoft.Azure.Diagnostics",
+                  "type": "LinuxDiagnostic",
+                  "typeHandlerVersion": "3.0",
+                  "settings": {
+                    "StorageAccount": "[parameters('storageAccountName')]",
+                    "ladCfg": {
+                      "diagnosticMonitorConfiguration": {
+                        "performanceCounters": {
+                          "sinks": "WADMetricJsonBlob",
+                          "performanceCounterConfiguration": [
+                            {
+                              "unit": "percent",
+                              "type": "builtin",
+                              "class": "memory",
+                              "counter": "percentUsedMemory",
+                              "counterSpecifier": "/builtin/memory/percentUsedMemory",
+                              "condition": "IsAggregate=TRUE"
+                            }
+                          ]
+                        },
+                        "metrics": {
+                          "metricAggregation": [
+                            {
+                              "scheduledTransferPeriod": "PT1M"
+                            }
+                          ],
+                          "resourceId": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]"
+                        }
+                      }
+                    }
+                  },
+                  "protectedSettings": {
+                    "storageAccountName": "[parameters('storageAccountName')]",
+                    "storageAccountSasToken": "[parameters('storageAccountSasToken')]",
+                    "sinksConfig": {
+                      "sink": [
+                        {
+                          "name": "WADMetricJsonBlob",
+                          "type": "JsonBlob"
+                        }
+                      ]
+                    }
+                  }
+                }
+              }
+            ]
           }
         }
       }
```

Enfin, nous ajoutons un `autoscaleSettings` tooconfigure mise à l’échelle les ressources en fonction de ces mesures. Cette ressource a un `dependsOn` la clause qui fait référence à l’échelle de hello définie tooensure hello identiques existe avant de tenter de tooautoscale il. Si vous choisissez un autre tooautoscale métrique sur, nous utiliseriez hello `counterSpecifier` à partir de la configuration de l’extension diagnostics hello comme hello `metricName` dans la configuration de mise à l’échelle hello. Pour plus d’informations sur la configuration de l’échelle automatique, consultez hello [mise à l’échelle les meilleures pratiques](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) et hello [documentation de référence API REST de Azure analyse](https://msdn.microsoft.com/library/azure/dn931928.aspx).

```diff
+    },
+    {
+      "type": "Microsoft.Insights/autoscaleSettings",
+      "apiVersion": "2015-04-01",
+      "name": "guestMetricsAutoscale",
+      "location": "[resourceGroup().location]",
+      "dependsOn": [
+        "Microsoft.Compute/virtualMachineScaleSets/myScaleSet"
+      ],
+      "properties": {
+        "name": "guestMetricsAutoscale",
+        "targetResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+        "enabled": true,
+        "profiles": [
+          {
+            "name": "Profile1",
+            "capacity": {
+              "minimum": "1",
+              "maximum": "10",
+              "default": "3"
+            },
+            "rules": [
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "GreaterThan",
+                  "threshold": 60
+                },
+                "scaleAction": {
+                  "direction": "Increase",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              },
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "LessThan",
+                  "threshold": 30
+                },
+                "scaleAction": {
+                  "direction": "Decrease",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              }
+            ]
+          }
+        ]
+      }
     }
   ]
 }
```





## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
