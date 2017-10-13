---
title: "Agrégation d’événements Azure Service Fabric à l’aide des diagnostics Windows Azure | Microsoft Docs"
description: "Découvrez comment agréger et collecter des événements à l’aide des diagnostics Windows Azure pour la surveillance et le diagnostic de clusters Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 5773361fdec4cb8ee54fa2856f6aa969d5dac4e9
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a>Agrégation et collecte d’événements à l’aide des diagnostics Windows Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Lorsque vous exécutez un cluster Service Fabric dans Azure, il peut être intéressant de collecter les journaux de tous les nœuds pour les regrouper dans un emplacement central. La centralisation des journaux vous permet d’analyser et résoudre les problèmes que vous pourriez rencontrer dans votre cluster ou dans les applications et services exécutés dans ce cluster.

Pour télécharger et collecter des journaux, vous pouvez utiliser l’extension Windows Azure Diagnostics (WAD), qui télécharge les journaux dans Azure Storage, ou envoyer les journaux à Azure Application Insights ou à des concentrateurs d’événements. Vous pouvez également utiliser un processus externe pour lire les événements à partir du stockage et les placer dans une plateforme d’analyse, par exemple [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) ou une autre solution d’analyse de journaux.

## <a name="prerequisites"></a>Composants requis
Ces outils sont utilisés pour effectuer certaines opérations de ce document :

