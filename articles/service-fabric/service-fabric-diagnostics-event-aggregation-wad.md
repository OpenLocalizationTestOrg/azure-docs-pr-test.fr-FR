---
title: "aaaAzure l’agrégation d’événements Service Fabric avec Windows Azure Diagnostics | Documents Microsoft"
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
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a>Agrégation et collecte d’événements à l’aide des diagnostics Windows Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Lorsque vous exécutez un cluster Azure Service Fabric, il s’agit d’une bonne idée toocollect hello les journaux à partir de tous les nœuds hello dans un emplacement central. Ayant hello journaux dans un emplacement central vous permet d’analyser et résoudre les problèmes de votre cluster, ou dans les applications hello et les services exécutés dans ce cluster.

Tooupload d’une façon et collecter des journaux est extension toouse hello Windows Azure Diagnostics (WAD), qui télécharge les journaux tooAzure stockage et est également hello option toosend journaux tooAzure Application Insights ou concentrateurs d’événements. Vous pouvez également utiliser un processus externe tooread hello d’événements à partir du stockage et les placer dans un produit de plateforme d’analyse, tels que [Analytique des journaux OMS](../log-analytics/log-analytics-service-fabric.md) ou une autre solution d’analyse de journal.

## <a name="prerequisites"></a>Composants requis
Ces outils sont utilisé tooperform certaines opérations hello dans ce document :

