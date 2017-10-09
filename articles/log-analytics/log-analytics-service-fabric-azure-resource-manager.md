---
title: "aaaAssess des applications de Service Fabric à l’aide de l’Analytique de journal hello portail Azure | Documents Microsoft"
description: "Vous pouvez utiliser la solution de Service Fabric hello dans Analytique de journal à l’aide de risque de hello hello tooassess portail Azure et de l’intégrité de vos applications de Service Fabric, micro-services, les nœuds et les clusters."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a><span data-ttu-id="5fb08-103">Évaluer des applications de Service Fabric et micro-services avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5fb08-103">Assess Service Fabric applications and micro-services with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5fb08-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="5fb08-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="5fb08-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fb08-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Symbole Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="5fb08-107">Cet article décrit comment toouse hello solution de l’infrastructure de Service dans le journal Analytique toohelp identifier et résoudre les problèmes sur votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5fb08-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="5fb08-108">Hello solution d’infrastructure de Service utilise des données de Diagnostics Windows Azure à partir de vos machines virtuelles de l’infrastructure Service, collecte des données de vos tables WAD d’Azure.</span><span class="sxs-lookup"><span data-stu-id="5fb08-108">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="5fb08-109">Log Analytics lit ensuite les événements d’infrastructure Service Fabric, notamment les **événements de service fiable**, les **événements d’acteurs**, les **événements opérationnels** et les **événements ETW personnalisés**.</span><span class="sxs-lookup"><span data-stu-id="5fb08-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="5fb08-110">Avec hello solution du tableau de bord, vous êtes tooview en mesure de détecter les problèmes importants et les événements pertinents dans votre environnement de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5fb08-110">With hello solution dashboard, you are able tooview notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="5fb08-111">tooget solution de hello en main, vous devez tooconnect votre espace de travail Analytique des journaux de tooa cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5fb08-111">tooget started with hello solution, you need tooconnect your Service Fabric cluster tooa Log Analytics workspace.</span></span> <span data-ttu-id="5fb08-112">Voici trois scénarios tooconsider :</span><span class="sxs-lookup"><span data-stu-id="5fb08-112">Here are three scenarios tooconsider:</span></span>

1. <span data-ttu-id="5fb08-113">Si vous n’avez pas déployé votre cluster Service Fabric, utilisez les étapes de hello dans ***déployer un espace de travail Analytique des journaux de Cluster Service Fabric connecté tooa*** toodeploy un nouveau cluster et de le configurer tooreport tooLog Analytique.</span><span class="sxs-lookup"><span data-stu-id="5fb08-113">If you have not deployed your Service Fabric cluster, use hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace*** toodeploy a new cluster and have it configured tooreport tooLog Analytics.</span></span>
2. <span data-ttu-id="5fb08-114">Si vous avez besoin des compteurs de performance toocollect à partir de votre toouse hôtes autres solutions OMS, telles que la sécurité sur votre Cluster Service Fabric, suivez les étapes de hello dans ***déployer un espace de travail Analytique des journaux de tooa Cluster Service Fabric connecté avec l’Extension de machine virtuelle installé.***</span><span class="sxs-lookup"><span data-stu-id="5fb08-114">If you need toocollect performance counters from your hosts toouse other OMS solutions such as Security on your Service Fabric Cluster, follow hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="5fb08-115">Si vous avez déjà déployé votre cluster Service Fabric et que vous souhaitez tooconnect il tooLog Analytique, suivez les étapes de hello dans ***Ajout d’un tooLog de compte de stockage existant Analytique.***</span><span class="sxs-lookup"><span data-stu-id="5fb08-115">If you have already deployed your Service Fabric cluster and want tooconnect it tooLog Analytics, follow hello steps in ***Adding an existing storage account tooLog Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a><span data-ttu-id="5fb08-116">Déployer un espace de travail de Cluster Service Fabric connecté tooa Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="5fb08-116">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace.</span></span>
<span data-ttu-id="5fb08-117">Ce modèle hello suivant :</span><span class="sxs-lookup"><span data-stu-id="5fb08-117">This template does hello following:</span></span>

