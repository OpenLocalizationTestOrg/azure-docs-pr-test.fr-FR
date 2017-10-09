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
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="2b78a-103">Mise à l’échelle automatique en utilisant des mesures invitées dans un modèle de groupe identique Linux</span><span class="sxs-lookup"><span data-stu-id="2b78a-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="2b78a-104">Il existe deux types de mesures dans Azure qui sont rassemblées à partir d’ordinateurs virtuels et mettre à l’échelle des jeux : certains proviennent de hello héberger l’ordinateur virtuel et d’autres proviennent de machine virtuelle invitée la hello.</span><span class="sxs-lookup"><span data-stu-id="2b78a-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from hello host VM and others come from hello guest VM.</span></span> <span data-ttu-id="2b78a-105">Mesures d’ordinateur hôte ne nécessitent pas le programme d’installation supplémentaire, car ils sont collectés par l’hôte hello machine virtuelle, tandis que les métriques invité nécessitent tooinstall hello [extension des Diagnostics Windows Azure](../virtual-machines/windows/extensions-diagnostics-template.md) ou hello [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) Bonjour ordinateur virtuel invité.</span><span class="sxs-lookup"><span data-stu-id="2b78a-105">Host metrics do not require additional setup because they are collected by hello host VM, whereas guest metrics require us tooinstall hello [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or hello [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in hello guest VM.</span></span> <span data-ttu-id="2b78a-106">Une raison toouse invité mesures courantes au lieu de mesures d’ordinateur hôte est que les métriques invité offrent un plus large éventail de mesures que les mesures de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="2b78a-106">One common reason toouse guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="2b78a-107">Les mesures de consommation de la mémoire, notamment, ne sont disponibles que via les mesures invitées.</span><span class="sxs-lookup"><span data-stu-id="2b78a-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="2b78a-108">mesures d’ordinateur hôte Hello pris en charge sont répertoriés [ici](../monitoring-and-diagnostics/monitoring-supported-metrics.md), et les métriques invité couramment utilisés sont répertoriés [ici](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="2b78a-108">hello supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="2b78a-109">Cet article explique comment toomodify hello [échelle viable minimale définie modèle](./virtual-machine-scale-sets-mvss-start.md) toouse les règles de mise à l’échelle en fonction de mesures d’invité pour Linux identiques.</span><span class="sxs-lookup"><span data-stu-id="2b78a-109">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toouse autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="2b78a-110">Modifier la définition de modèle hello</span><span class="sxs-lookup"><span data-stu-id="2b78a-110">Change hello template definition</span></span>

<span data-ttu-id="2b78a-111">Notre modèle de jeu minimale viable peut être consulté [ici](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), et de notre modèle de déploiement de mise à l’échelle de hello Linux avec mise à l’échelle basée sur invité peut être consulté [ici](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="2b78a-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="2b78a-112">Examinons hello diff utilisé toocreate ce modèle (`git diff minimum-viable-scale-set existing-vnet`) élément par élément :</span><span class="sxs-lookup"><span data-stu-id="2b78a-112">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="2b78a-113">Ajoutons tout d’abord les paramètres de `storageAccountName` et `storageAccountSasToken`.</span><span class="sxs-lookup"><span data-stu-id="2b78a-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="2b78a-114">agent de diagnostics Hello stockera les données de mesure dans un [table](../cosmos-db/table-storage-how-to-use-dotnet.md) dans ce compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2b78a-114">hello diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="2b78a-115">À compter de l’Agent de Diagnostics Linux version 3.0 de hello, à l’aide d’une clé d’accès de stockage n’est plus pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2b78a-115">As of hello Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="2b78a-116">Nous devons utiliser un [jeton SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="2b78a-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

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

<span data-ttu-id="2b78a-117">Ensuite, nous modifions l’ensemble d’échelle hello `extensionProfile` extension de diagnostics tooinclude hello.</span><span class="sxs-lookup"><span data-stu-id="2b78a-117">Next, we modify hello scale set `extensionProfile` tooinclude hello diagnostics extension.</span></span> <span data-ttu-id="2b78a-118">Dans cette configuration, nous spécifier les ID de mise à l’échelle hello jeu toocollect les métriques à partir de la ressource hello, ainsi que hello compte de stockage et les métriques SAS toouse jeton toostore hello.</span><span class="sxs-lookup"><span data-stu-id="2b78a-118">In this configuration, we specify hello resource ID of hello scale set toocollect metrics from, as well as hello storage account and SAS token toouse toostore hello metrics.</span></span> <span data-ttu-id="2b78a-119">Nous avons également de spécifier la fréquence à laquelle les métriques de hello sont agrégés (dans ce cas, toutes les minutes) et le tootrack métriques (dans ce cas mémoire utilisée pour cent).</span><span class="sxs-lookup"><span data-stu-id="2b78a-119">We also specify how frequently hello metrics are aggregated (in this case every minute) and which metrics tootrack (in this case percent used memory).</span></span> <span data-ttu-id="2b78a-120">Pour plus d’informations sur cette configuration et les mesures autres que le pourcentage de mémoire utilisée, consultez [cette documentation](../virtual-machines/linux/diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="2b78a-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

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

<span data-ttu-id="2b78a-121">Enfin, nous ajoutons un `autoscaleSettings` tooconfigure mise à l’échelle les ressources en fonction de ces mesures.</span><span class="sxs-lookup"><span data-stu-id="2b78a-121">Finally, we add an `autoscaleSettings` resource tooconfigure autoscale based on these metrics.</span></span> <span data-ttu-id="2b78a-122">Cette ressource a un `dependsOn` la clause qui fait référence à l’échelle de hello définie tooensure hello identiques existe avant de tenter de tooautoscale il.</span><span class="sxs-lookup"><span data-stu-id="2b78a-122">This resource has a `dependsOn` clause that references hello scale set tooensure that hello scale set exists before attempting tooautoscale it.</span></span> <span data-ttu-id="2b78a-123">Si vous choisissez un autre tooautoscale métrique sur, nous utiliseriez hello `counterSpecifier` à partir de la configuration de l’extension diagnostics hello comme hello `metricName` dans la configuration de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="2b78a-123">If we choose a different metric tooautoscale on, we would use hello `counterSpecifier` from hello diagnostics extension configuration as hello `metricName` in hello autoscale configuration.</span></span> <span data-ttu-id="2b78a-124">Pour plus d’informations sur la configuration de l’échelle automatique, consultez hello [mise à l’échelle les meilleures pratiques](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) et hello [documentation de référence API REST de Azure analyse](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b78a-124">For more information on autoscale configuration, see hello [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and hello [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

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





## <a name="next-steps"></a><span data-ttu-id="2b78a-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2b78a-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
