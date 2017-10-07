---
title: "application du correctif logiciel de l’infrastructure de Service d’orchestration d’aaaAzure | Documents Microsoft"
description: "Tooautomate application fonctionne la mise à jour corrective du système sur un cluster Service Fabric."
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="d4053-103">Correctif logiciel de système de d’exploitation Windows hello dans votre cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d4053-103">Patch hello Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="d4053-104">application d’orchestration Hello correctif est une application Azure Service Fabric qui automatise le système d’exploitation mise à jour corrective sur un cluster Service Fabric sur Azure sans temps mort.</span><span class="sxs-lookup"><span data-stu-id="d4053-104">hello patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="d4053-105">application d’orchestration Hello correctif fournit des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="d4053-105">hello patch orchestration app provides hello following:</span></span>

- <span data-ttu-id="d4053-106">**Installation automatique de mise à jour du système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="d4053-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="d4053-107">Des mises à jour du système d’exploitation sont téléchargées et installées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d4053-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="d4053-108">Les nœuds de cluster sont redémarrés en fonction des besoins sans temps d’arrêt du cluster.</span><span class="sxs-lookup"><span data-stu-id="d4053-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="d4053-109">**Application de correctifs et intégration de l’intégrité adaptées au cluster**.</span><span class="sxs-lookup"><span data-stu-id="d4053-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="d4053-110">Lors de l’application des mises à jour, application d’orchestration hello correctif surveille l’intégrité de hello hello des nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="d4053-110">While applying updates, hello patch orchestration app monitors hello health of hello cluster nodes.</span></span> <span data-ttu-id="d4053-111">Les nœuds de cluster sont mis à niveau l’un après l’autre, ou domaine de mise à niveau après domaine de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="d4053-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="d4053-112">Si le contrôle d’intégrité hello du cluster de hello tombe en panne en raison du processus de correction toohello, la mise à jour corrective est arrêté tooprevent aggraver le problème de hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-112">If hello health of hello cluster goes down due toohello patching process, patching is stopped tooprevent aggravating hello problem.</span></span>

## <a name="internal-details-of-hello-app"></a><span data-ttu-id="d4053-113">Détails internes de l’application hello</span><span class="sxs-lookup"><span data-stu-id="d4053-113">Internal details of hello app</span></span>

<span data-ttu-id="d4053-114">application d’orchestration de correctif Hello est composée de hello suivant sous-composants :</span><span class="sxs-lookup"><span data-stu-id="d4053-114">hello patch orchestration app is composed of hello following subcomponents:</span></span>

- <span data-ttu-id="d4053-115">**Service Coordinateur** : ce service avec état est responsable des aspects suivants :</span><span class="sxs-lookup"><span data-stu-id="d4053-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="d4053-116">Coordonner le travail de mise à jour de Windows hello sur l’intégralité du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-116">Coordinating hello Windows Update job on hello entire cluster.</span></span>
    - <span data-ttu-id="d4053-117">Le stockage de résultats des opérations terminées et mise à jour de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-117">Storing hello result of completed Windows Update operations.</span></span>
- <span data-ttu-id="d4053-118">**Service Agent du nœud** : ce service sans état s’exécute sur tous les nœuds de cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d4053-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="d4053-119">service de Hello est chargé de :</span><span class="sxs-lookup"><span data-stu-id="d4053-119">hello service is responsible for:</span></span>
    - <span data-ttu-id="d4053-120">Amorçage hello du service NT de l’Agent de nœud.</span><span class="sxs-lookup"><span data-stu-id="d4053-120">Bootstrapping hello Node Agent NTService.</span></span>
    - <span data-ttu-id="d4053-121">Analyse hello du service NT de l’Agent de nœud.</span><span class="sxs-lookup"><span data-stu-id="d4053-121">Monitoring hello Node Agent NTService.</span></span>
- <span data-ttu-id="d4053-122">**service NT Agent du nœud** : ce service Windows NT s’exécute avec un privilège de niveau supérieur (système).</span><span class="sxs-lookup"><span data-stu-id="d4053-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="d4053-123">En revanche, hello Service Agent de nœud et hello Service coordinateur d’exécutent avec un privilège de niveau inférieur (SERVICE réseau).</span><span class="sxs-lookup"><span data-stu-id="d4053-123">In contrast, hello Node Agent Service and hello Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="d4053-124">service de Hello est chargé d’effectuer hello suivant des travaux de mise à jour de Windows sur tous les nœuds de cluster hello :</span><span class="sxs-lookup"><span data-stu-id="d4053-124">hello service is responsible for performing hello following Windows Update jobs on all hello cluster nodes:</span></span>
    - <span data-ttu-id="d4053-125">Désactivation de la mise à jour automatique de Windows sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-125">Disabling automatic Windows Update on hello node.</span></span>
    - <span data-ttu-id="d4053-126">Téléchargement et installation des mises à jour Windows selon l’utilisateur de hello stratégie toohello a fourni.</span><span class="sxs-lookup"><span data-stu-id="d4053-126">Downloading and installing Windows Update according toohello policy hello user has provided.</span></span>
    - <span data-ttu-id="d4053-127">Le redémarrage de billet d’ordinateur hello installation mise à jour de Windows.</span><span class="sxs-lookup"><span data-stu-id="d4053-127">Restarting hello machine post Windows Update installation.</span></span>
    - <span data-ttu-id="d4053-128">Chargement des résultats hello de mises à jour de Windows toohello Service de coordinateur.</span><span class="sxs-lookup"><span data-stu-id="d4053-128">Uploading hello results of Windows updates toohello Coordinator Service.</span></span>
    - <span data-ttu-id="d4053-129">génération de rapport d’intégrité en cas d’échec de l’opération une fois toutes les nouvelles tentatives effectuées.</span><span class="sxs-lookup"><span data-stu-id="d4053-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="d4053-130">Hello correctif orchestration application utilise hello Service Fabric réparer toodisable de service manager système ou activer le nœud de hello et d’effectuer des vérifications d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="d4053-130">hello patch orchestration app uses hello Service Fabric repair manager system service toodisable or enable hello node and perform health checks.</span></span> <span data-ttu-id="d4053-131">tâche de réparation Hello créé par hello correctif orchestration application pistes hello cours de mise à jour de Windows pour chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="d4053-131">hello repair task created by hello patch orchestration app tracks hello Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4053-132">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d4053-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="d4053-133">Version du runtime Service Fabric minimale prise en charge</span><span class="sxs-lookup"><span data-stu-id="d4053-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="d4053-134">Clusters Azure</span><span class="sxs-lookup"><span data-stu-id="d4053-134">Azure clusters</span></span>
<span data-ttu-id="d4053-135">application d’orchestration Hello patch doit être exécutée sur des clusters Azure qui ont l’infrastructure de Service runtime version 5.5 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d4053-135">hello patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="d4053-136">Clusters locaux autonomes</span><span class="sxs-lookup"><span data-stu-id="d4053-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="d4053-137">application d’orchestration Hello correctif doit être exécutée sur les clusters autonomes qui ont la version 5.6 version de runtime Service Fabric ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d4053-137">hello patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="d4053-138">Activer le service de gestionnaire de réparation hello (si ce n’est pas déjà fait)</span><span class="sxs-lookup"><span data-stu-id="d4053-138">Enable hello repair manager service (if it's not running already)</span></span>

