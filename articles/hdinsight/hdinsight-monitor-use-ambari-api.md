---
title: "Surveiller les clusters Hadoop dans HDInsight à l’aide de l’API Ambari - Azure | Microsoft Docs"
description: "Utilisez les API Apache Ambari pour la création, la gestion et la surveillance des clusters Hadoop. Les outils intuitifs pour opérateurs et les API masquent la complexité de Hadoop."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
editor: cgronlun
manager: jhubbard
ms.assetid: 052135b3-d497-4acc-92ff-71cee49356ff
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: b6fc2098027690eb76b69b1427f0e9541b8a7a69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-the-ambari-api"></a><span data-ttu-id="def2c-104">Surveillance des clusters Hadoop dans HDInsight à l'aide des API Ambari</span><span class="sxs-lookup"><span data-stu-id="def2c-104">Monitor Hadoop clusters in HDInsight using the Ambari API</span></span>
<span data-ttu-id="def2c-105">Découvrez comment surveiller les clusters HDInsight à l’aide des API Ambari.</span><span class="sxs-lookup"><span data-stu-id="def2c-105">Learn how to monitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="def2c-106">Les informations contenues dans cet article sont adaptées principalement aux clusters HDInsight basés sur Windows, qui fournissent une version en lecture seule de l’API REST Ambari.</span><span class="sxs-lookup"><span data-stu-id="def2c-106">The information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of the Ambari REST API.</span></span> <span data-ttu-id="def2c-107">Pour les clusters basés sur Linux, consultez la page [Gestion des clusters HDInsight à l’aide d’Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="def2c-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="def2c-108">Présentation d'Ambari</span><span class="sxs-lookup"><span data-stu-id="def2c-108">What is Ambari?</span></span>
<span data-ttu-id="def2c-109">[Apache Ambari][ambari-home] est destiné à l’approvisionnement, à la gestion et à la surveillance des clusters Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="def2c-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="def2c-110">Il comprend une collection intuitive d'outils d'opérateurs et un solide jeu d'API qui masque la complexité de Hadoop, en simplifiant le fonctionnement des clusters.</span><span class="sxs-lookup"><span data-stu-id="def2c-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide the complexity of Hadoop, simplifying the operation of clusters.</span></span> <span data-ttu-id="def2c-111">Pour plus d’informations sur les API, consultez la page [Référence des API Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="def2c-111">For more information about the APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="def2c-112">HDInsight prend actuellement en charge la fonctionnalité de surveillance Ambari uniquement.</span><span class="sxs-lookup"><span data-stu-id="def2c-112">HDInsight currently supports only the Ambari monitoring feature.</span></span> <span data-ttu-id="def2c-113">La version 1.0 de l’API Ambari est prise en charge par les clusters HDInsight versions 2.1 et 3.0.</span><span class="sxs-lookup"><span data-stu-id="def2c-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="def2c-114">Cet article présente l’accès aux API Ambari sur les versions de clusters HDInsight 3.1 et 2.1.</span><span class="sxs-lookup"><span data-stu-id="def2c-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="def2c-115">La différence principale entre les deux est que certains des composants ont changé avec l'introduction des nouvelles fonctionnalités (telles que le serveur d'historique des tâches).</span><span class="sxs-lookup"><span data-stu-id="def2c-115">The key difference between the two is that some of the components have changed with the introduction of new capabilities (such as the Job History Server).</span></span> 

<span data-ttu-id="def2c-116">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="def2c-116">**Prerequisites**</span></span>

<span data-ttu-id="def2c-117">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="def2c-117">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="def2c-118">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="def2c-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="def2c-119">[cURL][curl] est facultatif.</span><span class="sxs-lookup"><span data-stu-id="def2c-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="def2c-120">Pour l’installer, consultez [Versions et téléchargements de cURL][curl-download].</span><span class="sxs-lookup"><span data-stu-id="def2c-120">To install it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="def2c-121">Lorsque vous utilisez la commande cURL sous Windows, remplacez les guillemets simples par des guillemets doubles pour exprimer la valeur des options.</span><span class="sxs-lookup"><span data-stu-id="def2c-121">When use the cURL command in Windows, use double-quotation marks instead of single-quotation marks for the option values.</span></span>
  > 
  > 
* <span data-ttu-id="def2c-122">Un **cluster Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="def2c-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="def2c-123">Pour obtenir des instructions sur l’approvisionnement des clusters, consultez la rubrique [Prise en main de HDInsight][hdinsight-get-started] ou [Approvisionnement de clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="def2c-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="def2c-124">Vous aurez besoin des données suivantes pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="def2c-124">You need the following data to go through the tutorial:</span></span>
  
  | <span data-ttu-id="def2c-125">Propriété du cluster</span><span class="sxs-lookup"><span data-stu-id="def2c-125">Cluster property</span></span> | <span data-ttu-id="def2c-126">Nom de la variable Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="def2c-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="def2c-127">Valeur</span><span class="sxs-lookup"><span data-stu-id="def2c-127">Value</span></span> | <span data-ttu-id="def2c-128">Description</span><span class="sxs-lookup"><span data-stu-id="def2c-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="def2c-129">Nom du cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="def2c-129">HDInsight cluster name</span></span> |<span data-ttu-id="def2c-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="def2c-130">$clusterName</span></span> | |<span data-ttu-id="def2c-131">Nom de votre cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="def2c-131">The name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="def2c-132">Nom d'utilisateur du cluster</span><span class="sxs-lookup"><span data-stu-id="def2c-132">Cluster username</span></span> |<span data-ttu-id="def2c-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="def2c-133">$clusterUsername</span></span> | |<span data-ttu-id="def2c-134">Nom d’utilisateur du cluster spécifié lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="def2c-134">Cluster user name specified when the cluster was created.</span></span> |
  |   <span data-ttu-id="def2c-135">Mot de passe du cluster</span><span class="sxs-lookup"><span data-stu-id="def2c-135">Cluster password</span></span> |<span data-ttu-id="def2c-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="def2c-136">$clusterPassword</span></span> | |<span data-ttu-id="def2c-137">Mot de passe utilisateur du cluster</span><span class="sxs-lookup"><span data-stu-id="def2c-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="def2c-138">Lancer rapidement</span><span class="sxs-lookup"><span data-stu-id="def2c-138">Jump-start</span></span>
<span data-ttu-id="def2c-139">Il existe plusieurs façons d'utiliser Ambari pour surveiller les clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="def2c-139">There are several ways to use Ambari to monitor HDInsight clusters.</span></span>

<span data-ttu-id="def2c-140">**Utilisation d'Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="def2c-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="def2c-141">Le script Azure PowerShell suivant permet d’obtenir les informations de suivi des tâches MapReduce *dans un cluster HDInsight 3.5.*</span><span class="sxs-lookup"><span data-stu-id="def2c-141">The following Azure PowerShell script gets the MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="def2c-142">La différence principale réside dans le fait que nous allons extraire ces détails à partir du service YARN (plutôt que Map Reduce).</span><span class="sxs-lookup"><span data-stu-id="def2c-142">The key difference is that we pull these details from the YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="def2c-143">Le script PowerShell suivant permet d’obtenir les informations de suivi des tâches MapReduce *dans un cluster HDInsight 2.1* :</span><span class="sxs-lookup"><span data-stu-id="def2c-143">The following PowerShell script gets the MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="def2c-144">La sortie est la suivante :</span><span class="sxs-lookup"><span data-stu-id="def2c-144">The output is:</span></span>

![Sortie du jobtracker][img-jobtracker-output]

<span data-ttu-id="def2c-146">**Utilisation de curl**</span><span class="sxs-lookup"><span data-stu-id="def2c-146">**Use cURL**</span></span>

<span data-ttu-id="def2c-147">L’exemple suivant permet d’obtenir des informations de cluster à l’aide de cURL :</span><span class="sxs-lookup"><span data-stu-id="def2c-147">The following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="def2c-148">La sortie est la suivante :</span><span class="sxs-lookup"><span data-stu-id="def2c-148">The output is:</span></span>

    {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/",
     "Clusters":{"cluster_name":"hdi0211v2.azurehdinsight.net","version":"2.1.3.0.432823"},
     "services"[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/hdfs",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"hdfs"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/mapreduce",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"mapreduce"}}],
     "hosts":[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/headnode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/workernode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0.{ClusterDNS}.azurehdinsight.net"}}]}

<span data-ttu-id="def2c-149">**Pour la version du 8/10/2014**:</span><span class="sxs-lookup"><span data-stu-id="def2c-149">**For the 10/8/2014 release**:</span></span>

<span data-ttu-id="def2c-150">Lors de l’utilisation du point de terminaison Ambari, « https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname} », le champ *host_name* renvoie le nom de domaine complet du nœud au lieu du nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="def2c-150">When using the Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", the *host_name* field returns the fully qualified domain name (FQDN) of the node instead of the host name.</span></span> <span data-ttu-id="def2c-151">Avant la version du 8/10/2014, cet exemple renvoyait simplement «**headnode0**».</span><span class="sxs-lookup"><span data-stu-id="def2c-151">Before the 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="def2c-152">Après la version du 8/10/2014, vous obtenez le nom de domaine complet «**headnode0.{ClusterDNS}.azurehdinsight.net**», comme illustré dans l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="def2c-152">After the 10/8/2014 release, you get the FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in the previous example.</span></span> <span data-ttu-id="def2c-153">Cette modification était nécessaire pour permettre les scénarios dans lesquels plusieurs types de cluster tels que HBase et Hadoop sont déployés dans un réseau virtuel (VNET).</span><span class="sxs-lookup"><span data-stu-id="def2c-153">This change was required to facilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="def2c-154">Cela se produit, par exemple, lors de l'utilisation de HBase en tant que plateforme principale pour Hadoop.</span><span class="sxs-lookup"><span data-stu-id="def2c-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="def2c-155">API de surveillance Ambari</span><span class="sxs-lookup"><span data-stu-id="def2c-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="def2c-156">Le tableau suivant répertorie certains des appels d'API de surveillance Ambari les plus connus.</span><span class="sxs-lookup"><span data-stu-id="def2c-156">The following table lists some of the most common Ambari monitoring API calls.</span></span> <span data-ttu-id="def2c-157">Pour plus d’informations sur l’API, consultez la page [Référence des API Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="def2c-157">For more information about the API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="def2c-158">Appel d'API de surveillance</span><span class="sxs-lookup"><span data-stu-id="def2c-158">Monitor API call</span></span> | <span data-ttu-id="def2c-159">URI</span><span class="sxs-lookup"><span data-stu-id="def2c-159">URI</span></span> | <span data-ttu-id="def2c-160">Description</span><span class="sxs-lookup"><span data-stu-id="def2c-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="def2c-161">Obtenir des clusters</span><span class="sxs-lookup"><span data-stu-id="def2c-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="def2c-162">Obtenir des infos sur les clusters</span><span class="sxs-lookup"><span data-stu-id="def2c-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="def2c-163">clusters, services, hôtes</span><span class="sxs-lookup"><span data-stu-id="def2c-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="def2c-164">Obtenir des services</span><span class="sxs-lookup"><span data-stu-id="def2c-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="def2c-165">Les services incluent : hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="def2c-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="def2c-166">Obtenir des infos sur les services</span><span class="sxs-lookup"><span data-stu-id="def2c-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="def2c-167">Obtenir des composants de service</span><span class="sxs-lookup"><span data-stu-id="def2c-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="def2c-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="def2c-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="def2c-169">Obtenir des infos sur les composants</span><span class="sxs-lookup"><span data-stu-id="def2c-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="def2c-170">ServiceComponentInfo, host-components, mesures</span><span class="sxs-lookup"><span data-stu-id="def2c-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="def2c-171">Obtenir des hôtes</span><span class="sxs-lookup"><span data-stu-id="def2c-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="def2c-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="def2c-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="def2c-173">Obtenir des infos sur les hôtes</span><span class="sxs-lookup"><span data-stu-id="def2c-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="def2c-174">Obtenir des composants d'hôte</span><span class="sxs-lookup"><span data-stu-id="def2c-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="def2c-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="def2c-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="def2c-176">Obtenir des informations sur les composants d'hôte</span><span class="sxs-lookup"><span data-stu-id="def2c-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="def2c-177">HostRoles, composant, hôte, mesure</span><span class="sxs-lookup"><span data-stu-id="def2c-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="def2c-178">Obtenir des configurations</span><span class="sxs-lookup"><span data-stu-id="def2c-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="def2c-179">Types de configurations : core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="def2c-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="def2c-180">Obtenir des infos sur la configuration</span><span class="sxs-lookup"><span data-stu-id="def2c-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="def2c-181">Types de configurations : core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="def2c-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="def2c-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="def2c-182">Next Steps</span></span>
<span data-ttu-id="def2c-183">Vous avez appris à utiliser les appels d'API de surveillance Ambari.</span><span class="sxs-lookup"><span data-stu-id="def2c-183">Now you have learned how to use Ambari monitoring API calls.</span></span> <span data-ttu-id="def2c-184">Pour plus d'informations, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="def2c-184">To learn more, see:</span></span>

* <span data-ttu-id="def2c-185">[Gestion des clusters HDInsight à l’aide du portail Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="def2c-185">[Manage HDInsight clusters using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="def2c-186">[Gestion des clusters HDInsight à l’aide d’Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="def2c-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="def2c-187">[Gestion de clusters HDInsight à l’aide de l’interface de ligne de commande][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="def2c-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="def2c-188">[Documentation HDInsight][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="def2c-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="def2c-189">[Prise en main de HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="def2c-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

[ambari-home]: http://ambari.apache.org/
[ambari-api-reference]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[microsoft-hadoop-SDK]: http://hadoopsdk.codeplex.com/wikipage?title=Ambari%20Monitoring%20Client

[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-documentation]: https://docs.microsoft.com/azure/hdinsight/
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[img-jobtracker-output]: ./media/hdinsight-monitor-use-ambari-api/hdi.ambari.monitor.jobtracker.output.png
