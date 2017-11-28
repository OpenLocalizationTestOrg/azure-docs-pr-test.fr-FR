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
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="9ef3d-103">Collecte des journaux avec Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="9ef3d-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ef3d-104">Windows</span><span class="sxs-lookup"><span data-stu-id="9ef3d-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="9ef3d-105">Linux</span><span class="sxs-lookup"><span data-stu-id="9ef3d-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="9ef3d-106">Lorsque vous exécutez un cluster Azure Service Fabric, il s’agit d’une bonne idée toocollect hello les journaux à partir de tous les nœuds hello dans un emplacement central.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="9ef3d-107">Ayant hello journaux dans un emplacement central vous permet d’analyser et résoudre les problèmes de votre cluster, ou dans les applications hello et les services exécutés dans ce cluster.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="9ef3d-108">Tooupload d’une façon et collecter des journaux est l’extension de Diagnostics Windows Azure hello toouse, les téléchargements de journaux tooAzure stockage Azure Application Insights ou Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-108">One way tooupload and collect logs is toouse hello Azure Diagnostics extension, which uploads logs tooAzure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="9ef3d-109">journaux de Hello ne sont pas utiles directement dans le stockage ou dans des concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-109">hello logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="9ef3d-110">Mais vous pouvez utiliser un processus externe tooread hello d’événements à partir du stockage et les placer dans un produit tel que [Analytique de journal](../log-analytics/log-analytics-service-fabric.md) ou une autre solution d’analyse de journal.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-110">But you can use an external process tooread hello events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="9ef3d-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) est fourni avec un service complet de recherche dans les journaux et d’analyse des données intégré.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ef3d-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9ef3d-112">Prerequisites</span></span>
<span data-ttu-id="9ef3d-113">Vous utilisez ces outils tooperform certaines opérations hello dans ce document :</span><span class="sxs-lookup"><span data-stu-id="9ef3d-113">You use these tools tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="9ef3d-114">[Diagnostics Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (liés tooAzure Services de cloud computing a, mais les bonnes informations et des exemples)</span><span class="sxs-lookup"><span data-stu-id="9ef3d-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="9ef3d-115">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9ef3d-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="9ef3d-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ef3d-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="9ef3d-117">Applets de commande Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9ef3d-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="9ef3d-118">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9ef3d-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a><span data-ttu-id="9ef3d-119">Vous voudrez probablement toocollect des sources de journal</span><span class="sxs-lookup"><span data-stu-id="9ef3d-119">Log sources that you might want toocollect</span></span>
* <span data-ttu-id="9ef3d-120">**Les journaux de l’infrastructure de service**: émis à partir de hello plateforme toostandard suivi d’événements pour Windows (ETW) et EventSource des canaux.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-120">**Service Fabric logs**: Emitted from hello platform toostandard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="9ef3d-121">Il existe plusieurs types de journaux :</span><span class="sxs-lookup"><span data-stu-id="9ef3d-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="9ef3d-122">Les événements opérationnels : journaux pour les opérations qui hello Service Fabric effectue de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-122">Operational events: Logs for operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="9ef3d-123">Par exemple : la création d’applications et de services, les modifications d’état des nœuds et les informations de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="9ef3d-124">Événements du modèle de programmation Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="9ef3d-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="9ef3d-125">Événements du modèle de programmation Reliable Services</span><span class="sxs-lookup"><span data-stu-id="9ef3d-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="9ef3d-126">**Événements d’application**: événements émis à partir du code de votre service et l’écrit à l’aide de classe d’assistance de hello EventSource fournie dans les modèles de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-126">**Application events**: Events emitted from your service's code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="9ef3d-127">Pour plus d’informations sur comment toowrite se connecte à partir de votre application, consultez [analyse et de diagnostiquer les services dans une installation de développement local machine](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="9ef3d-127">For more information on how toowrite logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="9ef3d-128">Déployer l’extension de Diagnostics hello</span><span class="sxs-lookup"><span data-stu-id="9ef3d-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="9ef3d-129">Hello première étape de collecte de journaux est l’extension de Diagnostics toodeploy hello sur chacune des machines virtuelles de hello dans le cluster Service Fabric de hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="9ef3d-130">Hello, extension de diagnostic collecte des journaux sur chaque machine virtuelle et les charge compte de stockage toohello que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="9ef3d-131">étapes de Hello varient légèrement en fonction de que vous utilisez hello portail Azure ou Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="9ef3d-132">également, les étapes de Hello varient en fonction de déploiement de hello fait partie de la création du cluster ou pour un cluster existe déjà.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="9ef3d-133">Examinez les étapes hello pour chaque scénario.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a><span data-ttu-id="9ef3d-134">Déployer l’extension de Diagnostics hello dans le cadre de la création du cluster via le portail de hello</span><span class="sxs-lookup"><span data-stu-id="9ef3d-134">Deploy hello Diagnostics extension as part of cluster creation through hello portal</span></span>
<span data-ttu-id="9ef3d-135">toodeploy hello Diagnostics extension toohello machines virtuelles dans le cluster hello dans le cadre de la création du cluster, vous utilisez Panneau de paramètres de Diagnostics hello illustré hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image.</span></span> <span data-ttu-id="9ef3d-136">tooenable Reliable Actors ou des Services fiables collecte d’événements, vérifiez que les tests de diagnostic est défini trop**sur** (paramètre par défaut de hello).</span><span class="sxs-lookup"><span data-stu-id="9ef3d-136">tooenable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="9ef3d-137">Après avoir créé le cluster de hello, vous ne pouvez pas modifier ces paramètres à l’aide du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-137">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Paramètres de Diagnostics Azure dans le portail hello pour la création du cluster](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="9ef3d-139">Bienvenue équipe de support Azure *requiert* prise en charge des journaux toohelp résoudre toutes les demandes de prise en charge que vous créez.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-139">hello Azure support team *requires* support logs toohelp resolve any support requests that you create.</span></span> <span data-ttu-id="9ef3d-140">Ces journaux sont collectés en temps réel et sont stockés dans un des comptes de stockage hello créés dans le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-140">These logs are collected in real time and are stored in one of hello storage accounts created in hello resource group.</span></span> <span data-ttu-id="9ef3d-141">paramètres de diagnostic Hello configurent les événements de niveau application.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-141">hello Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="9ef3d-142">Ces événements sont notamment [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) événements, [des Services fiables](service-fabric-reliable-services-diagnostics.md) certains toobe d’événements de l’infrastructure de Service au niveau du système stockées dans le stockage Azure et les événements.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events toobe stored in Azure Storage.</span></span>

<span data-ttu-id="9ef3d-143">Produits tels que [Elasticsearch](https://www.elastic.co/guide/index.html) ou votre propre processus peuvent obtenir les événements de hello du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get hello events from hello storage account.</span></span> <span data-ttu-id="9ef3d-144">Il n’existe actuellement aucun moyen toofilter ou marié hello événements envoyés toohello table.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-144">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="9ef3d-145">Si vous n’implémentez pas tooremove un traitement des événements à partir de la table de hello, table de hello continue toogrow.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-145">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span>

<span data-ttu-id="9ef3d-146">Lorsque vous créez un cluster à l’aide du portail de hello, nous recommandons vivement que vous téléchargez le modèle de hello **avant de cliquer sur OK** cluster hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-146">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="9ef3d-147">Pour plus d’informations, consultez trop[configurer un cluster Service Fabric à l’aide d’un modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9ef3d-147">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="9ef3d-148">Vous aurez besoin des modifications apportées au modèle toomake hello plus tard, car vous ne pouvez pas apporter des modifications à l’aide du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-148">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

<span data-ttu-id="9ef3d-149">Vous pouvez exporter des modèles à partir du portail de hello à l’aide de hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-149">You can export templates from hello portal by using hello following steps.</span></span> <span data-ttu-id="9ef3d-150">Toutefois, ces modèles peuvent être toouse plus difficile, car ils peuvent avoir des valeurs null que les informations requises sont manquantes.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-150">However, these templates can be more difficult toouse because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="9ef3d-151">Ouvrez votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-151">Open your resource group.</span></span>
2. <span data-ttu-id="9ef3d-152">Sélectionnez **paramètres** Panneau de paramètres toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-152">Select **Settings** toodisplay hello settings panel.</span></span>
3. <span data-ttu-id="9ef3d-153">Sélectionnez **déploiements** Panneau de l’historique du déploiement toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-153">Select **Deployments** toodisplay hello deployment history panel.</span></span>
4. <span data-ttu-id="9ef3d-154">Sélectionnez un déploiement toodisplay hello les détails du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-154">Select a deployment toodisplay hello details of hello deployment.</span></span>
5. <span data-ttu-id="9ef3d-155">Sélectionnez **exporter le modèle** Panneau de modèle toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-155">Select **Export Template** toodisplay hello template panel.</span></span>
6. <span data-ttu-id="9ef3d-156">Sélectionnez **enregistrer toofile** tooexport un fichier .zip qui contient le modèle de hello, paramètres et fichiers de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-156">Select **Save toofile** tooexport a .zip file that contains hello template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="9ef3d-157">Une fois que vous exportez les fichiers hello, vous devez toomake une modification.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-157">After you export hello files, you need toomake a modification.</span></span> <span data-ttu-id="9ef3d-158">Modifier le fichier de parameters.json hello et supprimer hello **adminPassword** élément.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-158">Edit hello parameters.json file and remove hello **adminPassword** element.</span></span> <span data-ttu-id="9ef3d-159">Cela entraîne une invite de mot de passe hello lors de l’exécution de script de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-159">This will cause a prompt for hello password when hello deployment script is run.</span></span> <span data-ttu-id="9ef3d-160">Lorsque vous exécutez le script de déploiement hello, vous pouvez avoir des valeurs de paramètre null toofix.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-160">When you're running hello deployment script, you might have toofix null parameter values.</span></span>

<span data-ttu-id="9ef3d-161">toouse hello téléchargé une configuration à tooupdate du modèle :</span><span class="sxs-lookup"><span data-stu-id="9ef3d-161">toouse hello downloaded template tooupdate a configuration:</span></span>

1. <span data-ttu-id="9ef3d-162">Extrayez hello contenu tooa dossier sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-162">Extract hello contents tooa folder on your local computer.</span></span>
2. <span data-ttu-id="9ef3d-163">Modifier la nouvelle configuration hello contenu tooreflect hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-163">Modify hello contents tooreflect hello new configuration.</span></span>
3. <span data-ttu-id="9ef3d-164">Démarrez PowerShell et modifier le dossier toohello où vous avez extrait le contenu hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-164">Start PowerShell and change toohello folder where you extracted hello content.</span></span>
4. <span data-ttu-id="9ef3d-165">Exécutez **deploy.ps1** et renseignez les ID d’abonnement hello, nom de groupe de ressources hello (utilisez hello même configuration hello tooupdate du nom) et un nom unique de déploiement.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-165">Run **deploy.ps1** and fill in hello subscription ID, hello resource group name (use hello same name tooupdate hello configuration), and a unique deployment name.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="9ef3d-166">Déployer l’extension de Diagnostics hello dans le cadre de la création du cluster à l’aide du Gestionnaire de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="9ef3d-166">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="9ef3d-167">toocreate un cluster à l’aide du Gestionnaire de ressources, vous devez modèle de gestionnaire de ressources du cluster complet configuration JSON toohello tooadd hello Diagnostics avant de créer le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-167">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="9ef3d-168">Nous fournissons un modèle de gestionnaire de ressources de cluster de cinq-VM avec la configuration des Diagnostics ajoutée tooit dans le cadre de nos exemples de modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="9ef3d-169">Vous pouvez le voir à cet emplacement dans la galerie d’exemples de Azure hello : [cluster à cinq nœuds avec l’exemple de modèle de gestionnaire de ressources de diagnostic](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span><span class="sxs-lookup"><span data-stu-id="9ef3d-169">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="9ef3d-170">toosee hello Diagnostics des paramètres de modèle de gestionnaire de ressources hello, fichier de azuredeploy.json hello ouvert et recherchez **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-170">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="9ef3d-171">toocreate un cluster à l’aide de ce modèle, un select hello **déployer tooAzure** bouton disponible sur le lien précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-171">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="9ef3d-172">Ou bien, vous pouvez télécharger l’exemple de gestionnaire de ressources hello, apporter des modifications tooit et créer un cluster avec le modèle modifié de hello à l’aide de hello `New-AzureRmResourceGroupDeployment` dans une fenêtre Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-172">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="9ef3d-173">Consultez hello suivant de code pour les paramètres hello que vous passez dans toohello commande.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-173">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="9ef3d-174">Pour plus d’informations sur la façon dont toodeploy une ressource de groupe à l’aide de PowerShell, voir l’article hello [déployer un groupe de ressources avec le modèle de gestionnaire de ressources Azure hello](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9ef3d-174">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="9ef3d-175">Déployer le cluster existant de hello Diagnostics extension tooan</span><span class="sxs-lookup"><span data-stu-id="9ef3d-175">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="9ef3d-176">Si vous avez un cluster existant n’ayant pas déployé de Diagnostics, ou si vous souhaitez toomodify une configuration existante, vous pouvez ajouter ou mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="9ef3d-177">Modifier le modèle de gestionnaire de ressources hello cluster existant de hello toocreate utilisés ou télécharger le modèle de hello à partir du portail hello comme décrit précédemment.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-177">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="9ef3d-178">Modifier le fichier de template.json de hello en effectuant hello tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-178">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="9ef3d-179">Ajouter un nouveau modèle de toohello de ressources de stockage en ajoutant la section de ressources toohello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-179">Add a new storage resource toohello template by adding toohello resources section.</span></span>

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

 <span data-ttu-id="9ef3d-180">Ensuite, ajoutez les paramètres toohello section juste après les définitions de compte de stockage hello, entre `supportLogStorageAccountName` et `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-180">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="9ef3d-181">Remplacez le texte d’espace réservé hello *nom de compte de stockage ici* avec nom hello hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-181">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

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
<span data-ttu-id="9ef3d-182">Ensuite, mettez à jour hello `VirtualMachineProfile` section du fichier de template.json hello en ajoutant hello suivant le code dans le tableau d’extensions hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-182">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="9ef3d-183">Être tooadd vraiment une virgule au début de hello ou hello fin, selon lequel il est inséré.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-183">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="9ef3d-184">Après avoir modifié le fichier de template.json hello comme décrit, republiez le modèle de gestionnaire de ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-184">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="9ef3d-185">Si le modèle de hello a été exporté, le fichier de deploy.ps1 hello en cours d’exécution republie modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-185">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="9ef3d-186">Après le déploiement, assurez-vous que **ProvisioningState** présente la valeur **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-toocollect-health-and-load-events"></a><span data-ttu-id="9ef3d-187">Mettre à jour les événements de contrôle d’intégrité et de charge de toocollect diagnostics</span><span class="sxs-lookup"><span data-stu-id="9ef3d-187">Update diagnostics toocollect health and load events</span></span>

<span data-ttu-id="9ef3d-188">À partir de la version de hello 5.4 de l’infrastructure de Service, les événements de métrique d’intégrité et de charge sont disponibles pour la collection.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-188">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="9ef3d-189">Ces événements reflète les événements générés par le système de hello ou votre code à l’aide du contrôle d’intégrité hello ou charger les API de création de rapports tels que [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) ou [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ef3d-189">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="9ef3d-190">Cela permet non seulement de consolider et de visualiser l’intégrité du système dans le temps, mais aussi de générer des alertes en fonction de certains événements d’intégrité et de charge.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="9ef3d-191">tooview ces événements dans l’Observateur d’événements Diagnostic de Visual Studio ajoutent « Microsoft-ServiceFabric:4:0x4000000000000008 « toohello la liste des fournisseurs ETW.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-191">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="9ef3d-192">événements de hello toocollect, modifier tooinclude de modèle de gestionnaire de ressources hello</span><span class="sxs-lookup"><span data-stu-id="9ef3d-192">toocollect hello events, modify hello resource manager template tooinclude</span></span>

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

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="9ef3d-193">Mettre à jour des Diagnostics toocollect et télécharger les journaux de nouveaux canaux EventSource</span><span class="sxs-lookup"><span data-stu-id="9ef3d-193">Update Diagnostics toocollect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="9ef3d-194">journaux de toocollect tooupdate Diagnostics à partir de nouveaux canaux EventSource qui représentent une nouvelle application que vous êtes sur toodeploy, effectuer hello même procédure que dans hello [section précédente](#deploywadarm) pour le programme d’installation de Diagnostics pour une existante cluster.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-194">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as in hello [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="9ef3d-195">Mettre à jour hello `EtwEventSourceProviderConfiguration` section dans les entrées de hello template.json fichier tooadd pour hello nouveau EventSource canaux avant d’appliquer la configuration de hello mise à jour à l’aide de hello `New-AzureRmResourceGroupDeployment` commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-195">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="9ef3d-196">nom de Hello de source d’événements hello est défini en tant que partie de votre code dans un fichier généré par Visual Studio de ServiceEventSource.cs hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-196">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="9ef3d-197">Par exemple, si votre source d’événements est mon-Eventsource, ajoutez hello suivant des événements de code tooplace hello dans mon-Eventsource dans une table nommée MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-197">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="9ef3d-198">les compteurs de performances toocollect ou les journaux des événements, modifier le modèle de gestionnaire de ressources de hello à l’aide d’exemples hello dans [créer une machine virtuelle Windows avec l’analyse et de diagnostics à l’aide d’un modèle Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9ef3d-198">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="9ef3d-199">Ensuite, publier à nouveau modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-199">Then, republish hello Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ef3d-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ef3d-200">Next steps</span></span>
<span data-ttu-id="9ef3d-201">toounderstand plus en détail les événements que vous devez rechercher lors de la résolution des problèmes, consultez les événements de diagnostic hello émis pour [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) et [des Services fiables](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="9ef3d-201">toounderstand in more detail what events you should look for while troubleshooting issues, see hello diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="9ef3d-202">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="9ef3d-202">Related articles</span></span>
* [<span data-ttu-id="9ef3d-203">Découvrez comment les compteurs de performances toocollect ou journaux à l’aide de hello extension des Diagnostics</span><span class="sxs-lookup"><span data-stu-id="9ef3d-203">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="9ef3d-204">Solution Service Fabric dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9ef3d-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)

