---
title: "Évaluer des applications Service Fabric avec Log Analytics à l’aide du portail Azure | Microsoft Docs"
description: "Vous pouvez utiliser la solution Service Fabric dans Log Analytics, à l’aide du portail Azure, pour évaluer les risques et l’intégrité de vos applications, micro-services, nœuds et clusters Service Fabric."
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
ms.openlocfilehash: 8c564c0dcbb2f9be286917b2f4d8a40da5406fae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-the-azure-portal"></a><span data-ttu-id="3661c-103">Évaluer les micro-services et applications Service Fabric avec le portail Azure | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="3661c-103">Assess Service Fabric applications and micro-services with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3661c-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="3661c-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="3661c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3661c-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Symbole Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="3661c-107">Cet article décrit comment utiliser la solution Service Fabric dans Log Analytics pour identifier et résoudre les problèmes sur l’ensemble de votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3661c-107">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="3661c-108">La solution Service Fabric utilise les données de diagnostic Azure provenant de vos machines virtuelles Fabric Service. Ces données sont collectées à partir de vos tables Azure WAD.</span><span class="sxs-lookup"><span data-stu-id="3661c-108">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="3661c-109">Log Analytics lit ensuite les événements d’infrastructure Service Fabric, notamment les **événements de service fiable**, les **événements d’acteurs**, les **événements opérationnels** et les **événements ETW personnalisés**.</span><span class="sxs-lookup"><span data-stu-id="3661c-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="3661c-110">Le tableau de bord de la solution vous montre les problèmes notables et les événements pertinents qui s’appliquent à votre environnement Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3661c-110">With the solution dashboard, you are able to view notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="3661c-111">Pour commencer à utiliser la solution, connectez votre cluster Service Fabric à un espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3661c-111">To get started with the solution, you need to connect your Service Fabric cluster to a Log Analytics workspace.</span></span> <span data-ttu-id="3661c-112">Trois scénarios sont à envisager :</span><span class="sxs-lookup"><span data-stu-id="3661c-112">Here are three scenarios to consider:</span></span>

1. <span data-ttu-id="3661c-113">Si vous n’avez pas déployé votre cluster Service Fabric, effectuez les étapes de la section ***Déployer un cluster Service Fabric connecté à un espace de travail Log Analytics*** pour déployer un nouveau cluster et le configurer pour qu’il rende compte à Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3661c-113">If you have not deployed your Service Fabric cluster, use the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace*** to deploy a new cluster and have it configured to report to Log Analytics.</span></span>
2. <span data-ttu-id="3661c-114">Si vous avez besoin de collecter les compteurs de performances de vos hôtes pour utiliser d’autres solutions OMS, telles que Sécurité, sur votre cluster Service Fabric, effectuez les étapes de la section ***Déployer un cluster Service Fabric connecté à un espace de travail Log Analytics avec l’extension de machine virtuelle installée***.</span><span class="sxs-lookup"><span data-stu-id="3661c-114">If you need to collect performance counters from your hosts to use other OMS solutions such as Security on your Service Fabric Cluster, follow the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="3661c-115">Si vous avez déjà déployé votre cluster Service Fabric et que vous souhaitez le connecter à Log Analytics, effectuez les étapes de la section ***Ajout d’un compte de stockage existant à Log Analytics***.</span><span class="sxs-lookup"><span data-stu-id="3661c-115">If you have already deployed your Service Fabric cluster and want to connect it to Log Analytics, follow the steps in ***Adding an existing storage account to Log Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace"></a><span data-ttu-id="3661c-116">Déployer un cluster Service Fabric connecté à un espace de travail Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3661c-116">Deploy a Service Fabric Cluster connected to a Log Analytics workspace.</span></span>
<span data-ttu-id="3661c-117">Ce modèle effectue les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="3661c-117">This template does the following:</span></span>