1. <span data-ttu-id="5fb08-118">Déploie un espace de travail Azure Service Fabric cluster déjà connecté tooa Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="5fb08-118">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="5fb08-119">Vous avez hello option toocreate d’un espace de travail lors du déploiement de modèle de hello, ou nom d’entrée hello d’espace de travail Analytique de journal déjà existant.</span><span class="sxs-lookup"><span data-stu-id="5fb08-119">You have hello option toocreate a new workspace while deploying hello template, or input hello name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="5fb08-120">Ajoute un espace de travail hello le stockage des diagnostics compte toohello Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="5fb08-120">Adds hello diagnostic storage account toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="5fb08-121">Permet la solution de Service Fabric hello dans votre espace de travail Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="5fb08-121">Enables hello Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="5fb08-122">[![Déployer tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="5fb08-122">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="5fb08-123">Une fois que vous sélectionnez hello déployer bouton ci-dessus, hello Azure portail s’ouvre et affiche les paramètres pour vous tooedit.</span><span class="sxs-lookup"><span data-stu-id="5fb08-123">Once you select hello deploy button above, hello Azure portal opens with parameters for you tooedit.</span></span> <span data-ttu-id="5fb08-124">Si vous entrez un nouveau nom d’espace de travail Analytique des journaux, être toocreate assurer un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="5fb08-124">Be sure toocreate a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="5fb08-127">Acceptez les conditions juridiques hello et cliquez sur **créer** déploiement de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="5fb08-127">Accept hello legal terms and click **Create** toostart hello deployment.</span></span> <span data-ttu-id="5fb08-128">Une fois le déploiement de hello est terminé, vous devez voir le nouvel espace de travail hello et cluster créé et hello WADServiceFabric * WADETWEvent, WADWindowsEventLogs et événements tables ajoutées :</span><span class="sxs-lookup"><span data-stu-id="5fb08-128">Once hello deployment is completed, you should see hello new workspace and cluster created, and hello WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="5fb08-130">Déployer un espace de travail de Cluster Service Fabric connecté tooa Analytique de journal avec l’Extension de machine virtuelle installé.</span><span class="sxs-lookup"><span data-stu-id="5fb08-130">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="5fb08-131">Ce modèle hello suivant :</span><span class="sxs-lookup"><span data-stu-id="5fb08-131">This template does hello following:</span></span>

1. <span data-ttu-id="5fb08-132">Déploie un espace de travail Azure Service Fabric cluster déjà connecté tooa Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="5fb08-132">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="5fb08-133">Vous pouvez créer un espace de travail ou utiliser un espace de travail existant.</span><span class="sxs-lookup"><span data-stu-id="5fb08-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="5fb08-134">Ajoute un espace de travail hello le stockage des diagnostics comptes toohello Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="5fb08-134">Adds hello diagnostic storage accounts toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="5fb08-135">Permet la solution de Service Fabric hello dans l’espace de travail hello Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="5fb08-135">Enables hello Service Fabric solution in hello Log Analytics workspace.</span></span>
4. <span data-ttu-id="5fb08-136">Installe l’extension de l’agent MMA hello dans l’échelle de chaque ordinateur virtuel défini dans votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5fb08-136">Installs hello MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="5fb08-137">Agent hello MMA est installé, vous êtes tooview en mesure de performances sur vos nœuds.</span><span class="sxs-lookup"><span data-stu-id="5fb08-137">With hello MMA agent installed, you are able tooview performance metrics about your nodes.</span></span>

<span data-ttu-id="5fb08-138">[![Déployer tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="5fb08-138">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="5fb08-139">Suivant hello les mêmes étapes ci-dessus, les paramètres d’entrée hello nécessaires et déclencher un déploiement.</span><span class="sxs-lookup"><span data-stu-id="5fb08-139">Following hello same steps above, input hello necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="5fb08-140">Une fois encore, vous devez voir l’espace de travail hello, le cluster et tables WAD créés toutes les :</span><span class="sxs-lookup"><span data-stu-id="5fb08-140">Once again you should see hello new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="5fb08-142">Affichage des données de performances</span><span class="sxs-lookup"><span data-stu-id="5fb08-142">Viewing Performance Data</span></span>

<span data-ttu-id="5fb08-143">tooview des données de performances à partir de vos nœuds :</span><span class="sxs-lookup"><span data-stu-id="5fb08-143">tooview Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="5fb08-144">Lancer l’espace de travail hello Analytique de journal à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5fb08-144">Launch hello Log Analytics workspace from hello Azure portal.</span></span>
  <span data-ttu-id="5fb08-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="5fb08-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="5fb08-146">Accédez tooSettings sur le volet gauche de hello, puis sélectionnez les données >> compteurs de Performance Windows >> « Ajouter hello sélectionné les compteurs de performance » : ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="5fb08-146">Go tooSettings on hello left pane, and select Data >> Windows Performance Counters >> "Add hello selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="5fb08-147">Dans la recherche de journal, utilisez hello suivant toodelve de requêtes dans les métriques clés sur vos nœuds :</span><span class="sxs-lookup"><span data-stu-id="5fb08-147">In Log Search, use hello following queries toodelve into key metrics about your nodes:</span></span>

    <span data-ttu-id="5fb08-148">a.</span><span class="sxs-lookup"><span data-stu-id="5fb08-148">a.</span></span> <span data-ttu-id="5fb08-149">Comparaison hello utilisation moyenne du processeur sur tous les nœuds de votre dernière toosee une heure hello, les nœuds qui rencontrent des problèmes et à quel intervalle de temps, un nœud avait un pic d’activité :</span><span class="sxs-lookup"><span data-stu-id="5fb08-149">Compare hello average CPU Utilization across all your nodes in hello last one hour toosee which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="5fb08-151">b.</span><span class="sxs-lookup"><span data-stu-id="5fb08-151">b.</span></span> <span data-ttu-id="5fb08-152">Examinez des graphiques en courbes similaires pour la mémoire disponible sur chaque nœud avec cette requête :</span><span class="sxs-lookup"><span data-stu-id="5fb08-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="5fb08-153">tooview une liste de tous les nœuds, présentant les valeur moyenne de hello exact pour mégaoctets disponibles pour chaque nœud, utilisez cette requête :</span><span class="sxs-lookup"><span data-stu-id="5fb08-153">tooview a listing of all your nodes, showing hello exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="5fb08-155">c.</span><span class="sxs-lookup"><span data-stu-id="5fb08-155">c.</span></span> <span data-ttu-id="5fb08-156">Dans les cas de hello que vous souhaitez toodrill vers le bas dans un nœud spécifique en examinant la moyenne de toutes les heures hello, minimale, maximale et 75-centile utilisation du processeur, vous êtes en mesure de toodo en à l’aide de cette requête (remplacez le champ de l’ordinateur) :</span><span class="sxs-lookup"><span data-stu-id="5fb08-156">In hello case that you want toodrill down into a specific node by examining hello hourly average, minimum, maximum and 75-percentile CPU usage, you're able toodo this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="5fb08-158">En savoir plus sur les métriques de performances dans le journal Analytique à hello [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span><span class="sxs-lookup"><span data-stu-id="5fb08-158">Read more information about performance metrics in Log Analytics at hello [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-toolog-analytics"></a><span data-ttu-id="5fb08-159">Ajout d’un tooLog de compte de stockage existant Analytique</span><span class="sxs-lookup"><span data-stu-id="5fb08-159">Adding an existing storage account tooLog Analytics</span></span>

<span data-ttu-id="5fb08-160">Ce modèle ajoute simplement votre stockage comptes tooa nouveau ou existant Analytique de journal espace de travail existant.</span><span class="sxs-lookup"><span data-stu-id="5fb08-160">This template simply adds your existing storage accounts tooa new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="5fb08-161">[![Déployer tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="5fb08-161">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="5fb08-162">Dans la sélection d’un groupe de ressources, si vous travaillez avec un espace de travail Analytique de journal déjà existant, sélectionnez « Utiliser l’existante » et recherchez le groupe de ressources hello contenant l’espace de travail hello Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="5fb08-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for hello resource group containing hello Log Analytics workspace.</span></span> <span data-ttu-id="5fb08-163">Dans le cas contraire, créez-en un.</span><span class="sxs-lookup"><span data-stu-id="5fb08-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="5fb08-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="5fb08-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="5fb08-165">Une fois que ce modèle a été déployé, vous serez en mesure de toosee hello stockage compte connecté tooyour Analytique de journal espace de travail.</span><span class="sxs-lookup"><span data-stu-id="5fb08-165">After this template has been deployed, you will be able toosee hello storage account connected tooyour Log Analytics workspace.</span></span> <span data-ttu-id="5fb08-166">Dans ce cas, j’ai ajouté un plus stockage compte toohello Exchange espace de travail que j’ai créé ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="5fb08-166">In this instance, I added one more storage account toohello Exchange workspace I created above.</span></span>
<span data-ttu-id="5fb08-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="5fb08-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="5fb08-168">Afficher les événements Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5fb08-168">View Service Fabric events</span></span>

<span data-ttu-id="5fb08-169">Une fois que les déploiements de hello sont terminées et hello solution d’infrastructure de Service a été activée dans votre espace de travail, sélectionnez hello **Service Fabric** vignette dans le tableau de bord de Service Fabric hello Analytique de journal toolaunch portail hello.</span><span class="sxs-lookup"><span data-stu-id="5fb08-169">Once hello deployments are completed and hello Service Fabric solution has been enabled in your workspace, select hello **Service Fabric** tile in hello Log Analytics portal toolaunch hello Service Fabric dashboard.</span></span> <span data-ttu-id="5fb08-170">tableau de bord Hello inclut des colonnes de hello Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="5fb08-170">hello dashboard includes hello columns in hello following table.</span></span> <span data-ttu-id="5fb08-171">Chaque colonne répertorie les événements de 10 supérieure de hello en mettant en correspondance de nombre que les critères de la colonne pour hello spécifié de plage de temps.</span><span class="sxs-lookup"><span data-stu-id="5fb08-171">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="5fb08-172">Vous pouvez exécuter une recherche de journal qui fournit l’intégralité de la liste hello en cliquant sur **afficher tous les** à hello droite en bas de chaque colonne, ou en cliquant sur en-tête de colonne hello.</span><span class="sxs-lookup"><span data-stu-id="5fb08-172">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="5fb08-173">**Événement Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="5fb08-173">**Service Fabric event**</span></span> | <span data-ttu-id="5fb08-174">**description**</span><span class="sxs-lookup"><span data-stu-id="5fb08-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="5fb08-175">Problèmes notables</span><span class="sxs-lookup"><span data-stu-id="5fb08-175">Notable Issues</span></span> |<span data-ttu-id="5fb08-176">Affichage des problèmes tels que RunAsyncFailures RunAsynCancellations et des pannes de nœud.</span><span class="sxs-lookup"><span data-stu-id="5fb08-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="5fb08-177">Événements opérationnels</span><span class="sxs-lookup"><span data-stu-id="5fb08-177">Operational Events</span></span> |<span data-ttu-id="5fb08-178">Événements opérationnels notables, tels que les déploiements et mises à niveau d’application.</span><span class="sxs-lookup"><span data-stu-id="5fb08-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="5fb08-179">Événements de service fiable</span><span class="sxs-lookup"><span data-stu-id="5fb08-179">Reliable Service Events</span></span> |<span data-ttu-id="5fb08-180">Événements de service fiable notables, comme Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="5fb08-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="5fb08-181">Événements des acteurs</span><span class="sxs-lookup"><span data-stu-id="5fb08-181">Actor Events</span></span> |<span data-ttu-id="5fb08-182">Événements d’acteur notables générés par vos microservices, notamment les exceptions levées par une méthode d’acteur, les activations et désactivations d’acteur, etc.</span><span class="sxs-lookup"><span data-stu-id="5fb08-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="5fb08-183">Événements d’application</span><span class="sxs-lookup"><span data-stu-id="5fb08-183">Application Events</span></span> |<span data-ttu-id="5fb08-184">Tous les événements ETW personnalisés générés par vos applications.</span><span class="sxs-lookup"><span data-stu-id="5fb08-184">All custom ETW events generated by your applications.</span></span> |

![Tableau de bord Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Tableau de bord Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="5fb08-187">Hello tableau suivant montre les méthodes de collecte de données et d’autres détails sur la façon dont les données sont collectées pour Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5fb08-187">hello following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="5fb08-188">plateforme</span><span class="sxs-lookup"><span data-stu-id="5fb08-188">platform</span></span> | <span data-ttu-id="5fb08-189">Agent direct</span><span class="sxs-lookup"><span data-stu-id="5fb08-189">Direct Agent</span></span> | <span data-ttu-id="5fb08-190">Agent Operations Manager</span><span class="sxs-lookup"><span data-stu-id="5fb08-190">Operations Manager agent</span></span> | <span data-ttu-id="5fb08-191">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5fb08-191">Azure Storage</span></span> | <span data-ttu-id="5fb08-192">Operations Manager requis ?</span><span class="sxs-lookup"><span data-stu-id="5fb08-192">Operations Manager required?</span></span> | <span data-ttu-id="5fb08-193">Données de l’agent Operations Manager envoyées via un groupe d’administration</span><span class="sxs-lookup"><span data-stu-id="5fb08-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="5fb08-194">fréquence de collecte</span><span class="sxs-lookup"><span data-stu-id="5fb08-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="5fb08-195">Windows</span><span class="sxs-lookup"><span data-stu-id="5fb08-195">Windows</span></span> |  |  | <span data-ttu-id="5fb08-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5fb08-196">&#8226;</span></span> |  |  |<span data-ttu-id="5fb08-197">10 minutes</span><span class="sxs-lookup"><span data-stu-id="5fb08-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="5fb08-198">Vous pouvez modifier l’étendue de hello de ces événements Bonjour solution d’infrastructure de Service en cliquant sur **les données basées sur les 7 derniers jours** haut hello du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="5fb08-198">You can change hello scope of these events in hello Service Fabric solution by clicking **Data based on last 7 days** at hello top of hello dashboard.</span></span> <span data-ttu-id="5fb08-199">Vous pouvez également afficher les événements générés dans hello sept derniers jours, un jour ou six heures.</span><span class="sxs-lookup"><span data-stu-id="5fb08-199">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="5fb08-200">Vous pouvez également sélectionner **personnalisé** toospecify une plage de dates personnalisée.</span><span class="sxs-lookup"><span data-stu-id="5fb08-200">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="5fb08-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5fb08-201">Next steps</span></span>

* <span data-ttu-id="5fb08-202">Utilisez [recherches de journal dans le journal Analytique](log-analytics-log-searches.md) tooview détaillées des données d’événement Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5fb08-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