<span data-ttu-id="d4053-139">application d’orchestration Hello correctif requiert hello réparation Gestionnaire système service toobe est activé sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-139">hello patch orchestration app requires hello repair manager system service toobe enabled on hello cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="d4053-140">Clusters Azure</span><span class="sxs-lookup"><span data-stu-id="d4053-140">Azure clusters</span></span>

<span data-ttu-id="d4053-141">Les clusters Azure dans le niveau de durabilité silver hello ont hello réparer service manager est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="d4053-141">Azure clusters in hello silver durability tier have hello repair manager service enabled by default.</span></span> <span data-ttu-id="d4053-142">Les clusters Azure dans le niveau de durabilité gold hello peuvent ou peut-être pas le service de gestionnaire de réparation hello activé, en fonction de laquelle ces clusters ont été créées.</span><span class="sxs-lookup"><span data-stu-id="d4053-142">Azure clusters in hello gold durability tier might or might not have hello repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="d4053-143">Les clusters Azure dans le niveau de durabilité bronze hello, par défaut, n’ont pas hello de réparation de service manager est activé.</span><span class="sxs-lookup"><span data-stu-id="d4053-143">Azure clusters in hello bronze durability tier, by default, do not have hello repair manager service enabled.</span></span> <span data-ttu-id="d4053-144">Si le service de hello est déjà activé, vous pouvez le voir en cours d’exécution dans la section de services système hello Bonjour Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="d4053-144">If hello service is already enabled, you can see it running in hello system services section in hello Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="d4053-145">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d4053-145">Azure portal</span></span>
<span data-ttu-id="d4053-146">Vous pouvez activer le Gestionnaire de réparation à partir du portail Azure au moment de hello de configuration du cluster.</span><span class="sxs-lookup"><span data-stu-id="d4053-146">You can enable repair manager from Azure portal at hello time of setting up of cluster.</span></span> <span data-ttu-id="d4053-147">Sélectionnez `Include Repair Manager` sous `Add on features` au moment de hello de configuration du Cluster.</span><span class="sxs-lookup"><span data-stu-id="d4053-147">Select `Include Repair Manager` option under `Add on features` at hello time of Cluster configuration.</span></span>
<span data-ttu-id="d4053-148">![Image représentant l’activation du gestionnaire des réparations à partir du portail Azure](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="d4053-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="d4053-149">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d4053-149">Azure Resource Manager template</span></span>
<span data-ttu-id="d4053-150">Vous pouvez également utiliser hello [modèle Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) service de gestionnaire de réparation tooenable hello sur des clusters Service Fabric nouveaux et existants.</span><span class="sxs-lookup"><span data-stu-id="d4053-150">Alternatively you can use hello [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="d4053-151">Obtenir le modèle de hello pour le cluster de hello que vous souhaitez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="d4053-151">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="d4053-152">Vous pouvez utiliser des modèles d’exemple hello ou créer un modèle de gestionnaire de ressources personnalisé.</span><span class="sxs-lookup"><span data-stu-id="d4053-152">You can either use hello sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="d4053-153">tooenable hello réparation manager service à l’aide de [modèle Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="d4053-153">tooenable hello repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="d4053-154">Vérifiez tout d’abord que hello `apiversion` est défini trop`2017-07-01-preview` pour hello `Microsoft.ServiceFabric/clusters` ressource, comme indiqué dans hello suivant extrait de code.</span><span class="sxs-lookup"><span data-stu-id="d4053-154">First check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, as shown in hello following snippet.</span></span> <span data-ttu-id="d4053-155">Si elle est différente, vous devez tooupdate hello `apiVersion` toohello valeur `2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="d4053-155">If it is different, then you need tooupdate hello `apiVersion` toohello value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="d4053-156">Service de gestionnaire de réparation hello à présent activer en ajoutant des éléments suivants de hello `addonFeatures` section après hello `fabricSettings` section :</span><span class="sxs-lookup"><span data-stu-id="d4053-156">Now enable hello repair manager service by adding hello following `addonFeatures` section after hello `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="d4053-157">Une fois que vous avez mis à jour votre modèle de cluster avec ces modifications, appliquez-les et laissez la mise à niveau hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-157">After you have updated your cluster template with these changes, apply them and let hello upgrade finish.</span></span> <span data-ttu-id="d4053-158">Vous pouvez maintenant voir le service système hello réparation manager en cours d’exécution dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d4053-158">You can now see hello repair manager system service running in your cluster.</span></span> <span data-ttu-id="d4053-159">Il est appelé `fabric:/System/RepairManagerService` dans la section de services système hello Bonjour Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="d4053-159">It is called `fabric:/System/RepairManagerService` in hello system services section in hello Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="d4053-160">Clusters locaux autonomes</span><span class="sxs-lookup"><span data-stu-id="d4053-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="d4053-161">Vous pouvez utiliser hello [paramètres de Configuration de cluster de Windows autonome](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) service de gestionnaire de réparation tooenable hello sur le cluster de Service Fabric nouveaux et existant.</span><span class="sxs-lookup"><span data-stu-id="d4053-161">You can use hello [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="d4053-162">service de gestionnaire de réparation tooenable hello :</span><span class="sxs-lookup"><span data-stu-id="d4053-162">tooenable hello repair manager service:</span></span>

1. <span data-ttu-id="d4053-163">Vérifiez tout d’abord que hello `apiversion` dans [configurations de cluster général](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) est défini trop`04-2017` ou une version ultérieure :</span><span class="sxs-lookup"><span data-stu-id="d4053-163">First check that hello `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set too`04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="d4053-164">Service de gestionnaire de réparation à présent activer en ajoutant des éléments suivants de hello `addonFeaturres` section après hello `fabricSettings` section comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d4053-164">Now enable repair manager service by adding hello following `addonFeaturres` section after hello `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="d4053-165">Mettre à jour votre manifeste de cluster avec ces modifications, à l’aide de manifeste du cluster hello mis à jour [créer un nouveau cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) ou [configuration de cluster de mise à niveau hello](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span><span class="sxs-lookup"><span data-stu-id="d4053-165">Update your cluster manifest with these changes, using hello updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade hello cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="d4053-166">Une fois que le cluster de hello est en cours d’exécution avec un manifeste de cluster mis à jour, vous pouvez maintenant voir le service système hello réparation manager en cours d’exécution dans votre cluster, qui est appelé `fabric:/System/RepairManagerService`, sous la section dans l’Explorateur de Service Fabric hello des services système.</span><span class="sxs-lookup"><span data-stu-id="d4053-166">Once hello cluster is running with updated cluster manifest, you can now see hello repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in hello Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="d4053-167">Désactiver les mises à jour automatiques Windows Update sur tous les nœuds</span><span class="sxs-lookup"><span data-stu-id="d4053-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="d4053-168">Mises à jour automatiques de Windows peuvent provoquer des tooavailability perte, car plusieurs nœuds de cluster peuvent redémarrer hello même temps.</span><span class="sxs-lookup"><span data-stu-id="d4053-168">Automatic Windows updates might lead tooavailability loss because multiple cluster nodes can restart at hello same time.</span></span> <span data-ttu-id="d4053-169">application d’orchestration de correctif Hello, par défaut, les tentatives toodisable hello automatique Windows Update sur chaque nœud du cluster.</span><span class="sxs-lookup"><span data-stu-id="d4053-169">hello patch orchestration app, by default, tries toodisable hello automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="d4053-170">Toutefois, si les paramètres de hello sont gérés par un administrateur ou d’une stratégie de groupe, nous vous recommandons de hello du paramètre stratégie trop « avertir avant le téléchargement « explicitement de la mise à jour Windows.</span><span class="sxs-lookup"><span data-stu-id="d4053-170">However, if hello settings are managed by an administrator or group policy, we recommend setting hello Windows Update policy too“Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="d4053-171">Facultatif : Activer Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="d4053-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="d4053-172">Pour les clusters exécutant la version du runtime Service Fabric `5.6.220.9494` ou une version supérieure, les journaux de l’application d’orchestration des correctifs sont collectés en même temps que les journaux Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d4053-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="d4053-173">Vous pouvez ignorer cette étape si votre cluster exécute le runtime Service Fabric version `5.6.220.9494` et plus.</span><span class="sxs-lookup"><span data-stu-id="d4053-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="d4053-174">Pour les clusters exécutant la version du runtime Service Fabric moins `5.6.220.9494`, journaux pour l’application d’orchestration hello correctif sont collectés localement sur chaque nœud de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for hello patch orchestration app are collected locally on each of hello cluster nodes.</span></span>
<span data-ttu-id="d4053-175">Nous vous recommandons de configurer des journaux de tooupload de Diagnostics Windows Azure à partir de tous les nœuds tooa point central.</span><span class="sxs-lookup"><span data-stu-id="d4053-175">We recommend that you configure Azure Diagnostics tooupload logs from all nodes tooa central location.</span></span>

<span data-ttu-id="d4053-176">Pour plus d’informations sur l’activation d’Azure Diagnostics, voir [Collecte des journaux avec Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span><span class="sxs-lookup"><span data-stu-id="d4053-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="d4053-177">Journaux pour l’application d’orchestration hello correctif sont générés sur hello suit les ID de fournisseur fixe :</span><span class="sxs-lookup"><span data-stu-id="d4053-177">Logs for hello patch orchestration app are generated on hello following fixed provider IDs:</span></span>

- <span data-ttu-id="d4053-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="d4053-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="d4053-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="d4053-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="d4053-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="d4053-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="d4053-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="d4053-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="d4053-182">Dans le Gestionnaire de ressources du modèle goto `EtwEventSourceProviderConfiguration` sous `WadCfg` et ajoutez hello suivant entrées :</span><span class="sxs-lookup"><span data-stu-id="d4053-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add hello following entries:</span></span>

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> <span data-ttu-id="d4053-183">Si votre cluster Service Fabric a plusieurs types de nœuds, puis hello précédente doit être ajoutée pour toutes les hello `WadCfg` sections.</span><span class="sxs-lookup"><span data-stu-id="d4053-183">If your Service Fabric cluster has multiple node types, then hello previous section must be added for all hello `WadCfg` sections.</span></span>

## <a name="download-hello-app-package"></a><span data-ttu-id="d4053-184">Télécharger le package d’application hello</span><span class="sxs-lookup"><span data-stu-id="d4053-184">Download hello app package</span></span>

<span data-ttu-id="d4053-185">Télécharger l’application hello de hello [lien de téléchargement](https://go.microsoft.com/fwlink/P/?linkid=849590).</span><span class="sxs-lookup"><span data-stu-id="d4053-185">Download hello application from hello [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-hello-app"></a><span data-ttu-id="d4053-186">Configurer l’application hello</span><span class="sxs-lookup"><span data-stu-id="d4053-186">Configure hello app</span></span>

<span data-ttu-id="d4053-187">Hello le comportement de l’application d’orchestration hello correctif peut être configuré toomeet vos besoins.</span><span class="sxs-lookup"><span data-stu-id="d4053-187">hello behavior of hello patch orchestration app can be configured toomeet your needs.</span></span> <span data-ttu-id="d4053-188">Remplacer les valeurs par défaut hello en passant dans le paramètre de l’application hello lors de la création d’application ou de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="d4053-188">Override hello default values by passing in hello application parameter during application creation or update.</span></span> <span data-ttu-id="d4053-189">Paramètres de l’application peuvent être fournis en spécifiant `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` ou `New-ServiceFabricApplication` applets de commande.</span><span class="sxs-lookup"><span data-stu-id="d4053-189">Application parameters can be provided by specifying `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="d4053-190">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="d4053-190">**Parameter**</span></span>        |<span data-ttu-id="d4053-191">**Type**</span><span class="sxs-lookup"><span data-stu-id="d4053-191">**Type**</span></span>                          | <span data-ttu-id="d4053-192">**Détails**</span><span class="sxs-lookup"><span data-stu-id="d4053-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="d4053-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="d4053-193">MaxResultsToCache</span></span>    |<span data-ttu-id="d4053-194">long</span><span class="sxs-lookup"><span data-stu-id="d4053-194">Long</span></span>                              | <span data-ttu-id="d4053-195">Nombre maximal de résultats d’exécution de Windows Update à mettre en cache.</span><span class="sxs-lookup"><span data-stu-id="d4053-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="d4053-196">La valeur par défaut est 3 000, en supposant ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="d4053-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="d4053-197">- Le nombre de nœuds est 20.</span><span class="sxs-lookup"><span data-stu-id="d4053-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="d4053-198">- Le nombre de mises à jour par mois effectuées sur un nœud est 5.</span><span class="sxs-lookup"><span data-stu-id="d4053-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="d4053-199">- Le nombre maximal de résultats par opération est 10.</span><span class="sxs-lookup"><span data-stu-id="d4053-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="d4053-200">-Les résultats pour hello trois derniers mois doivent être stockées.</span><span class="sxs-lookup"><span data-stu-id="d4053-200">- Results for hello past three months should be stored.</span></span> |
|<span data-ttu-id="d4053-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="d4053-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="d4053-202">Enum</span><span class="sxs-lookup"><span data-stu-id="d4053-202">Enum</span></span> <br> <span data-ttu-id="d4053-203">{ NodeWise, UpgradeDomainWise }</span><span class="sxs-lookup"><span data-stu-id="d4053-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="d4053-204">TaskApprovalPolicy indique la stratégie de hello toobe utilisé par les mises à jour tooinstall hello Service coordinateur entre les nœuds du cluster Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-204">TaskApprovalPolicy indicates hello policy that is toobe used by hello Coordinator Service tooinstall Windows updates across hello Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="d4053-205">Les valeurs autorisées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="d4053-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="d4053-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="d4053-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="d4053-207">Les mises à jour Windows Update sont installées de façon séquentielle, nœud après nœud.</span><span class="sxs-lookup"><span data-stu-id="d4053-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="d4053-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="d4053-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="d4053-209">Les mises à jour Windows Update sont installées sur un domaine de mise à niveau à la fois</span><span class="sxs-lookup"><span data-stu-id="d4053-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="d4053-210">(À hello maximale, tous les nœuds de hello appartenant domaine de mise à niveau tooan obtenir Windows Update.)</span><span class="sxs-lookup"><span data-stu-id="d4053-210">(At hello maximum, all hello nodes belonging tooan upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="d4053-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="d4053-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="d4053-212">long</span><span class="sxs-lookup"><span data-stu-id="d4053-212">Long</span></span>  <br> <span data-ttu-id="d4053-213">(Par défaut : 1024)</span><span class="sxs-lookup"><span data-stu-id="d4053-213">(Default: 1024)</span></span>               |<span data-ttu-id="d4053-214">Taille maximale en Mo des journaux de l’application d’orchestration des correctifs qui peuvent être conservés localement sur des nœuds.</span><span class="sxs-lookup"><span data-stu-id="d4053-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="d4053-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="d4053-215">WUQuery</span></span>               | <span data-ttu-id="d4053-216">string</span><span class="sxs-lookup"><span data-stu-id="d4053-216">string</span></span><br><span data-ttu-id="d4053-217">(Par défaut : « IsInstalled=0 »)</span><span class="sxs-lookup"><span data-stu-id="d4053-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="d4053-218">Requête tooget Windows met à jour.</span><span class="sxs-lookup"><span data-stu-id="d4053-218">Query tooget Windows updates.</span></span> <span data-ttu-id="d4053-219">Pour plus d’informations, voir [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="d4053-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="d4053-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="d4053-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="d4053-221">Bool</span><span class="sxs-lookup"><span data-stu-id="d4053-221">Bool</span></span> <br> <span data-ttu-id="d4053-222">(Par défaut : True)</span><span class="sxs-lookup"><span data-stu-id="d4053-222">(default: True)</span></span>                 | <span data-ttu-id="d4053-223">Cet indicateur permet toobe de mises à jour système installé de système d’exploitation Windows.</span><span class="sxs-lookup"><span data-stu-id="d4053-223">This flag allows Windows operating system updates toobe installed.</span></span>            |
| <span data-ttu-id="d4053-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="d4053-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="d4053-225">Int</span><span class="sxs-lookup"><span data-stu-id="d4053-225">Int</span></span> <br><span data-ttu-id="d4053-226">(Par défaut : 90)</span><span class="sxs-lookup"><span data-stu-id="d4053-226">(Default: 90)</span></span>                   | <span data-ttu-id="d4053-227">Spécifie le délai d’attente hello pour toute opération de mise à jour de Windows (recherche ou téléchargement ou installation).</span><span class="sxs-lookup"><span data-stu-id="d4053-227">Specifies hello timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="d4053-228">Si l’opération de hello n’est pas effectuée dans hello de délai d’attente spécifié, elle est abandonnée.</span><span class="sxs-lookup"><span data-stu-id="d4053-228">If hello operation is not completed within hello specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="d4053-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="d4053-229">WURescheduleCount</span></span>     | <span data-ttu-id="d4053-230">Int</span><span class="sxs-lookup"><span data-stu-id="d4053-230">Int</span></span> <br> <span data-ttu-id="d4053-231">(Par défaut : 5)</span><span class="sxs-lookup"><span data-stu-id="d4053-231">(Default: 5)</span></span>                  | <span data-ttu-id="d4053-232">nombre maximal de Hello de service de hello replanifie hello Windows update au cas où une opération continue à échouer.</span><span class="sxs-lookup"><span data-stu-id="d4053-232">hello maximum number of times hello service reschedules hello Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="d4053-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="d4053-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="d4053-234">Int</span><span class="sxs-lookup"><span data-stu-id="d4053-234">Int</span></span> <br><span data-ttu-id="d4053-235">(Par défaut : 30)</span><span class="sxs-lookup"><span data-stu-id="d4053-235">(Default: 30)</span></span> | <span data-ttu-id="d4053-236">intervalle de salutation à quels hello service replanifie la mise à jour de Windows hello en cas de problème persiste.</span><span class="sxs-lookup"><span data-stu-id="d4053-236">hello interval at which hello service reschedules hello Windows update in case failure persists.</span></span> |
| <span data-ttu-id="d4053-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="d4053-237">WUFrequency</span></span>           | <span data-ttu-id="d4053-238">Chaîne de valeurs séparées par des virgules (par défaut : « Hebdomadaire, Mercredi, 7:00:00 »).</span><span class="sxs-lookup"><span data-stu-id="d4053-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="d4053-239">fréquence de Hello pour l’installation de Windows Update.</span><span class="sxs-lookup"><span data-stu-id="d4053-239">hello frequency for installing Windows Update.</span></span> <span data-ttu-id="d4053-240">les valeurs Hello format et possibles sont :</span><span class="sxs-lookup"><span data-stu-id="d4053-240">hello format and possible values are:</span></span> <br><span data-ttu-id="d4053-241">-   Mensuelle, JJ,HH:MM:SS, par exemple, Mensuelle, 5,12:22:32.</span><span class="sxs-lookup"><span data-stu-id="d4053-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="d4053-242">-   Hebdomadaire, JOUR,HH:MM:SS, par exemple, Hebdomadaire, Mardi, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="d4053-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="d4053-243">-   Quotidienne, HH:MM:SS, par exemple, Quotidienne, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="d4053-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="d4053-244">-  Aucune  indique que les mises à jour Windows Update ne doivent pas être effectuées.</span><span class="sxs-lookup"><span data-stu-id="d4053-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="d4053-245">Notez que toutes les heures de hello sont au format UTC.</span><span class="sxs-lookup"><span data-stu-id="d4053-245">Note that all hello times are in UTC.</span></span>|
| <span data-ttu-id="d4053-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="d4053-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="d4053-247">Bool</span><span class="sxs-lookup"><span data-stu-id="d4053-247">Bool</span></span> <br><span data-ttu-id="d4053-248">(Par défaut : true)</span><span class="sxs-lookup"><span data-stu-id="d4053-248">(Default: true)</span></span> | <span data-ttu-id="d4053-249">En définissant cet indicateur, application hello accepte hello contrat de licence par l’utilisateur pour Windows Update pour le compte de propriétaire hello de l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-249">By setting this flag, hello application accepts hello End-User License Agreement for Windows Update on behalf of hello owner of hello machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="d4053-250">Si vous souhaitez que Windows Update toohappen immédiatement, définissez `WUFrequency` le temps de déploiement d’application toohello relatif.</span><span class="sxs-lookup"><span data-stu-id="d4053-250">If you want Windows Update toohappen immediately, set `WUFrequency` relative toohello application deployment time.</span></span> <span data-ttu-id="d4053-251">Par exemple, supposons que vous avez une application de hello de toodeploy cluster et le plan de test de nœud de cinq à environ 5 h 00 UTC.</span><span class="sxs-lookup"><span data-stu-id="d4053-251">For example, suppose that you have a five-node test cluster and plan toodeploy hello app at around 5:00 PM UTC.</span></span> <span data-ttu-id="d4053-252">Si vous supposez que le déploiement ou mise à niveau des applications hello prend 30 minutes à hello hello maximale, définissez WUFrequency en tant que « Tous les jours, 17:30:00. »</span><span class="sxs-lookup"><span data-stu-id="d4053-252">If you assume that hello application upgrade or deployment takes 30 minutes at hello maximum, set hello WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-hello-app"></a><span data-ttu-id="d4053-253">Déployer l’application hello</span><span class="sxs-lookup"><span data-stu-id="d4053-253">Deploy hello app</span></span>

1. <span data-ttu-id="d4053-254">Terminer tous les clusters de hello de tooprepare hello étapes préliminaires.</span><span class="sxs-lookup"><span data-stu-id="d4053-254">Finish all hello prerequisite steps tooprepare hello cluster.</span></span>
2. <span data-ttu-id="d4053-255">Déploiement d’une application d’orchestration de correctif hello comme toute autre application de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d4053-255">Deploy hello patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="d4053-256">Vous pouvez déployer l’application hello à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4053-256">You can deploy hello app by using PowerShell.</span></span> <span data-ttu-id="d4053-257">Suivez les étapes de hello dans [déployer et supprimer des applications à l’aide de PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="d4053-257">Follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="d4053-258">application de hello tooconfigure au moment de hello du déploiement, passez hello `ApplicationParamater` toohello `New-ServiceFabricApplication` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d4053-258">tooconfigure hello application at hello time of deployment, pass hello `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="d4053-259">Pour votre commodité, nous vous avons fourni script hello Deploy.ps1 en même temps que l’application hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-259">For your convenience, we’ve provided hello script Deploy.ps1 along with hello application.</span></span> <span data-ttu-id="d4053-260">script de hello toouse :</span><span class="sxs-lookup"><span data-stu-id="d4053-260">toouse hello script:</span></span>

    - <span data-ttu-id="d4053-261">Connecter le cluster Service Fabric de tooa à l’aide de `Connect-ServiceFabricCluster`.</span><span class="sxs-lookup"><span data-stu-id="d4053-261">Connect tooa Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="d4053-262">Exécuter le script hello PowerShell Deploy.ps1 avec hello approprié `ApplicationParameter` valeur.</span><span class="sxs-lookup"><span data-stu-id="d4053-262">Execute hello PowerShell script Deploy.ps1 with hello appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="d4053-263">Conserver le script de hello et le dossier de l’application hello PatchOrchestrationApplication Bonjour même répertoire.</span><span class="sxs-lookup"><span data-stu-id="d4053-263">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="upgrade-hello-app"></a><span data-ttu-id="d4053-264">Mise à niveau d’application hello</span><span class="sxs-lookup"><span data-stu-id="d4053-264">Upgrade hello app</span></span>

<span data-ttu-id="d4053-265">tooupgrade une application d’orchestration correctif existante à l’aide de PowerShell, suivez les étapes de hello dans [mise à niveau de l’application Service Fabric à l’aide de PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span><span class="sxs-lookup"><span data-stu-id="d4053-265">tooupgrade an existing patch orchestration app by using PowerShell, follow hello steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-hello-app"></a><span data-ttu-id="d4053-266">Supprimer l’application hello</span><span class="sxs-lookup"><span data-stu-id="d4053-266">Remove hello app</span></span>

<span data-ttu-id="d4053-267">application de hello tooremove, suivez les étapes hello dans [déployer et supprimer des applications à l’aide de PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="d4053-267">tooremove hello application, follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="d4053-268">Pour votre commodité, nous vous avons fourni script hello Undeploy.ps1 en même temps que l’application hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-268">For your convenience, we've provided hello script Undeploy.ps1 along with hello application.</span></span> <span data-ttu-id="d4053-269">script de hello toouse :</span><span class="sxs-lookup"><span data-stu-id="d4053-269">toouse hello script:</span></span>

  - <span data-ttu-id="d4053-270">Connecter le cluster Service Fabric de tooa à l’aide de ```Connect-ServiceFabricCluster```.</span><span class="sxs-lookup"><span data-stu-id="d4053-270">Connect tooa Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="d4053-271">Exécuter le script PowerShell de hello Undeploy.ps1.</span><span class="sxs-lookup"><span data-stu-id="d4053-271">Execute hello PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="d4053-272">Conserver le script de hello et le dossier de l’application hello PatchOrchestrationApplication Bonjour même répertoire.</span><span class="sxs-lookup"><span data-stu-id="d4053-272">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="view-hello-windows-update-results"></a><span data-ttu-id="d4053-273">Afficher les résultats de mise à jour de Windows hello</span><span class="sxs-lookup"><span data-stu-id="d4053-273">View hello Windows Update results</span></span>

<span data-ttu-id="d4053-274">application d’orchestration Hello correctif expose utilisateur toohello d’API REST toodisplay hello historique des résultats.</span><span class="sxs-lookup"><span data-stu-id="d4053-274">hello patch orchestration app exposes REST APIs toodisplay hello historical results toohello user.</span></span> <span data-ttu-id="d4053-275">Un exemple de résultat de hello JSON :</span><span class="sxs-lookup"><span data-stu-id="d4053-275">An example of hello result JSON:</span></span>
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
<span data-ttu-id="d4053-276">Si aucune mise à jour n’est planifiée encore, le résultat de hello JSON est vide.</span><span class="sxs-lookup"><span data-stu-id="d4053-276">If no update is scheduled yet, hello result JSON is empty.</span></span>

<span data-ttu-id="d4053-277">Consigner les résultats dans un cluster de toohello tooquery mise à jour de Windows.</span><span class="sxs-lookup"><span data-stu-id="d4053-277">Log in toohello cluster tooquery Windows Update results.</span></span> <span data-ttu-id="d4053-278">Puis savoir adresse hello réplica principal hello Hello coordinateur Service et d’accès URL hello à partir du navigateur de hello : http://&lt;IP de RÉPLICA&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="d4053-278">Then find out hello replica address for hello primary of hello Coordinator Service, and hit hello URL from hello browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="d4053-279">point de terminaison REST Hello pour hello coordinateur Service dispose d’un port dynamique.</span><span class="sxs-lookup"><span data-stu-id="d4053-279">hello REST endpoint for hello Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="d4053-280">toocheck hello URL exacte, consultez le toohello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="d4053-280">toocheck hello exact URL, refer toohello Service Fabric Explorer.</span></span> <span data-ttu-id="d4053-281">Par exemple, les résultats de hello sont disponibles sur `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span><span class="sxs-lookup"><span data-stu-id="d4053-281">For example, hello results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![Image de point de terminaison REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="d4053-283">Si le proxy inverse de hello est activé sur le cluster de hello, vous pouvez accéder à des URL hello à partir d’en dehors du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-283">If hello reverse proxy is enabled on hello cluster, you can access hello URL from outside of hello cluster as well.</span></span>
<span data-ttu-id="d4053-284">Hello du point de terminaison doit toobe atteint est http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="d4053-284">hello endpoint that needs toobe hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="d4053-285">proxy inverse de hello tooenable sur le cluster de hello, suivez les étapes de hello dans [proxy dans Azure Service Fabric inverse](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span><span class="sxs-lookup"><span data-stu-id="d4053-285">tooenable hello reverse proxy on hello cluster, follow hello steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="d4053-286">Après la configuration de proxy inverse de hello, tous les services cluster de hello micro qui exposent un point de terminaison HTTP sont adressables à partir de l’extérieur hello cluster.</span><span class="sxs-lookup"><span data-stu-id="d4053-286">After hello reverse proxy is configured, all micro services in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="d4053-287">Événements de diagnostic et d’intégrité</span><span class="sxs-lookup"><span data-stu-id="d4053-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="d4053-288">Collecter les journaux de l’application d’orchestration des correctifs</span><span class="sxs-lookup"><span data-stu-id="d4053-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="d4053-289">Depuis la version du runtime `5.6.220.9494`, les journaux de l’application d’orchestration des correctifs sont collectés en même temps que les journaux Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d4053-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="d4053-290">Pour les clusters exécutant la version du runtime Service Fabric moins `5.6.220.9494`, les journaux peuvent être collectées à l’aide d’une des méthodes suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of hello following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="d4053-291">Localement sur chaque nœud</span><span class="sxs-lookup"><span data-stu-id="d4053-291">Locally on each node</span></span>

<span data-ttu-id="d4053-292">Si la version du runtime Service Fabric est inférieure à `5.6.220.9494`, les journaux sont collectés en local sur chaque nœud du cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d4053-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="d4053-293">Bonjour emplacement tooaccess hello journaux est \[Service Fabric\_Installation\_lecteur\]:\\PatchOrchestrationApplication\\journaux.</span><span class="sxs-lookup"><span data-stu-id="d4053-293">hello location tooaccess hello logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="d4053-294">Par exemple, si le Service Fabric est installé sur le lecteur D, chemin d’accès hello est D:\\PatchOrchestrationApplication\\journaux.</span><span class="sxs-lookup"><span data-stu-id="d4053-294">For example, if Service Fabric is installed on drive D, hello path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="d4053-295">Emplacement central</span><span class="sxs-lookup"><span data-stu-id="d4053-295">Central location</span></span>

<span data-ttu-id="d4053-296">Si les Diagnostics Azure est configuré en tant que partie des étapes requises, les journaux pour l’application d’orchestration hello correctif sont disponibles dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d4053-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for hello patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="d4053-297">Rapports d'intégrité</span><span class="sxs-lookup"><span data-stu-id="d4053-297">Health reports</span></span>

<span data-ttu-id="d4053-298">application d’orchestration Hello correctif publie également les rapports d’intégrité sur hello Service coordinateur ou hello Service Agent de nœud Bonjour suivant cas :</span><span class="sxs-lookup"><span data-stu-id="d4053-298">hello patch orchestration app also publishes health reports against hello Coordinator Service or hello Node Agent Service in hello following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="d4053-299">Une opération de Windows Update a échoué</span><span class="sxs-lookup"><span data-stu-id="d4053-299">A Windows Update operation failed</span></span>

<span data-ttu-id="d4053-300">Si une opération de mise à jour Windows échoue sur un nœud, un rapport d’intégrité est généré sur hello Service Agent de nœud.</span><span class="sxs-lookup"><span data-stu-id="d4053-300">If a Windows Update operation fails on a node, a health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="d4053-301">Détails du rapport de contrôle d’intégrité hello contiennent le nom du nœud problématique hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-301">Details of hello health report contain hello problematic node name.</span></span>

<span data-ttu-id="d4053-302">Une fois la mise à jour corrective est effectuée avec succès sur le nœud de problématique hello, rapport de hello est automatiquement effacé.</span><span class="sxs-lookup"><span data-stu-id="d4053-302">After patching is successfully completed on hello problematic node, hello report is automatically cleared.</span></span>

#### <a name="hello-node-agent-ntservice-is-down"></a><span data-ttu-id="d4053-303">Hello du service NT de l’Agent de nœud est arrêté</span><span class="sxs-lookup"><span data-stu-id="d4053-303">hello Node Agent NTService is down</span></span>

<span data-ttu-id="d4053-304">Si hello du service NT de l’Agent de nœud est arrêté sur un nœud, un rapport d’intégrité du niveau d’avertissement est généré par rapport à hello Service Agent de nœud.</span><span class="sxs-lookup"><span data-stu-id="d4053-304">If hello Node Agent NTService is down on a node, a warning-level health report is generated against hello Node Agent Service.</span></span>

#### <a name="hello-repair-manager-service-is-not-enabled"></a><span data-ttu-id="d4053-305">service de gestionnaire de réparation Hello n’est pas activé.</span><span class="sxs-lookup"><span data-stu-id="d4053-305">hello repair manager service is not enabled</span></span>

<span data-ttu-id="d4053-306">Si le service de gestionnaire de réparation hello est introuvable sur le cluster de hello, un rapport d’intégrité du niveau d’avertissement est généré pour hello Service coordinateur.</span><span class="sxs-lookup"><span data-stu-id="d4053-306">If hello repair manager service is not found on hello cluster, a warning-level health report is generated for hello Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="d4053-307">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="d4053-307">Frequently asked questions</span></span>

<span data-ttu-id="d4053-308">Q :</span><span class="sxs-lookup"><span data-stu-id="d4053-308">Q.</span></span> <span data-ttu-id="d4053-309">**Pourquoi mon cluster dans un état d’erreur lors de l’application d’orchestration hello correctif est en cours d’exécution ?**</span><span class="sxs-lookup"><span data-stu-id="d4053-309">**Why do I see my cluster in an error state when hello patch orchestration app is running?**</span></span>

<span data-ttu-id="d4053-310">R :</span><span class="sxs-lookup"><span data-stu-id="d4053-310">A.</span></span> <span data-ttu-id="d4053-311">Au cours du processus d’installation hello, application d’orchestration hello correctif désactive ou redémarre les nœuds, ce qui peuvent provoquer temporairement une intégrité de cluster hello descendent hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-311">During hello installation process, hello patch orchestration app disables or restarts nodes, which can temporarily result in hello health of hello cluster going down.</span></span>

<span data-ttu-id="d4053-312">Selon la stratégie de hello pour une application hello, soit un seul nœud peut s’arrêtent pendant une opération de mise à jour corrective *ou* tout un domaine de mise à niveau peut accéder simultanément vers le bas.</span><span class="sxs-lookup"><span data-stu-id="d4053-312">Based on hello policy for hello application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="d4053-313">Fin de hello de hello installation mise à jour de Windows, hello réactiver des nœuds après le redémarrage.</span><span class="sxs-lookup"><span data-stu-id="d4053-313">By hello end of hello Windows Update installation, hello nodes are reenabled post restart.</span></span>

<span data-ttu-id="d4053-314">Dans l’exemple suivant de hello, cluster de hello est allé état d’erreur tooan temporairement, car les deux nœuds ont été vers le bas et hello MaxPercentageUnhealthNodes stratégie a été violée.</span><span class="sxs-lookup"><span data-stu-id="d4053-314">In hello following example, hello cluster went tooan error state temporarily because two nodes were down and hello MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="d4053-315">Erreur de Hello est temporaire jusqu'à ce que l’opération de mise à jour corrective de hello est en cours.</span><span class="sxs-lookup"><span data-stu-id="d4053-315">hello error is temporary until hello patching operation is ongoing.</span></span>

![Image de cluster défectueux](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="d4053-317">Si hello problème persiste, consultez Dépannage toohello.</span><span class="sxs-lookup"><span data-stu-id="d4053-317">If hello issue persists, refer toohello Troubleshooting section.</span></span>

<span data-ttu-id="d4053-318">Q :</span><span class="sxs-lookup"><span data-stu-id="d4053-318">Q.</span></span> <span data-ttu-id="d4053-319">**L’application d’orchestration des correctifs est en état d’avertissement**</span><span class="sxs-lookup"><span data-stu-id="d4053-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="d4053-320">R :</span><span class="sxs-lookup"><span data-stu-id="d4053-320">A.</span></span> <span data-ttu-id="d4053-321">Vérifiez toosee si un rapport d’intégrité validé par rapport à l’application hello est la cause première hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-321">Check toosee if a health report posted against hello application is hello root cause.</span></span> <span data-ttu-id="d4053-322">En règle générale, les avertissement hello contient les détails du problème de hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-322">Usually, hello warning contains details of hello problem.</span></span> <span data-ttu-id="d4053-323">Si le problème de hello est transitoire, application hello est attendu tooauto-restaurer à partir de cet état.</span><span class="sxs-lookup"><span data-stu-id="d4053-323">If hello issue is transient, hello application is expected tooauto-recover from this state.</span></span>

<span data-ttu-id="d4053-324">Q :</span><span class="sxs-lookup"><span data-stu-id="d4053-324">Q.</span></span> <span data-ttu-id="d4053-325">**Que puis-je faire si mon cluster n’est pas intègre et que j’ai besoin d’une mise à jour des systèmes d’exploitation urgente de toodo ?**</span><span class="sxs-lookup"><span data-stu-id="d4053-325">**What can I do if my cluster is unhealthy and I need toodo an urgent operating system update?**</span></span>

<span data-ttu-id="d4053-326">R :</span><span class="sxs-lookup"><span data-stu-id="d4053-326">A.</span></span> <span data-ttu-id="d4053-327">application d’orchestration Hello correctif n’installe pas les mises à jour pendant que le cluster de hello n’est pas sain.</span><span class="sxs-lookup"><span data-stu-id="d4053-327">hello patch orchestration app does not install updates while hello cluster is unhealthy.</span></span> <span data-ttu-id="d4053-328">Essayez toobring votre cluster tooa état sain toounblock hello correctif orchestration application flux de travail.</span><span class="sxs-lookup"><span data-stu-id="d4053-328">Try toobring your cluster tooa healthy state toounblock hello patch orchestration app workflow.</span></span>

<span data-ttu-id="d4053-329">Q :</span><span class="sxs-lookup"><span data-stu-id="d4053-329">Q.</span></span> <span data-ttu-id="d4053-330">**Pourquoi mise à jour corrective sur tous les clusters si longue toorun ?**</span><span class="sxs-lookup"><span data-stu-id="d4053-330">**Why does patching across clusters take so long toorun?**</span></span>

<span data-ttu-id="d4053-331">R :</span><span class="sxs-lookup"><span data-stu-id="d4053-331">A.</span></span> <span data-ttu-id="d4053-332">Durée Hello requise par l’application d’orchestration hello correctif dépend principalement de hello suivant facteurs :</span><span class="sxs-lookup"><span data-stu-id="d4053-332">hello time needed by hello patch orchestration app is mostly dependent on hello following factors:</span></span>

- <span data-ttu-id="d4053-333">stratégie de Hello de hello Service coordinateur.</span><span class="sxs-lookup"><span data-stu-id="d4053-333">hello policy of hello Coordinator Service.</span></span> 
  - <span data-ttu-id="d4053-334">Hello stratégie par défaut, `NodeWise`, entraîne la mise à jour corrective de qu’un seul nœud à la fois.</span><span class="sxs-lookup"><span data-stu-id="d4053-334">hello default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="d4053-335">En particulier dans les cas de hello des clusters de plus grandes, nous vous recommandons d’utiliser hello `UpgradeDomainWise` tooachieve stratégie plus rapide de mise à jour corrective sur tous les clusters.</span><span class="sxs-lookup"><span data-stu-id="d4053-335">Especially in hello case of bigger clusters, we recommend that you use hello `UpgradeDomainWise` policy tooachieve faster patching across clusters.</span></span>
- <span data-ttu-id="d4053-336">nombre de Hello de mises à jour disponibles pour téléchargement et l’installation.</span><span class="sxs-lookup"><span data-stu-id="d4053-336">hello number of updates available for download and installation.</span></span> 
- <span data-ttu-id="d4053-337">Hello toodownload de temps moyen nécessité et installer une mise à jour, qui ne doit pas dépasser quelques heures.</span><span class="sxs-lookup"><span data-stu-id="d4053-337">hello average time needed toodownload and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="d4053-338">Hello les performances de la bande passante réseau et de la machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-338">hello performance of hello VM and network bandwidth.</span></span>

<span data-ttu-id="d4053-339">Q :</span><span class="sxs-lookup"><span data-stu-id="d4053-339">Q.</span></span> <span data-ttu-id="d4053-340">**Pourquoi certaines mises à jour dans les résultats de la mise à jour Windows obtenues via les api REST, mais pas sous hello l’historique de Windows Update sur l’ordinateur**</span><span class="sxs-lookup"><span data-stu-id="d4053-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under hello Windows Update history on machine?**</span></span>

<span data-ttu-id="d4053-341">R :</span><span class="sxs-lookup"><span data-stu-id="d4053-341">A.</span></span> <span data-ttu-id="d4053-342">Certaines mises à jour du produit doivent toobe archivé leur historique de mise à jour/patch respectifs.</span><span class="sxs-lookup"><span data-stu-id="d4053-342">Some product updates need toobe checked in their respective update/patch history.</span></span> <span data-ttu-id="d4053-343">Ainsi, les mises à jour de Windows Defender ne s’affichent pas dans l’historique Windows Update de Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d4053-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="d4053-344">Clauses d’exclusion de responsabilité</span><span class="sxs-lookup"><span data-stu-id="d4053-344">Disclaimers</span></span>

- <span data-ttu-id="d4053-345">application d’orchestration Hello correctif accepte hello contrat de licence par l’utilisateur de Windows Update pour le compte d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-345">hello patch orchestration app accepts hello End-User License Agreement of Windows Update on behalf of hello user.</span></span> <span data-ttu-id="d4053-346">Si vous le souhaitez, paramètre de hello peut être désactivée dans la configuration de hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-346">Optionally, hello setting can be turned off in hello configuration of hello application.</span></span>

- <span data-ttu-id="d4053-347">application d’orchestration Hello correctif collecte des performances et l’utilisation de télémétrie tootrack.</span><span class="sxs-lookup"><span data-stu-id="d4053-347">hello patch orchestration app collects telemetry tootrack usage and performance.</span></span> <span data-ttu-id="d4053-348">données de télémétrie de l’application Hello suivant le paramètre hello du paramètre de télémétrie du runtime de Service Fabric hello (qui est activée par défaut).</span><span class="sxs-lookup"><span data-stu-id="d4053-348">hello application’s telemetry follows hello setting of hello Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d4053-349">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="d4053-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-tooup-state"></a><span data-ttu-id="d4053-350">Un nœud ne provient pas revenir tooup état</span><span class="sxs-lookup"><span data-stu-id="d4053-350">A node is not coming back tooup state</span></span>

<span data-ttu-id="d4053-351">**nœud de Hello peut être bloquée dans un état de désactivation, car**:</span><span class="sxs-lookup"><span data-stu-id="d4053-351">**hello node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="d4053-352">Une vérification de sécurité est en attente.</span><span class="sxs-lookup"><span data-stu-id="d4053-352">A safety check is pending.</span></span> <span data-ttu-id="d4053-353">tooremedy cette situation, assurez-vous que suffisamment de nœuds est disponibles dans un état sain.</span><span class="sxs-lookup"><span data-stu-id="d4053-353">tooremedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="d4053-354">**nœud de Hello peut être bloquée dans un état désactivé, car**:</span><span class="sxs-lookup"><span data-stu-id="d4053-354">**hello node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="d4053-355">nœud de Hello a été désactivé manuellement.</span><span class="sxs-lookup"><span data-stu-id="d4053-355">hello node was disabled manually.</span></span>
- <span data-ttu-id="d4053-356">nœud de Hello a été désactivée en raison de travail d’infrastructure Azure en cours tooan.</span><span class="sxs-lookup"><span data-stu-id="d4053-356">hello node was disabled due tooan ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="d4053-357">nœud de Hello a été désactivé temporairement par hello correctif application toopatch hello ce nœud.</span><span class="sxs-lookup"><span data-stu-id="d4053-357">hello node was disabled temporarily by hello patch orchestration app toopatch hello node.</span></span>

<span data-ttu-id="d4053-358">**Hello nœud peut être bloqué dans un état hors service car**:</span><span class="sxs-lookup"><span data-stu-id="d4053-358">**hello node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="d4053-359">nœud de Hello a été mis hors service manuellement.</span><span class="sxs-lookup"><span data-stu-id="d4053-359">hello node was put in a down state manually.</span></span>
- <span data-ttu-id="d4053-360">nœud de Hello est en cours de redémarrage (qui peut être déclenché par application d’orchestration hello correctif).</span><span class="sxs-lookup"><span data-stu-id="d4053-360">hello node is undergoing a restart (which might be triggered by hello patch orchestration app).</span></span>
- <span data-ttu-id="d4053-361">nœud de Hello est arrêté en raison de tooa défectueux machine virtuelle ou ordinateur ou réseau problèmes de connectivité.</span><span class="sxs-lookup"><span data-stu-id="d4053-361">hello node is down due tooa faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="d4053-362">Lises à jour ont été ignorés sur certains nœuds</span><span class="sxs-lookup"><span data-stu-id="d4053-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="d4053-363">application d’orchestration Hello correctif tente tooinstall une stratégie Windows update conséquente toohello replanification.</span><span class="sxs-lookup"><span data-stu-id="d4053-363">hello patch orchestration app tries tooinstall a Windows update according toohello rescheduling policy.</span></span> <span data-ttu-id="d4053-364">service de Hello tente de nœud de hello toorecover et ignorer la stratégie d’application toohello conséquente hello mise à jour.</span><span class="sxs-lookup"><span data-stu-id="d4053-364">hello service tries toorecover hello node and skip hello update according toohello application policy.</span></span>

<span data-ttu-id="d4053-365">Dans ce cas, un rapport d’intégrité du niveau d’avertissement est généré par rapport à hello Service Agent de nœud.</span><span class="sxs-lookup"><span data-stu-id="d4053-365">In such a case, a warning-level health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="d4053-366">résultat de Hello pour la mise à jour de Windows contient également des raisons de l’échec de hello hello.</span><span class="sxs-lookup"><span data-stu-id="d4053-366">hello result for Windows Update also contains hello possible reason for hello failure.</span></span>

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a><span data-ttu-id="d4053-367">contrôle d’intégrité Hello du cluster de hello passe tooerror pendant l’installation de mise à jour hello</span><span class="sxs-lookup"><span data-stu-id="d4053-367">hello health of hello cluster goes tooerror while hello update installs</span></span>

<span data-ttu-id="d4053-368">Une mise à jour Windows défectueux peut arrêter de contrôle d’intégrité hello d’une application ou d’un cluster sur un nœud particulier ou d’un domaine de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="d4053-368">A faulty Windows update can bring down hello health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="d4053-369">application d’orchestration Hello correctif interrompt toutes les opérations de mise à jour Windows jusqu'à ce que le cluster de hello est à nouveau intègre.</span><span class="sxs-lookup"><span data-stu-id="d4053-369">hello patch orchestration app discontinues any subsequent Windows Update operation until hello cluster is healthy again.</span></span>

<span data-ttu-id="d4053-370">Un administrateur doit intervenir et déterminer pourquoi application hello ou un cluster est devenu non intègre d’échéance tooWindows mise à jour.</span><span class="sxs-lookup"><span data-stu-id="d4053-370">An administrator must intervene and determine why hello application or cluster became unhealthy due tooWindows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="d4053-371">Notes de publication :</span><span class="sxs-lookup"><span data-stu-id="d4053-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="d4053-372">Version 1.1.0</span><span class="sxs-lookup"><span data-stu-id="d4053-372">Version 1.1.0</span></span>
- <span data-ttu-id="d4053-373">Version publique</span><span class="sxs-lookup"><span data-stu-id="d4053-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="d4053-374">Version 1.1.1</span><span class="sxs-lookup"><span data-stu-id="d4053-374">Version 1.1.1</span></span>
- <span data-ttu-id="d4053-375">Correction d’un bogue dans le paramètre SetupEntryPoint de NodeAgentService, qui empêchait l’installation de NodeAgentNTService.</span><span class="sxs-lookup"><span data-stu-id="d4053-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="d4053-376">Version 1.2.0 (dernière version)</span><span class="sxs-lookup"><span data-stu-id="d4053-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="d4053-377">Résolution de bogues liés au flux de travail de redémarrage du système.</span><span class="sxs-lookup"><span data-stu-id="d4053-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="d4053-378">Correctif de bogue dans la création de tâches du Gestionnaire de ressources en raison de la vérification d’intégrité de toowhich pendant la préparation des tâches de réparation ne se produisait pas comme prévu.</span><span class="sxs-lookup"><span data-stu-id="d4053-378">Bug fix in creation of RM tasks due toowhich health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="d4053-379">Mode de démarrage hello modifié pour le service windows POANodeSvc automatique toodelayed-auto.</span><span class="sxs-lookup"><span data-stu-id="d4053-379">Changed hello startup mode for windows service POANodeSvc from auto toodelayed-auto.</span></span>
