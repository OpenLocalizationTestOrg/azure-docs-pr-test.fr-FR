---
title: "Utiliser la mise à l’échelle automatique Azure avec des mesures invitées dans un modèle de groupe identique Linux | Microsoft Docs"
description: "Découvrez comment effectuer la mise à l’échelle automatique en utilisant des mesures invitées dans un modèle de groupe de machines virtuelles identiques Linux"
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
ms.openlocfilehash: ac0bbb4dbfccca3f3fc31526aeff11afe55d44be
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="6ed45-103">Mise à l’échelle automatique en utilisant des mesures invitées dans un modèle de groupe identique Linux</span><span class="sxs-lookup"><span data-stu-id="6ed45-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="6ed45-104">Dans Azure, il existe deux types de mesures collectées sur les machines virtuelles et les groupes identiques : certaines proviennent de la machine virtuelle hôte et d’autres de la machine virtuelles invitée.</span><span class="sxs-lookup"><span data-stu-id="6ed45-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from the host VM and others come from the guest VM.</span></span> <span data-ttu-id="6ed45-105">Les mesures hôtes ne requièrent aucune configuration supplémentaire, car elles sont collectées par la machine virtuelle hôte, tandis que les mesures invitées nécessitent d’installer [l’extension Windows Azure Diagnostics](../virtual-machines/windows/extensions-diagnostics-template.md) ou [l’extension Linux Azure Diagnostics](../virtual-machines/linux/diagnostic-extension.md) sur la machine virtuelle invitée.</span><span class="sxs-lookup"><span data-stu-id="6ed45-105">Host metrics do not require additional setup because they are collected by the host VM, whereas guest metrics require us to install the [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or the [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in the guest VM.</span></span> <span data-ttu-id="6ed45-106">L’utilisation des mesures invitées à la place des mesures hôtes est courante, car les premières sont plus variées que les dernières.</span><span class="sxs-lookup"><span data-stu-id="6ed45-106">One common reason to use guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="6ed45-107">Les mesures de consommation de la mémoire, notamment, ne sont disponibles que via les mesures invitées.</span><span class="sxs-lookup"><span data-stu-id="6ed45-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="6ed45-108">Les mesures hôtes prises en charge sont répertoriées [ici](../monitoring-and-diagnostics/monitoring-supported-metrics.md), et les mesures invitées couramment utilisées [ici](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="6ed45-108">The supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="6ed45-109">Cet article explique comment modifier le [modèle de groupe identique viable minimal](./virtual-machine-scale-sets-mvss-start.md) pour qu’il utilise des règles de mise à l’échelle automatique en fonction des mesures invitées des groupes identiques Linux.</span><span class="sxs-lookup"><span data-stu-id="6ed45-109">This article shows how to modify the [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) to use autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-the-template-definition"></a><span data-ttu-id="6ed45-110">Modifier la définition du modèle</span><span class="sxs-lookup"><span data-stu-id="6ed45-110">Change the template definition</span></span>

<span data-ttu-id="6ed45-111">Notre modèle de groupe identique viable minimal peut être consulté [ici](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json) et notre modèle de déploiement de groupe identique Linux avec mise à l’échelle automatique basée sur des invités peut être consulté [ici](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="6ed45-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying the Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="6ed45-112">Examinons le différentiel utilisé pour créer ce modèle (`git diff minimum-viable-scale-set existing-vnet`), élément par élément :</span><span class="sxs-lookup"><span data-stu-id="6ed45-112">Let's examine the diff used to create this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="6ed45-113">Ajoutons tout d’abord les paramètres de `storageAccountName` et `storageAccountSasToken`.</span><span class="sxs-lookup"><span data-stu-id="6ed45-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="6ed45-114">L’agent de diagnostic stocke les données de mesure dans une [table](../cosmos-db/table-storage-how-to-use-dotnet.md) de ce compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6ed45-114">The diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="6ed45-115">À compter de la version 3.0 de l’agent de diagnostic Linux, l’utilisation d’une clé d’accès de stockage n’est plus prise en charge.</span><span class="sxs-lookup"><span data-stu-id="6ed45-115">As of the Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="6ed45-116">Nous devons utiliser un [jeton SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="6ed45-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

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

<span data-ttu-id="6ed45-117">Ensuite, nous modifions le groupe identique `extensionProfile` pour y inclure l’extension de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="6ed45-117">Next, we modify the scale set `extensionProfile` to include the diagnostics extension.</span></span> <span data-ttu-id="6ed45-118">Dans cette configuration, nous spécifions l’ID de ressource du groupe identique à partir duquel collecter les mesures, ainsi que le compte de stockage et le jeton SAP à utiliser pour les stocker.</span><span class="sxs-lookup"><span data-stu-id="6ed45-118">In this configuration, we specify the resource ID of the scale set to collect metrics from, as well as the storage account and SAS token to use to store the metrics.</span></span> <span data-ttu-id="6ed45-119">Nous spécifions également la fréquence d’agrégation des mesures (dans ce cas, chaque minute) et les mesures à suivre (dans ce cas, le pourcentage de mémoire utilisée).</span><span class="sxs-lookup"><span data-stu-id="6ed45-119">We also specify how frequently the metrics are aggregated (in this case every minute) and which metrics to track (in this case percent used memory).</span></span> <span data-ttu-id="6ed45-120">Pour plus d’informations sur cette configuration et les mesures autres que le pourcentage de mémoire utilisée, consultez [cette documentation](../virtual-machines/linux/diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="6ed45-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

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

<span data-ttu-id="6ed45-121">Enfin, nous ajoutons une ressource `autoscaleSettings` pour configurer la mise à l’échelle automatique en fonction de ces mesures.</span><span class="sxs-lookup"><span data-stu-id="6ed45-121">Finally, we add an `autoscaleSettings` resource to configure autoscale based on these metrics.</span></span> <span data-ttu-id="6ed45-122">Cette ressource contient une clause `dependsOn` qui fait référence au groupe identique pour s’assurer que ce groupe existe avant d’essayer de le soumettre à une mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="6ed45-122">This resource has a `dependsOn` clause that references the scale set to ensure that the scale set exists before attempting to autoscale it.</span></span> <span data-ttu-id="6ed45-123">Pour baser la mise à l’échelle automatique sur une autre mesure, nous utiliserions la propriété `counterSpecifier` de la configuration de l’extension de diagnostic en tant que propriété `metricName` dans la configuration de la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="6ed45-123">If we choose a different metric to autoscale on, we would use the `counterSpecifier` from the diagnostics extension configuration as the `metricName` in the autoscale configuration.</span></span> <span data-ttu-id="6ed45-124">Pour plus d’informations sur la configuration de la mise à l’échelle automatique, consultez les [meilleures pratiques en matière de mise à l’échelle automatique](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) et la [documentation de référence de l’API REST Azure Monitor](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ed45-124">For more information on autoscale configuration, see the [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and the [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

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





## <a name="next-steps"></a><span data-ttu-id="6ed45-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6ed45-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
