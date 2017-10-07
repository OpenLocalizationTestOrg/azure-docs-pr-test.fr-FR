---
title: "journaux aaaCollect à l’aide des Diagnostics de Azure | Documents Microsoft"
description: "Cet article décrit comment tooset des Diagnostics Windows Azure toocollect se connecte à partir d’un cluster Service Fabric s’exécutant dans Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Collecte des journaux avec Azure Diagnostics
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Lorsque vous exécutez un cluster Azure Service Fabric, il s’agit d’une bonne idée toocollect hello les journaux à partir de tous les nœuds hello dans un emplacement central. Ayant hello journaux dans un emplacement central vous permet d’analyser et résoudre les problèmes de votre cluster, ou dans les applications hello et les services exécutés dans ce cluster.

Tooupload d’une façon et collecter des journaux est l’extension de Diagnostics Windows Azure hello toouse, les téléchargements de journaux tooAzure stockage Azure Application Insights ou Azure Event Hubs. journaux de Hello ne sont pas utiles directement dans le stockage ou dans des concentrateurs d’événements. Mais vous pouvez utiliser un processus externe tooread hello d’événements à partir du stockage et les placer dans un produit tel que [Analytique de journal](../log-analytics/log-analytics-service-fabric.md) ou une autre solution d’analyse de journal. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) est fourni avec un service complet de recherche dans les journaux et d’analyse des données intégré.

## <a name="prerequisites"></a>Composants requis
Vous utilisez ces outils tooperform certaines opérations hello dans ce document :