1. <span data-ttu-id="3661c-118">Déploie un cluster Azure Service Fabric déjà connecté à un espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3661c-118">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="3661c-119">Vous pouvez soit créer un espace de travail durant le déploiement du modèle, soit entrer le nom d’un espace de travail Log Analytics existant.</span><span class="sxs-lookup"><span data-stu-id="3661c-119">You have the option to create a new workspace while deploying the template, or input the name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="3661c-120">Ajoute le compte de stockage de diagnostic à l’espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3661c-120">Adds the diagnostic storage account to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="3661c-121">Active la solution Service Fabric dans votre espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3661c-121">Enables the Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="3661c-122">[![Déploiement sur Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="3661c-122">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="3661c-123">Quand vous appuyez sur le bouton Déployer ci-dessus, le portail Azure s’affiche et vous pouvez y modifier des paramètres.</span><span class="sxs-lookup"><span data-stu-id="3661c-123">Once you select the deploy button above, the Azure portal opens with parameters for you to edit.</span></span> <span data-ttu-id="3661c-124">Veillez à créer un groupe de ressources si vous entrez un nouveau nom d’espace de travail Log Analytics :</span><span class="sxs-lookup"><span data-stu-id="3661c-124">Be sure to create a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="3661c-127">Acceptez les conditions légales et cliquez sur **Créer** pour lancer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="3661c-127">Accept the legal terms and click **Create** to start the deployment.</span></span> <span data-ttu-id="3661c-128">Une fois le déploiement terminé, le nouvel espace de travail et le nouveau cluster doivent s’afficher, tandis que les tables WADServiceFabric*Event, WADWindowsEventLogs et WADETWEvent doivent être ajoutées :</span><span class="sxs-lookup"><span data-stu-id="3661c-128">Once the deployment is completed, you should see the new workspace and cluster created, and the WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="3661c-130">Déployez un cluster Service Fabric connecté à un espace de travail Log Analytics avec l’extension de machine virtuelle installée.</span><span class="sxs-lookup"><span data-stu-id="3661c-130">Deploy a Service Fabric Cluster connected to a Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="3661c-131">Ce modèle effectue les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="3661c-131">This template does the following:</span></span>

1. <span data-ttu-id="3661c-132">Déploie un cluster Azure Service Fabric déjà connecté à un espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3661c-132">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="3661c-133">Vous pouvez créer un espace de travail ou utiliser un espace de travail existant.</span><span class="sxs-lookup"><span data-stu-id="3661c-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="3661c-134">Ajoute les comptes de stockage de diagnostic à l’espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3661c-134">Adds the diagnostic storage accounts to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="3661c-135">Active la solution Service Fabric dans l’espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3661c-135">Enables the Service Fabric solution in the Log Analytics workspace.</span></span>
4. <span data-ttu-id="3661c-136">Installe l’extension de l’agent MMA dans chaque groupe de machines virtuelles identiques de votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3661c-136">Installs the MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="3661c-137">Une fois l’agent MMA installé, vous pouvez afficher les mesures de performances de vos nœuds.</span><span class="sxs-lookup"><span data-stu-id="3661c-137">With the MMA agent installed, you are able to view performance metrics about your nodes.</span></span>