* [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (page en lien avec Azure Cloud Services, mais qui contient des informations et des exemples pertinents)
* [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Applets de commande Azure Resource Manager](https://github.com/projectkudu/ARMClient)
* [Modèle Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a>Sources de journaux et d’événements

### <a name="service-fabric-platform-events"></a>Événements de la plateforme Service Fabric
Comme indiqué dans [cet article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric inclut quelques canaux de journalisation prêts à l’emploi, notamment les canaux suivants, facilement configurés à l’aide des diagnostics Windows Azure pour envoyer les données de surveillance et de diagnostic à une table de stockage ou un autre emplacement :
  * Événements opérationnels : opérations de niveau supérieur effectuées par la plateforme Service Fabric. Par exemple : la création d’applications et de services, les modifications d’état des nœuds et les informations de mise à niveau. Ces événements sont émis sous forme de journaux de suivi d’événements pour Windows (ETW)
  * [Événements du modèle de programmation Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
  * [Événements du modèle de programmation Reliable Services](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a>Événements liés aux applications
 Événements émis à partir du code de vos applications et services et écrits à l’aide de la classe d’assistance EventSource fournie dans les modèles Visual Studio. Pour plus d’informations sur la façon d’écrire des journaux EventSource à partir de votre application, consultez [Surveiller et diagnostiquer des services dans une configuration de développement de machine locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-the-diagnostics-extension"></a>Déployer l’extension Diagnostics
La première étape de la collecte de journaux consiste à déployer l’extension Diagnostics sur chaque machine virtuelle du cluster Service Fabric. Cette extension collecte les journaux sur chaque machine virtuelle et les charge dans le compte de stockage que vous spécifiez. Les étapes varient légèrement selon que vous utilisez le portail Azure ou Azure Resource Manager. Les étapes varient également selon que le déploiement fait partie de la création du cluster ou est effectué pour un cluster qui existe déjà. Examinons les différentes étapes pour chaque scénario.

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a>Déployer l’extension Diagnostics dans le cadre de la création d’un cluster via le portail Azure
Pour déployer l’extension Diagnostics sur les machines virtuelles du cluster dans le cadre de la création d’un cluster, utilisez le panneau des paramètres Diagnostics affiché dans l’image suivante - Assurez-vous que l’option Diagnostics est définie sur **On** (paramètre par défaut). Une fois le cluster créé, vous ne pouvez plus modifier ces paramètres à l’aide du portail.

![Paramètres Azure Diagnostics dans le portail pour la création d’un cluster](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

Lorsque vous créez un cluster à l’aide du portail, nous vous recommandons vivement de télécharger le modèle **avant de cliquer sur OK** pour créer le cluster. Pour plus de détails, voir [Configurer un cluster Service Fabric à l’aide d’un modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Vous aurez besoin du modèle pour pouvoir apporter des modifications ultérieurement, car vous ne pouvez effectuer aucune modification à l’aide du portail.

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Déploiement de l’extension Diagnostics dans le cadre de la création d’un cluster via Azure Resource Manager
Pour créer un cluster à l’aide de Resource Manager, vous devez ajouter le fichier de configuration Diagnostics JSON au modèle Resource Manager du cluster complet avant de créer le cluster. Nous fournissons un exemple de modèle Resource Manager de cluster à cinq machines virtuelles avec la configuration Diagnostics ajoutée dans le cadre de nos exemples de modèle Resource Manager. Vous pouvez le voir à cet emplacement dans la galerie d’exemples d’Azure : [cluster à cinq nœuds avec exemple de modèle Diagnostics Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).

Pour voir les paramètres de diagnostic dans le modèle Resource Manager, ouvrez le fichier azuredeploy.json et recherchez **IaaSDiagnostics**. Pour créer un cluster à l’aide de ce modèle, cliquez sur le bouton **Déployer sur Azure**, disponible via le lien précédent.

Vous pouvez également télécharger l’exemple Resource Manager, y apporter des modifications et créer un cluster à partir du modèle modifié en utilisant la commande `New-AzureRmResourceGroupDeployment` dans une fenêtre Azure PowerShell. Consultez le code suivant pour les paramètres que vous passez à la commande. Pour plus d’informations sur le déploiement d’un groupe de ressources à l’aide de PowerShell, consultez l’article [Déployer un groupe de ressources avec un modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a>Déployer l’extension Diagnostics sur un cluster existant
Si Diagnostics n’est pas déployé sur l’un de vos clusters existants ou que vous souhaitez modifier une configuration existante, vous pouvez l’ajouter ou la mettre à jour. Modifiez le modèle Resource Manager utilisé pour créer le cluster existant ou téléchargez le modèle sur le portail, comme décrit ci-dessus. Modifiez le fichier template.json en effectuant les opérations suivantes.

Ajouter une ressource de stockage au modèle en l’ajoutant à la section de ressources.

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 Ensuite, ajoutez la section parameters juste après les définitions de compte de stockage, entre `supportLogStorageAccountName` et `vmNodeType0Name`. Remplacez l’espace réservé *nom du compte de stockage* par le nom du compte de stockage.

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for the application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for the storage account that contains application diagnostics data from the cluster"
      }
    },
```
Mettez ensuite à jour la section `VirtualMachineProfile` du fichier template.json en ajoutant le code suivant dans le tableau extensions. N’oubliez pas d’ajouter une virgule au début ou à la fin, en fonction de l’emplacement d’insertion.

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

Après avoir modifié le fichier template.json comme décrit, republiez le modèle Resource Manager. Si le modèle a été exporté, exécutez le fichier deploy.ps1 pour republier le modèle. Après le déploiement, assurez-vous que **ProvisioningState** présente la valeur **Succeeded**.

## <a name="collect-health-and-load-events"></a>Collecter les événements d’intégrité et de charge

Depuis la version 5.4 de Service Fabric, il est possible de collecter les événements liés aux mesures d’intégrité et de charge. Ces événements reflètent les événements générés par le système ou votre code à l’aide d’API de création de rapports d’intégrité ou de charge comme [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) ou [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Cela permet non seulement de consolider et de visualiser l’intégrité du système dans le temps, mais aussi de générer des alertes en fonction de certains événements d’intégrité et de charge. Pour afficher ces événements dans la visionneuse d’événements de diagnostic de Visual Studio, ajoutez « Microsoft-ServiceFabric:4:0x4000000000000008 » à la liste des fournisseurs ETW.

Pour collecter les événements, modifiez le modèle Resource Manager de manière à inclure ce qui suit :

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="collect-reverse-proxy-events"></a>Collecter des événements de proxy inverse

Depuis la publication de Service Fabric version 5.7, il est possible de collecter des événements liés au [proxy inverse](service-fabric-reverseproxy.md).
Le proxy inverse émet des événements vers deux canaux, l’un contenant les événements d’erreur reflétant les échecs de traitement des demandes, et l’autre contenant les événements détaillés concernant toutes les demandes traitées au niveau du proxy inverse. 

1. Collecter des événements d’erreur : pour afficher ces événements dans l’observateur d’événements de diagnostic de Visual Studio, ajoutez « Microsoft-ServiceFabric:4:0x4000000000000010 » à la liste des fournisseurs ETW.
Pour collecter les événements des clusters Azure, modifiez le modèle Resource Manager de manière à inclure ce qui suit :

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. Collecter tous les événements de traitement des demandes : dans l’observateur d’événements de diagnostic de Visual Studio, remplacez l’entrée « Microsoft-ServiceFabric » par « Microsoft-ServiceFabric:4:0x4000000000000020 » dans la liste des fournisseurs ETW.
Pour les clusters Azure Service Fabric, modifiez le modèle Resource Manager de manière à inclure ce qui suit :

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> Faites attention lorsque vous activez la collecte des événements provenant de ce canal, car cela va collecter tout le trafic via le proxy inverse et consommer rapidement la capacité de stockage.

Pour les clusters Azure Service Fabric, les événements de tous les nœuds sont collectés et agrégés dans SystemEventTable.
Pour obtenir des solutions de dépannage détaillées concernant les événements de proxy inverse, consultez ce [guide de diagnostic pour le proxy inverse](service-fabric-reverse-proxy-diagnostics.md).

## <a name="collect-from-new-eventsource-channels"></a>Collecter à partir de nouveaux canaux EventSource

Pour mettre à jour Diagnostics afin de collecter les journaux de nouveaux canaux EventSource représentant une nouvelle application que vous êtes sur le point de déployer, effectuez les mêmes étapes que précédemment pour le programme d’installation de Diagnostics d’un cluster existant.

Mettez à jour la section `EtwEventSourceProviderConfiguration` dans le fichier template.json pour ajouter des entrées pour les nouveaux canaux EventSource avant d’appliquer la mise à jour de la configuration à l’aide de la commande PowerShell `New-AzureRmResourceGroupDeployment`. Le nom de la source de l’événement est défini dans le cadre de votre code dans le fichier ServiceEventSource.cs généré par Visual Studio.

Par exemple, si votre source d’événements est nommée My-Eventsource, ajoutez le code suivant pour placer les événements de My-Eventsource dans une table nommée MyDestinationTableName.

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

Pour collecter des compteurs de performances ou des journaux d’événements, modifiez le modèle Resource Manager en utilisant les exemples fournis dans [Créer une machine virtuelle Windows avec des fonctionnalités de surveillance et de diagnostics à l’aide d’un modèle Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Republiez ensuite le modèle Resource Manager.

## <a name="collect-performance-counters"></a>Collecter des compteurs de performances

Pour collecter les métriques de performances de votre cluster, ajoutez les compteurs de performances à « WadCfg > DiagnosticMonitorConfiguration » dans le modèle Resource Manager de votre cluster. Consultez [Compteurs de performances de Service Fabric](service-fabric-diagnostics-event-generation-perf.md) pour plus d’informations sur les compteurs de performances que nous vous recommandons de collecter.

Par exemple, nous définissons ici un compteur de performances, échantillonné toutes les 15 secondes (cette valeur peut être modifiée et adopte le format « PT\<temps>\<unité> », par exemple, PT3M crée un échantillon toutes les trois minutes), puis transféré chaque minute vers la table de stockage correspondante.

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
Si vous utilisez un récepteur Application Insights, comme décrit dans la section ci-dessous, et souhaitez afficher ces mesures dans Application Insights, assurez-vous d’ajouter le nom du récepteur dans la section « récepteurs » comme indiqué ci-dessus. Vous pouvez par ailleurs créer une table séparée vers laquelle envoyer vos compteurs de performances, pour éviter que cette table utilise les données provenant d’autres canaux de journalisation que vous avez activés.


## <a name="send-logs-to-application-insights"></a>Envoyer les journaux à Application Insights

Les données de surveillance et de diagnostic peuvent être envoyées à Application Insights (AI) dans le cadre de la configuration des diagnostics Windows Azure. Si vous décidez d’utiliser AI pour l’analyse et la visualisation des événements, lisez [Analyse et visualisation des événements avec Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) pour configurer un récepteur AI dans le cadre de votre « WadCfg ».

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez correctement configuré les diagnostics Azure, vous verrez les données de vos tables de stockage dans les journaux ETW et EventSource. Si vous choisissez d’utiliser OMS, Kibana ou une autre plateforme d’analyse et de visualisation des données qui n’est pas directement configurée dans le modèle Resource Manager, veillez à configurer la plateforme de votre choix pour lire les données à partir de ces tables de stockage. Cette opération relativement simple pour OMS est expliquée dans [Analyse d’événements et de journaux via OMS](service-fabric-diagnostics-event-analysis-oms.md). L’utilisation d’Application Insights est un peu plus compliquée ici, car il peut être configuré en tant que partie de la configuration de l’extension Diagnostics. Reportez-vous par conséquent à l[’article approprié](service-fabric-diagnostics-event-analysis-appinsights.md) si vous choisissez d’utiliser AI.

>[!NOTE]
>Il n’existe actuellement aucun moyen de filtrer ou de nettoyer les événements qui sont envoyés à la table. Si vous n’implémentez aucun processus de suppression des événements de la table, la table continuera à croître. Un exemple de service de nettoyage de données en cours d’exécution est inclus avec l[’échantillon Watchdog](https://github.com/Azure-Samples/service-fabric-watchdog-service), et il est recommandé d’en écrire un vous-même, sauf s’il existe une bonne raison de stocker les journaux au-delà de 30 ou 90 jours.

* [Découvrez comment collecter des compteurs de performances ou des journaux à l’aide de l’extension Diagnostics](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Analyse et visualisation d’événements avec Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)
* [Analyse et visualisation d’événements avec OMS](service-fabric-diagnostics-event-analysis-oms.md)