* [Diagnostics Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (liés tooAzure Services de cloud computing a, mais les bonnes informations et des exemples)
* [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Applets de commande Azure Resource Manager](https://github.com/projectkudu/ARMClient)
* [Modèle Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a>Vous voudrez probablement toocollect des sources de journal
* **Les journaux de l’infrastructure de service**: émis à partir de hello plateforme toostandard suivi d’événements pour Windows (ETW) et EventSource des canaux. Il existe plusieurs types de journaux :
  * Les événements opérationnels : journaux pour les opérations qui hello Service Fabric effectue de la plateforme. Par exemple : la création d’applications et de services, les modifications d’état des nœuds et les informations de mise à niveau.
  * [Événements du modèle de programmation Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
  * [Événements du modèle de programmation Reliable Services](service-fabric-reliable-services-diagnostics.md)
* **Événements d’application**: événements émis à partir du code de votre service et l’écrit à l’aide de classe d’assistance de hello EventSource fournie dans les modèles de Visual Studio hello. Pour plus d’informations sur comment toowrite se connecte à partir de votre application, consultez [analyse et de diagnostiquer les services dans une installation de développement local machine](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Déployer l’extension de Diagnostics hello
Hello première étape de collecte de journaux est l’extension de Diagnostics toodeploy hello sur chacune des machines virtuelles de hello dans le cluster Service Fabric de hello. Hello, extension de diagnostic collecte des journaux sur chaque machine virtuelle et les charge compte de stockage toohello que vous spécifiez. étapes de Hello varient légèrement en fonction de que vous utilisez hello portail Azure ou Azure Resource Manager. également, les étapes de Hello varient en fonction de déploiement de hello fait partie de la création du cluster ou pour un cluster existe déjà. Examinez les étapes hello pour chaque scénario.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a>Déployer l’extension de Diagnostics hello dans le cadre de la création du cluster via le portail de hello
toodeploy hello Diagnostics extension toohello machines virtuelles dans le cluster hello dans le cadre de la création du cluster, vous utilisez Panneau de paramètres de Diagnostics hello illustré hello suivant l’image. tooenable Reliable Actors ou des Services fiables collecte d’événements, vérifiez que les tests de diagnostic est défini trop**sur** (paramètre par défaut de hello). Après avoir créé le cluster de hello, vous ne pouvez pas modifier ces paramètres à l’aide du portail de hello.

![Paramètres de Diagnostics Azure dans le portail hello pour la création du cluster](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

Bienvenue équipe de support Azure *requiert* prise en charge des journaux toohelp résoudre toutes les demandes de prise en charge que vous créez. Ces journaux sont collectés en temps réel et sont stockés dans un des comptes de stockage hello créés dans le groupe de ressources hello. paramètres de diagnostic Hello configurent les événements de niveau application. Ces événements sont notamment [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) événements, [des Services fiables](service-fabric-reliable-services-diagnostics.md) certains toobe d’événements de l’infrastructure de Service au niveau du système stockées dans le stockage Azure et les événements.

Produits tels que [Elasticsearch](https://www.elastic.co/guide/index.html) ou votre propre processus peuvent obtenir les événements de hello du compte de stockage hello. Il n’existe actuellement aucun moyen toofilter ou marié hello événements envoyés toohello table. Si vous n’implémentez pas tooremove un traitement des événements à partir de la table de hello, table de hello continue toogrow.

Lorsque vous créez un cluster à l’aide du portail de hello, nous recommandons vivement que vous téléchargez le modèle de hello **avant de cliquer sur OK** cluster hello de toocreate. Pour plus d’informations, consultez trop[configurer un cluster Service Fabric à l’aide d’un modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Vous aurez besoin des modifications apportées au modèle toomake hello plus tard, car vous ne pouvez pas apporter des modifications à l’aide du portail de hello.

Vous pouvez exporter des modèles à partir du portail de hello à l’aide de hello comme suit. Toutefois, ces modèles peuvent être toouse plus difficile, car ils peuvent avoir des valeurs null que les informations requises sont manquantes.

1. Ouvrez votre groupe de ressources.
2. Sélectionnez **paramètres** Panneau de paramètres toodisplay hello.
3. Sélectionnez **déploiements** Panneau de l’historique du déploiement toodisplay hello.
4. Sélectionnez un déploiement toodisplay hello les détails du déploiement de hello.
5. Sélectionnez **exporter le modèle** Panneau de modèle toodisplay hello.
6. Sélectionnez **enregistrer toofile** tooexport un fichier .zip qui contient le modèle de hello, paramètres et fichiers de PowerShell.

Une fois que vous exportez les fichiers hello, vous devez toomake une modification. Modifier le fichier de parameters.json hello et supprimer hello **adminPassword** élément. Cela entraîne une invite de mot de passe hello lors de l’exécution de script de déploiement hello. Lorsque vous exécutez le script de déploiement hello, vous pouvez avoir des valeurs de paramètre null toofix.

toouse hello téléchargé une configuration à tooupdate du modèle :

1. Extrayez hello contenu tooa dossier sur votre ordinateur local.
2. Modifier la nouvelle configuration hello contenu tooreflect hello.
3. Démarrez PowerShell et modifier le dossier toohello où vous avez extrait le contenu hello.
4. Exécutez **deploy.ps1** et renseignez les ID d’abonnement hello, nom de groupe de ressources hello (utilisez hello même configuration hello tooupdate du nom) et un nom unique de déploiement.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Déployer l’extension de Diagnostics hello dans le cadre de la création du cluster à l’aide du Gestionnaire de ressources Azure
toocreate un cluster à l’aide du Gestionnaire de ressources, vous devez modèle de gestionnaire de ressources du cluster complet configuration JSON toohello tooadd hello Diagnostics avant de créer le cluster de hello. Nous fournissons un modèle de gestionnaire de ressources de cluster de cinq-VM avec la configuration des Diagnostics ajoutée tooit dans le cadre de nos exemples de modèle de gestionnaire de ressources. Vous pouvez le voir à cet emplacement dans la galerie d’exemples de Azure hello : [cluster à cinq nœuds avec l’exemple de modèle de gestionnaire de ressources de diagnostic](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).

toosee hello Diagnostics des paramètres de modèle de gestionnaire de ressources hello, fichier de azuredeploy.json hello ouvert et recherchez **IaaSDiagnostics**. toocreate un cluster à l’aide de ce modèle, un select hello **déployer tooAzure** bouton disponible sur le lien précédent de hello.

Ou bien, vous pouvez télécharger l’exemple de gestionnaire de ressources hello, apporter des modifications tooit et créer un cluster avec le modèle modifié de hello à l’aide de hello `New-AzureRmResourceGroupDeployment` dans une fenêtre Azure PowerShell. Consultez hello suivant de code pour les paramètres hello que vous passez dans toohello commande. Pour plus d’informations sur la façon dont toodeploy une ressource de groupe à l’aide de PowerShell, voir l’article hello [déployer un groupe de ressources avec le modèle de gestionnaire de ressources Azure hello](../azure-resource-manager/resource-group-template-deploy.md).

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

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

## <a name="update-diagnostics-toocollect-health-and-load-events"></a>Mettre à jour les événements de contrôle d’intégrité et de charge de toocollect diagnostics

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

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a>Mettre à jour des Diagnostics toocollect et télécharger les journaux de nouveaux canaux EventSource
journaux de toocollect tooupdate Diagnostics à partir de nouveaux canaux EventSource qui représentent une nouvelle application que vous êtes sur toodeploy, effectuer hello même procédure que dans hello [section précédente](#deploywadarm) pour le programme d’installation de Diagnostics pour une existante cluster.

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

## <a name="next-steps"></a>Étapes suivantes
toounderstand plus en détail les événements que vous devez rechercher lors de la résolution des problèmes, consultez les événements de diagnostic hello émis pour [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) et [des Services fiables](service-fabric-reliable-services-diagnostics.md).

## <a name="related-articles"></a>Articles connexes
* [Découvrez comment les compteurs de performances toocollect ou journaux à l’aide de hello extension des Diagnostics](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Solution Service Fabric dans Log Analytics](../log-analytics/log-analytics-service-fabric.md)