* [Diagnostics Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (liés tooAzure Services de cloud computing a, mais les bonnes informations et des exemples)
* [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Applets de commande Azure Resource Manager](https://github.com/projectkudu/ARMClient)
* [Modèle Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a>Sources de journaux et d’événements

### <a name="service-fabric-platform-events"></a>Événements de la plateforme Service Fabric
Comme indiqué dans [cet article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric configure vous avec quelques chaînes de journalisation, de laquelle hello canaux suivants sont facilement configurés avec WAD toosend analyse et aux diagnostics tooa stockage table de données ou Par ailleurs :
  * Les événements opérationnels : opérations de niveau supérieur qui hello Service Fabric effectue de la plateforme. Par exemple : la création d’applications et de services, les modifications d’état des nœuds et les informations de mise à niveau. Ces événements sont émis sous forme de journaux de suivi d’événements pour Windows (ETW)
  * [Événements du modèle de programmation Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
  * [Événements du modèle de programmation Reliable Services](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a>Événements liés aux applications
 Événements émis à partir du code de vos applications et services et écrites à l’aide de classe d’assistance de EventSource hello fournis Bonjour modèles Visual Studio. Pour plus d’informations sur comment toowrite EventSource se connecte à partir de votre application, consultez [analyse et de diagnostiquer les services dans une installation de développement local machine](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Déployer l’extension de Diagnostics hello
Hello première étape de collecte de journaux est l’extension de Diagnostics toodeploy hello sur chacune des machines virtuelles de hello dans le cluster Service Fabric de hello. Hello, extension de diagnostic collecte des journaux sur chaque machine virtuelle et les charge compte de stockage toohello que vous spécifiez. étapes de Hello varient légèrement en fonction de que vous utilisez hello portail Azure ou Azure Resource Manager. également, les étapes de Hello varient en fonction de déploiement de hello fait partie de la création du cluster ou pour un cluster existe déjà. Examinez les étapes hello pour chaque scénario.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a>Déployer l’extension de Diagnostics hello dans le cadre de la création du cluster via le portail Azure
toodeploy hello Diagnostics extension toohello machines virtuelles dans le cluster hello dans le cadre de la création du cluster, que vous utilisez le panneau de paramètres de Diagnostics de hello illustré dans hello suit l’image, assurez-vous que les tests de diagnostic est défini trop**sur** (paramètre par défaut de hello) . Après avoir créé le cluster de hello, vous ne pouvez pas modifier ces paramètres à l’aide du portail de hello.

![Paramètres de Diagnostics Azure dans le portail hello pour la création du cluster](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

Lorsque vous créez un cluster à l’aide du portail de hello, nous recommandons vivement que vous téléchargez le modèle de hello **avant de cliquer sur OK** cluster hello de toocreate. Pour plus d’informations, consultez trop[configurer un cluster Service Fabric à l’aide d’un modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Vous aurez besoin des modifications apportées au modèle toomake hello plus tard, car vous ne pouvez pas apporter des modifications à l’aide du portail de hello.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Déployer l’extension de Diagnostics hello dans le cadre de la création du cluster à l’aide du Gestionnaire de ressources Azure
toocreate un cluster à l’aide du Gestionnaire de ressources, vous devez modèle de gestionnaire de ressources du cluster complet configuration JSON toohello tooadd hello Diagnostics avant de créer le cluster de hello. Nous fournissons un modèle de gestionnaire de ressources de cluster de cinq-VM avec la configuration des Diagnostics ajoutée tooit dans le cadre de nos exemples de modèle de gestionnaire de ressources. Vous pouvez le voir à cet emplacement dans la galerie d’exemples de Azure hello : [cluster à cinq nœuds avec l’exemple de modèle de gestionnaire de ressources de diagnostic](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).

toosee hello Diagnostics des paramètres de modèle de gestionnaire de ressources hello, fichier de azuredeploy.json hello ouvert et recherchez **IaaSDiagnostics**. toocreate un cluster à l’aide de ce modèle, un select hello **déployer tooAzure** bouton disponible sur le lien précédent de hello.

Ou bien, vous pouvez télécharger l’exemple de gestionnaire de ressources hello, apporter des modifications tooit et créer un cluster avec le modèle modifié de hello à l’aide de hello `New-AzureRmResourceGroupDeployment` dans une fenêtre Azure PowerShell. Consultez hello suivant de code pour les paramètres hello que vous passez dans toohello commande. Pour plus d’informations sur la façon dont toodeploy une ressource de groupe à l’aide de PowerShell, voir l’article hello [déployer un groupe de ressources avec le modèle de gestionnaire de ressources Azure hello](../azure-resource-manager/resource-group-template-deploy.md).

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a>Déployer le cluster existant de hello Diagnostics extension tooan
Si vous avez un cluster existant n’ayant pas déployé de Diagnostics, ou si vous souhaitez toomodify une configuration existante, vous pouvez ajouter ou mettre à jour. Modifier le modèle de gestionnaire de ressources hello cluster existant de hello toocreate utilisés ou télécharger le modèle de hello à partir du portail hello comme décrit précédemment. Modifier le fichier de template.json de hello en effectuant hello tâches suivantes.

Ajouter un nouveau modèle de toohello de ressources de stockage en ajoutant la section de ressources toohello.

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

 Ensuite, ajoutez les paramètres toohello section juste après les définitions de compte de stockage hello, entre `supportLogStorageAccountName` et `vmNodeType0Name`. Remplacez le texte d’espace réservé hello *nom de compte de stockage ici* avec nom hello hello du compte de stockage.

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
Ensuite, mettez à jour hello `VirtualMachineProfile` section du fichier de template.json hello en ajoutant hello suivant le code dans le tableau d’extensions hello. Être tooadd vraiment une virgule au début de hello ou hello fin, selon lequel il est inséré.

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

Après avoir modifié le fichier de template.json hello comme décrit, republiez le modèle de gestionnaire de ressources de hello. Si le modèle de hello a été exporté, le fichier de deploy.ps1 hello en cours d’exécution republie modèle de hello. Après le déploiement, assurez-vous que **ProvisioningState** présente la valeur **Succeeded**.

## <a name="collect-health-and-load-events"></a>Collecter les événements d’intégrité et de charge

À partir de la version de hello 5.4 de l’infrastructure de Service, les événements de métrique d’intégrité et de charge sont disponibles pour la collection. Ces événements reflète les événements générés par le système de hello ou votre code à l’aide du contrôle d’intégrité hello ou charger les API de création de rapports tels que [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) ou [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Cela permet non seulement de consolider et de visualiser l’intégrité du système dans le temps, mais aussi de générer des alertes en fonction de certains événements d’intégrité et de charge. tooview ces événements dans l’Observateur d’événements Diagnostic de Visual Studio ajoutent « Microsoft-ServiceFabric:4:0x4000000000000008 « toohello la liste des fournisseurs ETW.

événements de hello toocollect, modifier tooinclude de modèle de gestionnaire de ressources hello

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

En commençant par la version de hello 5.7 de l’infrastructure de Service, [proxy inverse](service-fabric-reverseproxy.md) événements sont disponibles pour la collection.
Proxy inverse émet des événements dans deux canaux, une erreur contenante événements qui reflètent des échecs de traitement de demande et autres une contenant les événements détaillés de toutes les demandes de hello traitées au proxy inverse de hello hello. 

1. Collecter les événements d’erreur : tooview ces événements dans l’Observateur d’événements Diagnostic de Visual Studio ajoutent « Microsoft-ServiceFabric:4:0x4000000000000010 « toohello la liste des fournisseurs ETW.
événements de hello toocollect à partir de clusters Azure, modifier tooinclude de modèle de gestionnaire de ressources hello

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

2. Collecte toutes les demande le traitement des événements : Diagnostic Observateur d’événements dans Visual Studio, entrée hello Microsoft-ServiceFabric de mise à jour dans hello liste de fournisseurs ETW trop « Microsoft-ServiceFabric:4:0x4000000000000020 ».
Pour les clusters de Azure Service Fabric, modifiez tooinclude de modèle de gestionnaire de ressources hello

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
> Il est recommandé de toojudiciously activer la collecte les événements à partir de ce canal collecte tout le trafic via le proxy inverse hello et peut consommer rapidement la capacité de stockage.

Pour les clusters de Azure Service Fabric, les événements hello à partir de tous les nœuds de hello sont collectés et regroupés dans hello SystemEventTable.
Pour plus de résolution des problèmes d’événements de proxy inverse hello, consultez hello [proxy inverse diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).

## <a name="collect-from-new-eventsource-channels"></a>Collecter à partir de nouveaux canaux EventSource

journaux de toocollect tooupdate Diagnostics à partir de nouveaux canaux EventSource qui représentent une nouvelle application que vous êtes sur toodeploy, effectuez hello mêmes étapes comme décrit précédemment pour hello le programme d’installation de Diagnostics pour un cluster existant.

Mettre à jour hello `EtwEventSourceProviderConfiguration` section dans les entrées de hello template.json fichier tooadd pour hello nouveau EventSource canaux avant d’appliquer la configuration de hello mise à jour à l’aide de hello `New-AzureRmResourceGroupDeployment` commande PowerShell. nom de Hello de source d’événements hello est défini en tant que partie de votre code dans un fichier généré par Visual Studio de ServiceEventSource.cs hello.

Par exemple, si votre source d’événements est mon-Eventsource, ajoutez hello suivant des événements de code tooplace hello dans mon-Eventsource dans une table nommée MyDestinationTableName.

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

les compteurs de performances toocollect ou les journaux des événements, modifier le modèle de gestionnaire de ressources de hello à l’aide d’exemples hello dans [créer une machine virtuelle Windows avec l’analyse et de diagnostics à l’aide d’un modèle Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Ensuite, publier à nouveau modèle du Gestionnaire de ressources hello.

## <a name="collect-performance-counters"></a>Collecter des compteurs de performances

toocollect les métriques de performances de votre cluster, ajoutez tooyour de compteurs de performances hello « DiagnosticMonitorConfiguration de > WadCfg » dans le modèle de gestionnaire de ressources hello pour votre cluster. Consultez [Compteurs de performances de Service Fabric](service-fabric-diagnostics-event-generation-perf.md) pour plus d’informations sur les compteurs de performances que nous vous recommandons de collecter.

Par exemple, nous définir ici un compteur de performance, échantillonné toutes les 15 secondes (Cela peut être modifié et suit hello format de « PT\<temps >\<unité > », PT3M serait exemple toutes les trois minutes) et transférées toohello table de stockage approprié chaque minute.

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
  
Si vous utilisez un récepteur d’Application Insights, comme décrit dans la section hello ci-dessous et que vous souhaitez tooshow de ces métriques dans Application Insights, puis apportez que nom de récepteur tooadd hello dans hello « récepteurs » section comme indiqué ci-dessus. En outre, envisagez la création d’une table distincte de toosend vos compteurs de performances, afin qu’ils n’inutile out hello données provenant de hello autres canaux d’enregistrement que vous avez activé.


## <a name="send-logs-tooapplication-insights"></a>Envoi consigne tooApplication Insights

TooApplication de données de surveillance et de diagnostic Insights (AI) peut être envoyé dans le cadre de la configuration des diagnostics Windows AZURE hello. Si vous décidez toouse AI pour analyse des événements et la visualisation, lisez [analyse des événements et visualisation avec Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset d’un récepteur AI dans le cadre de votre « WadCfg ».

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez correctement configuré les diagnostics Azure, vous verrez les données de vos tables de stockage à partir de hello ETW et journaux d’EventSource. Si vous choisissez toouse OMS, Kibana ou autres données analytique et la visualisation des plates-formes qui n’est pas configuré directement dans le modèle de gestionnaire de ressources hello, assurez-vous que tooset plate-forme hello de tooread de votre choix dans les données de salutation à partir de ces tables de stockage. Cette opération relativement simple pour OMS est expliquée dans [Analyse d’événements et de journaux via OMS](service-fabric-diagnostics-event-analysis-oms.md). Application Insights est un peu d’un cas spécial en ce sens, car il peut être configuré en tant que partie de la configuration de l’extension Diagnostics hello, par conséquent, consultez le toohello [approprié](service-fabric-diagnostics-event-analysis-appinsights.md) si vous choisissez toouse AI.

>[!NOTE]
>Il n’existe actuellement aucun moyen toofilter ou marié hello événements envoyés toohello table. Si vous n’implémentez pas tooremove un traitement des événements à partir de la table de hello, table de hello continue toogrow. Actuellement, est un exemple d’un service de nettoyage de données en cours d’exécution dans hello [exemple de surveillance](https://github.com/Azure-Samples/service-fabric-watchdog-service), et il est recommandé d’écrire un pour vous-même, sauf s’il existe une bonne raison vous journaux toostore dépasse un laps de temps jour 30 ou 90.

* [Découvrez comment les compteurs de performances toocollect ou journaux à l’aide de hello extension des Diagnostics](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Analyse et visualisation d’événements avec Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)
* [Analyse et visualisation d’événements avec OMS](service-fabric-diagnostics-event-analysis-oms.md)