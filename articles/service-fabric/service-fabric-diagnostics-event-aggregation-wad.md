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
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="1f1b4-103">Agrégation et collecte d’événements à l’aide des diagnostics Windows Azure</span><span class="sxs-lookup"><span data-stu-id="1f1b4-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f1b4-104">Windows</span><span class="sxs-lookup"><span data-stu-id="1f1b4-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="1f1b4-105">Linux</span><span class="sxs-lookup"><span data-stu-id="1f1b4-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="1f1b4-106">Lorsque vous exécutez un cluster Azure Service Fabric, il s’agit d’une bonne idée toocollect hello les journaux à partir de tous les nœuds hello dans un emplacement central.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="1f1b4-107">Ayant hello journaux dans un emplacement central vous permet d’analyser et résoudre les problèmes de votre cluster, ou dans les applications hello et les services exécutés dans ce cluster.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="1f1b4-108">Tooupload d’une façon et collecter des journaux est extension toouse hello Windows Azure Diagnostics (WAD), qui télécharge les journaux tooAzure stockage et est également hello option toosend journaux tooAzure Application Insights ou concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-108">One way tooupload and collect logs is toouse hello Windows Azure Diagnostics (WAD) extension, which uploads logs tooAzure Storage, and also has hello option toosend logs tooAzure Application Insights or Event Hubs.</span></span> <span data-ttu-id="1f1b4-109">Vous pouvez également utiliser un processus externe tooread hello d’événements à partir du stockage et les placer dans un produit de plateforme d’analyse, tels que [Analytique des journaux OMS](../log-analytics/log-analytics-service-fabric.md) ou une autre solution d’analyse de journal.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-109">You can also use an external process tooread hello events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f1b4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1f1b4-110">Prerequisites</span></span>
<span data-ttu-id="1f1b4-111">Ces outils sont utilisé tooperform certaines opérations hello dans ce document :</span><span class="sxs-lookup"><span data-stu-id="1f1b4-111">These tools are used tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="1f1b4-112">[Diagnostics Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (liés tooAzure Services de cloud computing a, mais les bonnes informations et des exemples)</span><span class="sxs-lookup"><span data-stu-id="1f1b4-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="1f1b4-113">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1f1b4-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="1f1b4-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f1b4-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="1f1b4-115">Applets de commande Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1f1b4-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="1f1b4-116">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1f1b4-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="1f1b4-117">Sources de journaux et d’événements</span><span class="sxs-lookup"><span data-stu-id="1f1b4-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="1f1b4-118">Événements de la plateforme Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1f1b4-118">Service Fabric platform events</span></span>
<span data-ttu-id="1f1b4-119">Comme indiqué dans [cet article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric configure vous avec quelques chaînes de journalisation, de laquelle hello canaux suivants sont facilement configurés avec WAD toosend analyse et aux diagnostics tooa stockage table de données ou Par ailleurs :</span><span class="sxs-lookup"><span data-stu-id="1f1b4-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which hello following channels are easily configured with WAD toosend monitoring and diagnostics data tooa storage table or elsewhere:</span></span>
  * <span data-ttu-id="1f1b4-120">Les événements opérationnels : opérations de niveau supérieur qui hello Service Fabric effectue de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-120">Operational events: higher-level operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="1f1b4-121">Par exemple : la création d’applications et de services, les modifications d’état des nœuds et les informations de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="1f1b4-122">Ces événements sont émis sous forme de journaux de suivi d’événements pour Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="1f1b4-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * [<span data-ttu-id="1f1b4-123">Événements du modèle de programmation Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="1f1b4-123">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="1f1b4-124">Événements du modèle de programmation Reliable Services</span><span class="sxs-lookup"><span data-stu-id="1f1b4-124">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a><span data-ttu-id="1f1b4-125">Événements liés aux applications</span><span class="sxs-lookup"><span data-stu-id="1f1b4-125">Application events</span></span>
 <span data-ttu-id="1f1b4-126">Événements émis à partir du code de vos applications et services et écrites à l’aide de classe d’assistance de EventSource hello fournis Bonjour modèles Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-126">Events emitted from your applications' and services' code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="1f1b4-127">Pour plus d’informations sur comment toowrite EventSource se connecte à partir de votre application, consultez [analyse et de diagnostiquer les services dans une installation de développement local machine](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="1f1b4-127">For more information on how toowrite EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="1f1b4-128">Déployer l’extension de Diagnostics hello</span><span class="sxs-lookup"><span data-stu-id="1f1b4-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="1f1b4-129">Hello première étape de collecte de journaux est l’extension de Diagnostics toodeploy hello sur chacune des machines virtuelles de hello dans le cluster Service Fabric de hello.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="1f1b4-130">Hello, extension de diagnostic collecte des journaux sur chaque machine virtuelle et les charge compte de stockage toohello que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="1f1b4-131">étapes de Hello varient légèrement en fonction de que vous utilisez hello portail Azure ou Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="1f1b4-132">également, les étapes de Hello varient en fonction de déploiement de hello fait partie de la création du cluster ou pour un cluster existe déjà.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="1f1b4-133">Examinez les étapes hello pour chaque scénario.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="1f1b4-134">Déployer l’extension de Diagnostics hello dans le cadre de la création du cluster via le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1f1b4-134">Deploy hello Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="1f1b4-135">toodeploy hello Diagnostics extension toohello machines virtuelles dans le cluster hello dans le cadre de la création du cluster, que vous utilisez le panneau de paramètres de Diagnostics de hello illustré dans hello suit l’image, assurez-vous que les tests de diagnostic est défini trop**sur** (paramètre par défaut de hello) .</span><span class="sxs-lookup"><span data-stu-id="1f1b4-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image - ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="1f1b4-136">Après avoir créé le cluster de hello, vous ne pouvez pas modifier ces paramètres à l’aide du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-136">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Paramètres de Diagnostics Azure dans le portail hello pour la création du cluster](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="1f1b4-138">Lorsque vous créez un cluster à l’aide du portail de hello, nous recommandons vivement que vous téléchargez le modèle de hello **avant de cliquer sur OK** cluster hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-138">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="1f1b4-139">Pour plus d’informations, consultez trop[configurer un cluster Service Fabric à l’aide d’un modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="1f1b4-139">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="1f1b4-140">Vous aurez besoin des modifications apportées au modèle toomake hello plus tard, car vous ne pouvez pas apporter des modifications à l’aide du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-140">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="1f1b4-141">Déployer l’extension de Diagnostics hello dans le cadre de la création du cluster à l’aide du Gestionnaire de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="1f1b4-141">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="1f1b4-142">toocreate un cluster à l’aide du Gestionnaire de ressources, vous devez modèle de gestionnaire de ressources du cluster complet configuration JSON toohello tooadd hello Diagnostics avant de créer le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-142">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="1f1b4-143">Nous fournissons un modèle de gestionnaire de ressources de cluster de cinq-VM avec la configuration des Diagnostics ajoutée tooit dans le cadre de nos exemples de modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="1f1b4-144">Vous pouvez le voir à cet emplacement dans la galerie d’exemples de Azure hello : [cluster à cinq nœuds avec l’exemple de modèle de gestionnaire de ressources de diagnostic](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span><span class="sxs-lookup"><span data-stu-id="1f1b4-144">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="1f1b4-145">toosee hello Diagnostics des paramètres de modèle de gestionnaire de ressources hello, fichier de azuredeploy.json hello ouvert et recherchez **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-145">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="1f1b4-146">toocreate un cluster à l’aide de ce modèle, un select hello **déployer tooAzure** bouton disponible sur le lien précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-146">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="1f1b4-147">Ou bien, vous pouvez télécharger l’exemple de gestionnaire de ressources hello, apporter des modifications tooit et créer un cluster avec le modèle modifié de hello à l’aide de hello `New-AzureRmResourceGroupDeployment` dans une fenêtre Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-147">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="1f1b4-148">Consultez hello suivant de code pour les paramètres hello que vous passez dans toohello commande.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-148">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="1f1b4-149">Pour plus d’informations sur la façon dont toodeploy une ressource de groupe à l’aide de PowerShell, voir l’article hello [déployer un groupe de ressources avec le modèle de gestionnaire de ressources Azure hello](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1f1b4-149">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="1f1b4-150">Déployer le cluster existant de hello Diagnostics extension tooan</span><span class="sxs-lookup"><span data-stu-id="1f1b4-150">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="1f1b4-151">Si vous avez un cluster existant n’ayant pas déployé de Diagnostics, ou si vous souhaitez toomodify une configuration existante, vous pouvez ajouter ou mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="1f1b4-152">Modifier le modèle de gestionnaire de ressources hello cluster existant de hello toocreate utilisés ou télécharger le modèle de hello à partir du portail hello comme décrit précédemment.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-152">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="1f1b4-153">Modifier le fichier de template.json de hello en effectuant hello tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-153">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="1f1b4-154">Ajouter un nouveau modèle de toohello de ressources de stockage en ajoutant la section de ressources toohello.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-154">Add a new storage resource toohello template by adding toohello resources section.</span></span>

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

 <span data-ttu-id="1f1b4-155">Ensuite, ajoutez les paramètres toohello section juste après les définitions de compte de stockage hello, entre `supportLogStorageAccountName` et `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-155">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="1f1b4-156">Remplacez le texte d’espace réservé hello *nom de compte de stockage ici* avec nom hello hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-156">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

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
<span data-ttu-id="1f1b4-157">Ensuite, mettez à jour hello `VirtualMachineProfile` section du fichier de template.json hello en ajoutant hello suivant le code dans le tableau d’extensions hello.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-157">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="1f1b4-158">Être tooadd vraiment une virgule au début de hello ou hello fin, selon lequel il est inséré.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-158">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="1f1b4-159">Après avoir modifié le fichier de template.json hello comme décrit, republiez le modèle de gestionnaire de ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-159">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="1f1b4-160">Si le modèle de hello a été exporté, le fichier de deploy.ps1 hello en cours d’exécution republie modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-160">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="1f1b4-161">Après le déploiement, assurez-vous que **ProvisioningState** présente la valeur **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="1f1b4-162">Collecter les événements d’intégrité et de charge</span><span class="sxs-lookup"><span data-stu-id="1f1b4-162">Collect health and load events</span></span>

<span data-ttu-id="1f1b4-163">À partir de la version de hello 5.4 de l’infrastructure de Service, les événements de métrique d’intégrité et de charge sont disponibles pour la collection.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-163">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="1f1b4-164">Ces événements reflète les événements générés par le système de hello ou votre code à l’aide du contrôle d’intégrité hello ou charger les API de création de rapports tels que [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) ou [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f1b4-164">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="1f1b4-165">Cela permet non seulement de consolider et de visualiser l’intégrité du système dans le temps, mais aussi de générer des alertes en fonction de certains événements d’intégrité et de charge.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="1f1b4-166">tooview ces événements dans l’Observateur d’événements Diagnostic de Visual Studio ajoutent « Microsoft-ServiceFabric:4:0x4000000000000008 « toohello la liste des fournisseurs ETW.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-166">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="1f1b4-167">événements de hello toocollect, modifier tooinclude de modèle de gestionnaire de ressources hello</span><span class="sxs-lookup"><span data-stu-id="1f1b4-167">toocollect hello events, modify hello Resource Manager template tooinclude</span></span>

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

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="1f1b4-168">Collecter des événements de proxy inverse</span><span class="sxs-lookup"><span data-stu-id="1f1b4-168">Collect reverse proxy events</span></span>

<span data-ttu-id="1f1b4-169">En commençant par la version de hello 5.7 de l’infrastructure de Service, [proxy inverse](service-fabric-reverseproxy.md) événements sont disponibles pour la collection.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-169">Starting with hello 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="1f1b4-170">Proxy inverse émet des événements dans deux canaux, une erreur contenante événements qui reflètent des échecs de traitement de demande et autres une contenant les événements détaillés de toutes les demandes de hello traitées au proxy inverse de hello hello.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and hello other one containing verbose events about all hello requests processed at hello reverse proxy.</span></span> 

1. <span data-ttu-id="1f1b4-171">Collecter les événements d’erreur : tooview ces événements dans l’Observateur d’événements Diagnostic de Visual Studio ajoutent « Microsoft-ServiceFabric:4:0x4000000000000010 « toohello la liste des fournisseurs ETW.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-171">Collect error events: tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" toohello list of ETW providers.</span></span>
<span data-ttu-id="1f1b4-172">événements de hello toocollect à partir de clusters Azure, modifier tooinclude de modèle de gestionnaire de ressources hello</span><span class="sxs-lookup"><span data-stu-id="1f1b4-172">toocollect hello events from Azure clusters, modify hello Resource Manager template tooinclude</span></span>

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

2. <span data-ttu-id="1f1b4-173">Collecte toutes les demande le traitement des événements : Diagnostic Observateur d’événements dans Visual Studio, entrée hello Microsoft-ServiceFabric de mise à jour dans hello liste de fournisseurs ETW trop « Microsoft-ServiceFabric:4:0x4000000000000020 ».</span><span class="sxs-lookup"><span data-stu-id="1f1b4-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update hello Microsoft-ServiceFabric entry in hello ETW provider list too"Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="1f1b4-174">Pour les clusters de Azure Service Fabric, modifiez tooinclude de modèle de gestionnaire de ressources hello</span><span class="sxs-lookup"><span data-stu-id="1f1b4-174">For Azure Service Fabric clusters, modify hello resource manager template tooinclude</span></span>

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
> <span data-ttu-id="1f1b4-175">Il est recommandé de toojudiciously activer la collecte les événements à partir de ce canal collecte tout le trafic via le proxy inverse hello et peut consommer rapidement la capacité de stockage.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-175">It is recommended toojudiciously enable collecting events from this channel as this collects all traffic through hello reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="1f1b4-176">Pour les clusters de Azure Service Fabric, les événements hello à partir de tous les nœuds de hello sont collectés et regroupés dans hello SystemEventTable.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-176">For Azure Service Fabric clusters, hello events from all hello nodes are collected and aggregated in hello SystemEventTable.</span></span>
<span data-ttu-id="1f1b4-177">Pour plus de résolution des problèmes d’événements de proxy inverse hello, consultez hello [proxy inverse diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="1f1b4-177">For detailed troubleshooting of hello reverse proxy events, refer hello [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="1f1b4-178">Collecter à partir de nouveaux canaux EventSource</span><span class="sxs-lookup"><span data-stu-id="1f1b4-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="1f1b4-179">journaux de toocollect tooupdate Diagnostics à partir de nouveaux canaux EventSource qui représentent une nouvelle application que vous êtes sur toodeploy, effectuez hello mêmes étapes comme décrit précédemment pour hello le programme d’installation de Diagnostics pour un cluster existant.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-179">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as previously described for hello setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="1f1b4-180">Mettre à jour hello `EtwEventSourceProviderConfiguration` section dans les entrées de hello template.json fichier tooadd pour hello nouveau EventSource canaux avant d’appliquer la configuration de hello mise à jour à l’aide de hello `New-AzureRmResourceGroupDeployment` commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-180">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="1f1b4-181">nom de Hello de source d’événements hello est défini en tant que partie de votre code dans un fichier généré par Visual Studio de ServiceEventSource.cs hello.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-181">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="1f1b4-182">Par exemple, si votre source d’événements est mon-Eventsource, ajoutez hello suivant des événements de code tooplace hello dans mon-Eventsource dans une table nommée MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-182">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="1f1b4-183">les compteurs de performances toocollect ou les journaux des événements, modifier le modèle de gestionnaire de ressources de hello à l’aide d’exemples hello dans [créer une machine virtuelle Windows avec l’analyse et de diagnostics à l’aide d’un modèle Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1f1b4-183">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1f1b4-184">Ensuite, publier à nouveau modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-184">Then, republish hello Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="1f1b4-185">Collecter des compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="1f1b4-185">Collect Performance Counters</span></span>

<span data-ttu-id="1f1b4-186">toocollect les métriques de performances de votre cluster, ajoutez tooyour de compteurs de performances hello « DiagnosticMonitorConfiguration de > WadCfg » dans le modèle de gestionnaire de ressources hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-186">toocollect performance metrics from your cluster, add hello performance counters tooyour "WadCfg > DiagnosticMonitorConfiguration" in hello Resource Manager template for your cluster.</span></span> <span data-ttu-id="1f1b4-187">Consultez [Compteurs de performances de Service Fabric](service-fabric-diagnostics-event-generation-perf.md) pour plus d’informations sur les compteurs de performances que nous vous recommandons de collecter.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="1f1b4-188">Par exemple, nous définir ici un compteur de performance, échantillonné toutes les 15 secondes (Cela peut être modifié et suit hello format de « PT\<temps >\<unité > », PT3M serait exemple toutes les trois minutes) et transférées toohello table de stockage approprié chaque minute.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows hello format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred toohello appropriate storage table every one minute.</span></span>

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
  
<span data-ttu-id="1f1b4-189">Si vous utilisez un récepteur d’Application Insights, comme décrit dans la section hello ci-dessous et que vous souhaitez tooshow de ces métriques dans Application Insights, puis apportez que nom de récepteur tooadd hello dans hello « récepteurs » section comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-189">If you are using an Application Insights sink, as described in hello section below, and want these metrics tooshow up in Application Insights, then make sure tooadd hello sink name in hello "sinks" section as shown above.</span></span> <span data-ttu-id="1f1b4-190">En outre, envisagez la création d’une table distincte de toosend vos compteurs de performances, afin qu’ils n’inutile out hello données provenant de hello autres canaux d’enregistrement que vous avez activé.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-190">Additionally, consider creating a separate table toosend your Performance Counters to, so they don't crowd out hello data coming from hello other logging channels you have enabled.</span></span>


## <a name="send-logs-tooapplication-insights"></a><span data-ttu-id="1f1b4-191">Envoi consigne tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="1f1b4-191">Send logs tooApplication Insights</span></span>

<span data-ttu-id="1f1b4-192">TooApplication de données de surveillance et de diagnostic Insights (AI) peut être envoyé dans le cadre de la configuration des diagnostics Windows AZURE hello.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-192">Sending monitoring and diagnostics data tooApplication Insights (AI) can be done as part of hello WAD configuration.</span></span> <span data-ttu-id="1f1b4-193">Si vous décidez toouse AI pour analyse des événements et la visualisation, lisez [analyse des événements et visualisation avec Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset d’un récepteur AI dans le cadre de votre « WadCfg ».</span><span class="sxs-lookup"><span data-stu-id="1f1b4-193">If you decide toouse AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f1b4-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1f1b4-194">Next steps</span></span>

<span data-ttu-id="1f1b4-195">Une fois que vous avez correctement configuré les diagnostics Azure, vous verrez les données de vos tables de stockage à partir de hello ETW et journaux d’EventSource.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from hello ETW and EventSource logs.</span></span> <span data-ttu-id="1f1b4-196">Si vous choisissez toouse OMS, Kibana ou autres données analytique et la visualisation des plates-formes qui n’est pas configuré directement dans le modèle de gestionnaire de ressources hello, assurez-vous que tooset plate-forme hello de tooread de votre choix dans les données de salutation à partir de ces tables de stockage.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-196">If you choose toouse OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in hello Resource Manager template, make sure tooset up hello platform of your choice tooread in hello data from these storage tables.</span></span> <span data-ttu-id="1f1b4-197">Cette opération relativement simple pour OMS est expliquée dans [Analyse d’événements et de journaux via OMS](service-fabric-diagnostics-event-analysis-oms.md).</span><span class="sxs-lookup"><span data-stu-id="1f1b4-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="1f1b4-198">Application Insights est un peu d’un cas spécial en ce sens, car il peut être configuré en tant que partie de la configuration de l’extension Diagnostics hello, par conséquent, consultez le toohello [approprié](service-fabric-diagnostics-event-analysis-appinsights.md) si vous choisissez toouse AI.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of hello Diagnostics extension configuration, so refer toohello [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose toouse AI.</span></span>

>[!NOTE]
><span data-ttu-id="1f1b4-199">Il n’existe actuellement aucun moyen toofilter ou marié hello événements envoyés toohello table.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-199">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="1f1b4-200">Si vous n’implémentez pas tooremove un traitement des événements à partir de la table de hello, table de hello continue toogrow.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-200">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span> <span data-ttu-id="1f1b4-201">Actuellement, est un exemple d’un service de nettoyage de données en cours d’exécution dans hello [exemple de surveillance](https://github.com/Azure-Samples/service-fabric-watchdog-service), et il est recommandé d’écrire un pour vous-même, sauf s’il existe une bonne raison vous journaux toostore dépasse un laps de temps jour 30 ou 90.</span><span class="sxs-lookup"><span data-stu-id="1f1b4-201">Currently, there is an example of a data grooming service running in hello [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you toostore logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="1f1b4-202">Découvrez comment les compteurs de performances toocollect ou journaux à l’aide de hello extension des Diagnostics</span><span class="sxs-lookup"><span data-stu-id="1f1b4-202">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="1f1b4-203">Analyse et visualisation d’événements avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="1f1b4-203">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="1f1b4-204">Analyse et visualisation d’événements avec OMS</span><span class="sxs-lookup"><span data-stu-id="1f1b4-204">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)