<span data-ttu-id="3661c-138">[![Déployer sur Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="3661c-138">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="3661c-139">En suivant la même procédure que celle mentionnée ci-dessus, indiquez les paramètres nécessaires et lancez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="3661c-139">Following the same steps above, input the necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="3661c-140">Là encore, l’espace de travail, le cluster et les tables WAD que vous venez de créer doivent s’afficher :</span><span class="sxs-lookup"><span data-stu-id="3661c-140">Once again you should see the new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="3661c-142">Affichage des données de performances</span><span class="sxs-lookup"><span data-stu-id="3661c-142">Viewing Performance Data</span></span>

<span data-ttu-id="3661c-143">Pour afficher les données de performances de vos nœuds :</span><span class="sxs-lookup"><span data-stu-id="3661c-143">To view Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="3661c-144">Lancez l’espace de travail Log Analytics à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3661c-144">Launch the Log Analytics workspace from the Azure portal.</span></span>
  <span data-ttu-id="3661c-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="3661c-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="3661c-146">Accédez à Paramètres dans le volet gauche, puis sélectionnez Données >> Compteurs de performances Windows >> Ajouter les compteurs de performances sélectionnés : ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="3661c-146">Go to Settings on the left pane, and select Data >> Windows Performance Counters >> "Add the selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="3661c-147">Dans Recherche dans les journaux, utilisez les requêtes suivantes pour étudier les mesures clés sur vos nœuds :</span><span class="sxs-lookup"><span data-stu-id="3661c-147">In Log Search, use the following queries to delve into key metrics about your nodes:</span></span>

    <span data-ttu-id="3661c-148">a.</span><span class="sxs-lookup"><span data-stu-id="3661c-148">a.</span></span> <span data-ttu-id="3661c-149">Comparez l’utilisation moyenne du processeur sur tous les nœuds au cours de l’heure écoulée pour identifier les nœuds qui ont des problèmes et l’intervalle de temps dans lequel un nœud a connu une pointe d’activité :</span><span class="sxs-lookup"><span data-stu-id="3661c-149">Compare the average CPU Utilization across all your nodes in the last one hour to see which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="3661c-151">b.</span><span class="sxs-lookup"><span data-stu-id="3661c-151">b.</span></span> <span data-ttu-id="3661c-152">Examinez des graphiques en courbes similaires pour la mémoire disponible sur chaque nœud avec cette requête :</span><span class="sxs-lookup"><span data-stu-id="3661c-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="3661c-153">Pour répertorier tous les nœuds avec la valeur moyenne exacte de mégaoctets disponibles pour chaque nœud, utilisez cette requête :</span><span class="sxs-lookup"><span data-stu-id="3661c-153">To view a listing of all your nodes, showing the exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="3661c-155">c.</span><span class="sxs-lookup"><span data-stu-id="3661c-155">c.</span></span> <span data-ttu-id="3661c-156">Pour explorer au niveau du détail un nœud spécifique, notamment l’utilisation moyenne, minimale, maximale et au 75e centile du processeur par heure, utilisez cette requête (en remplaçant le champ Computer) :</span><span class="sxs-lookup"><span data-stu-id="3661c-156">In the case that you want to drill down into a specific node by examining the hourly average, minimum, maximum and 75-percentile CPU usage, you're able to do this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="3661c-158">Obtenez plus d’informations sur les métriques de performance dans Log Analytics dans le [blog Operations Management Suite](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span><span class="sxs-lookup"><span data-stu-id="3661c-158">Read more information about performance metrics in Log Analytics at the [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-to-log-analytics"></a><span data-ttu-id="3661c-159">Ajout d’un compte de stockage existant à Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3661c-159">Adding an existing storage account to Log Analytics</span></span>

<span data-ttu-id="3661c-160">Ce modèle ajoute simplement vos comptes de stockage existant à un espace de travail Log Analytics, nouveau ou existant.</span><span class="sxs-lookup"><span data-stu-id="3661c-160">This template simply adds your existing storage accounts to a new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="3661c-161">[![Déploiement sur Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="3661c-161">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="3661c-162">Si vous disposez déjà d’un espace de travail Log Analytics au moment de la sélection d’un groupe, sélectionnez Utiliser l’existant et recherchez le groupe de ressources contenant l’espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3661c-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for the resource group containing the Log Analytics workspace.</span></span> <span data-ttu-id="3661c-163">Dans le cas contraire, créez-en un.</span><span class="sxs-lookup"><span data-stu-id="3661c-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="3661c-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="3661c-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="3661c-165">Une fois ce modèle déployé, vous pouvez voir le compte de stockage connecté à votre espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3661c-165">After this template has been deployed, you will be able to see the storage account connected to your Log Analytics workspace.</span></span> <span data-ttu-id="3661c-166">Ici, j’ai ajouté un compte de stockage à l’espace de travail Exchange créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="3661c-166">In this instance, I added one more storage account to the Exchange workspace I created above.</span></span>
<span data-ttu-id="3661c-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="3661c-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="3661c-168">Afficher les événements Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3661c-168">View Service Fabric events</span></span>

<span data-ttu-id="3661c-169">Une fois les déploiements terminés et la solution Service Fabric activée dans votre espace de travail, sélectionnez la vignette **Service Fabric** dans le portail Log Analytics pour lancer le tableau de bord Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3661c-169">Once the deployments are completed and the Service Fabric solution has been enabled in your workspace, select the **Service Fabric** tile in the Log Analytics portal to launch the Service Fabric dashboard.</span></span> <span data-ttu-id="3661c-170">Le tableau de bord comprend les colonnes figurant dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="3661c-170">The dashboard includes the columns in the following table.</span></span> <span data-ttu-id="3661c-171">Chaque colonne répertorie les 10 premiers événements, classés selon leur nombre, correspondant aux critères de cette colonne pour l’intervalle de temps spécifié.</span><span class="sxs-lookup"><span data-stu-id="3661c-171">Each column lists the top 10 events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="3661c-172">Vous pouvez exécuter une recherche dans les journaux qui fournit la liste complète. Pour cela, cliquez sur **Afficher tout** en bas à droite de chaque colonne ou cliquez sur l’en-tête de colonne.</span><span class="sxs-lookup"><span data-stu-id="3661c-172">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="3661c-173">**Événement Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="3661c-173">**Service Fabric event**</span></span> | <span data-ttu-id="3661c-174">**description**</span><span class="sxs-lookup"><span data-stu-id="3661c-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="3661c-175">Problèmes notables</span><span class="sxs-lookup"><span data-stu-id="3661c-175">Notable Issues</span></span> |<span data-ttu-id="3661c-176">Affichage des problèmes tels que RunAsyncFailures RunAsynCancellations et des pannes de nœud.</span><span class="sxs-lookup"><span data-stu-id="3661c-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="3661c-177">Événements opérationnels</span><span class="sxs-lookup"><span data-stu-id="3661c-177">Operational Events</span></span> |<span data-ttu-id="3661c-178">Événements opérationnels notables, tels que les déploiements et mises à niveau d’application.</span><span class="sxs-lookup"><span data-stu-id="3661c-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="3661c-179">Événements de service fiable</span><span class="sxs-lookup"><span data-stu-id="3661c-179">Reliable Service Events</span></span> |<span data-ttu-id="3661c-180">Événements de service fiable notables, comme Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="3661c-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="3661c-181">Événements des acteurs</span><span class="sxs-lookup"><span data-stu-id="3661c-181">Actor Events</span></span> |<span data-ttu-id="3661c-182">Événements d’acteur notables générés par vos microservices, notamment les exceptions levées par une méthode d’acteur, les activations et désactivations d’acteur, etc.</span><span class="sxs-lookup"><span data-stu-id="3661c-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="3661c-183">Événements d’application</span><span class="sxs-lookup"><span data-stu-id="3661c-183">Application Events</span></span> |<span data-ttu-id="3661c-184">Tous les événements ETW personnalisés générés par vos applications.</span><span class="sxs-lookup"><span data-stu-id="3661c-184">All custom ETW events generated by your applications.</span></span> |

![Tableau de bord Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Tableau de bord Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="3661c-187">Le tableau suivant présente les méthodes de collecte des données et d’autres informations sur le mode de collecte de la solution de données pour Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3661c-187">The following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="3661c-188">plateforme</span><span class="sxs-lookup"><span data-stu-id="3661c-188">platform</span></span> | <span data-ttu-id="3661c-189">Agent direct</span><span class="sxs-lookup"><span data-stu-id="3661c-189">Direct Agent</span></span> | <span data-ttu-id="3661c-190">Agent Operations Manager</span><span class="sxs-lookup"><span data-stu-id="3661c-190">Operations Manager agent</span></span> | <span data-ttu-id="3661c-191">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3661c-191">Azure Storage</span></span> | <span data-ttu-id="3661c-192">Operations Manager requis ?</span><span class="sxs-lookup"><span data-stu-id="3661c-192">Operations Manager required?</span></span> | <span data-ttu-id="3661c-193">Données de l’agent Operations Manager envoyées via un groupe d’administration</span><span class="sxs-lookup"><span data-stu-id="3661c-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="3661c-194">fréquence de collecte</span><span class="sxs-lookup"><span data-stu-id="3661c-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="3661c-195">Windows</span><span class="sxs-lookup"><span data-stu-id="3661c-195">Windows</span></span> |  |  | <span data-ttu-id="3661c-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="3661c-196">&#8226;</span></span> |  |  |<span data-ttu-id="3661c-197">10 minutes</span><span class="sxs-lookup"><span data-stu-id="3661c-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="3661c-198">Vous pouvez modifier l’étendue de ces événements dans la solution Service Fabric en cliquant sur **Données basées sur les 7 derniers jours** dans la partie supérieure du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="3661c-198">You can change the scope of these events in the Service Fabric solution by clicking **Data based on last 7 days** at the top of the dashboard.</span></span> <span data-ttu-id="3661c-199">Vous pouvez également afficher les événements générés durant les sept derniers jours, la journée précédente ou les six dernières heures.</span><span class="sxs-lookup"><span data-stu-id="3661c-199">You can also show events generated within the last seven days, one day, or six hours.</span></span> <span data-ttu-id="3661c-200">Vous pouvez aussi sélectionner **Personnalisé** pour spécifier une plage de dates personnalisée.</span><span class="sxs-lookup"><span data-stu-id="3661c-200">Or, you can select **Custom** to specify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3661c-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3661c-201">Next steps</span></span>

* <span data-ttu-id="3661c-202">Utilisez [Recherches dans les journaux dans Log Analytics](log-analytics-log-searches.md) pour afficher des données détaillées sur les événements Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3661c-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>
