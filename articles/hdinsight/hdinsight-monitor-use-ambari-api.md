---
title: "aaaMonitor les clusters Hadoop dans HDInsight à l’aide de hello Ambari API - Azure | Documents Microsoft"
description: "Pour créer, gérer et surveiller les clusters Hadoop, utilisez hello Apache Ambari APIs. Opérateur intuitif outils et API masquer la complexité de hello de Hadoop."
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
ms.openlocfilehash: d61a8aae5ddfcd7d44f2e4cc899e0a4da5e5fdcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a><span data-ttu-id="3bed5-104">Analyser les clusters Hadoop dans HDInsight à l’aide de hello Ambari API</span><span class="sxs-lookup"><span data-stu-id="3bed5-104">Monitor Hadoop clusters in HDInsight using hello Ambari API</span></span>
<span data-ttu-id="3bed5-105">Découvrez comment les clusters à l’aide de Ambari APIs toomonitor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3bed5-105">Learn how toomonitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="3bed5-106">informations Hello dans cet article sont principalement pour les clusters HDInsight de basés sur Windows, qui fournissent une version en lecture seule de hello Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="3bed5-106">hello information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of hello Ambari REST API.</span></span> <span data-ttu-id="3bed5-107">Pour les clusters basés sur Linux, consultez la page [Gestion des clusters HDInsight à l’aide d’Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="3bed5-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="3bed5-108">Présentation d'Ambari</span><span class="sxs-lookup"><span data-stu-id="3bed5-108">What is Ambari?</span></span>
<span data-ttu-id="3bed5-109">[Apache Ambari][ambari-home] est destiné à l’approvisionnement, à la gestion et à la surveillance des clusters Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3bed5-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="3bed5-110">Elle inclut une collection d’outils de l’opérateur d’intuitive et un ensemble complet d’API qui masquent la complexité hello de Hadoop, ce qui simplifie le fonctionnement de hello de clusters.</span><span class="sxs-lookup"><span data-stu-id="3bed5-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide hello complexity of Hadoop, simplifying hello operation of clusters.</span></span> <span data-ttu-id="3bed5-111">Pour plus d’informations sur les API de hello, consultez [référence de l’API Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="3bed5-111">For more information about hello APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="3bed5-112">HDInsight prend actuellement en charge uniquement hello Ambari fonctionnalité d’analyse.</span><span class="sxs-lookup"><span data-stu-id="3bed5-112">HDInsight currently supports only hello Ambari monitoring feature.</span></span> <span data-ttu-id="3bed5-113">La version 1.0 de l’API Ambari est prise en charge par les clusters HDInsight versions 2.1 et 3.0.</span><span class="sxs-lookup"><span data-stu-id="3bed5-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="3bed5-114">Cet article présente l’accès aux API Ambari sur les versions de clusters HDInsight 3.1 et 2.1.</span><span class="sxs-lookup"><span data-stu-id="3bed5-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="3bed5-115">Hello principale différence entre hello deux est que certains composants de hello ont changé avec l’introduction de hello de nouvelles fonctionnalités (telles que le serveur de l’historique des travaux de hello).</span><span class="sxs-lookup"><span data-stu-id="3bed5-115">hello key difference between hello two is that some of hello components have changed with hello introduction of new capabilities (such as hello Job History Server).</span></span> 

<span data-ttu-id="3bed5-116">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="3bed5-116">**Prerequisites**</span></span>

<span data-ttu-id="3bed5-117">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="3bed5-117">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="3bed5-118">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="3bed5-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="3bed5-119">[cURL][curl] est facultatif.</span><span class="sxs-lookup"><span data-stu-id="3bed5-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="3bed5-120">tooinstall, consultez [cURL téléchargements et mises en production][curl-download].</span><span class="sxs-lookup"><span data-stu-id="3bed5-120">tooinstall it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3bed5-121">Quand utiliser hello cURL commande dans Windows, utilisez des guillemets doubles au lieu des guillemets simples pour les valeurs d’option hello.</span><span class="sxs-lookup"><span data-stu-id="3bed5-121">When use hello cURL command in Windows, use double-quotation marks instead of single-quotation marks for hello option values.</span></span>
  > 
  > 
* <span data-ttu-id="3bed5-122">Un **cluster Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3bed5-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="3bed5-123">Pour obtenir des instructions sur l’approvisionnement des clusters, consultez la rubrique [Prise en main de HDInsight][hdinsight-get-started] ou [Approvisionnement de clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="3bed5-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="3bed5-124">Vous devez hello suivant toogo données didacticiel de hello :</span><span class="sxs-lookup"><span data-stu-id="3bed5-124">You need hello following data toogo through hello tutorial:</span></span>
  
  | <span data-ttu-id="3bed5-125">Propriété du cluster</span><span class="sxs-lookup"><span data-stu-id="3bed5-125">Cluster property</span></span> | <span data-ttu-id="3bed5-126">Nom de la variable Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3bed5-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="3bed5-127">Valeur</span><span class="sxs-lookup"><span data-stu-id="3bed5-127">Value</span></span> | <span data-ttu-id="3bed5-128">Description</span><span class="sxs-lookup"><span data-stu-id="3bed5-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="3bed5-129">Nom du cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="3bed5-129">HDInsight cluster name</span></span> |<span data-ttu-id="3bed5-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="3bed5-130">$clusterName</span></span> | |<span data-ttu-id="3bed5-131">nom de Hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3bed5-131">hello name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="3bed5-132">Nom d'utilisateur du cluster</span><span class="sxs-lookup"><span data-stu-id="3bed5-132">Cluster username</span></span> |<span data-ttu-id="3bed5-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="3bed5-133">$clusterUsername</span></span> | |<span data-ttu-id="3bed5-134">Nom d’utilisateur de cluster spécifiée lors de la création de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="3bed5-134">Cluster user name specified when hello cluster was created.</span></span> |
  |   <span data-ttu-id="3bed5-135">Mot de passe du cluster</span><span class="sxs-lookup"><span data-stu-id="3bed5-135">Cluster password</span></span> |<span data-ttu-id="3bed5-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="3bed5-136">$clusterPassword</span></span> | |<span data-ttu-id="3bed5-137">Mot de passe utilisateur du cluster</span><span class="sxs-lookup"><span data-stu-id="3bed5-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="3bed5-138">Lancer rapidement</span><span class="sxs-lookup"><span data-stu-id="3bed5-138">Jump-start</span></span>
<span data-ttu-id="3bed5-139">Il existe plusieurs façons de clusters de HDInsight toomonitor toouse Ambari.</span><span class="sxs-lookup"><span data-stu-id="3bed5-139">There are several ways toouse Ambari toomonitor HDInsight clusters.</span></span>

<span data-ttu-id="3bed5-140">**Utilisation d'Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="3bed5-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="3bed5-141">Bonjour Azure PowerShell script suivant obtient des informations de suivi de travail de MapReduce hello *dans un cluster HDInsight 3.5.*</span><span class="sxs-lookup"><span data-stu-id="3bed5-141">hello following Azure PowerShell script gets hello MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="3bed5-142">Hello principale différence est que nous extraire ces informations à partir de service des fils hello (plutôt que MapReduce).</span><span class="sxs-lookup"><span data-stu-id="3bed5-142">hello key difference is that we pull these details from hello YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="3bed5-143">Hello PowerShell script suivant obtient des informations de suivi de travail de MapReduce hello *dans un cluster HDInsight 2.1*:</span><span class="sxs-lookup"><span data-stu-id="3bed5-143">hello following PowerShell script gets hello MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="3bed5-144">sortie de Hello est :</span><span class="sxs-lookup"><span data-stu-id="3bed5-144">hello output is:</span></span>

![Sortie du jobtracker][img-jobtracker-output]

<span data-ttu-id="3bed5-146">**Utilisation de curl**</span><span class="sxs-lookup"><span data-stu-id="3bed5-146">**Use cURL**</span></span>

<span data-ttu-id="3bed5-147">Hello exemple suivant obtient les informations de cluster à l’aide de cURL :</span><span class="sxs-lookup"><span data-stu-id="3bed5-147">hello following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="3bed5-148">sortie de Hello est :</span><span class="sxs-lookup"><span data-stu-id="3bed5-148">hello output is:</span></span>

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

<span data-ttu-id="3bed5-149">**Pour cette version 8/10/2014 hello**:</span><span class="sxs-lookup"><span data-stu-id="3bed5-149">**For hello 10/8/2014 release**:</span></span>

<span data-ttu-id="3bed5-150">Lorsque l’utilisation hello Ambari point de terminaison, « https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname} », hello *host_name* champ Retourne le nom de domaine complet (FQDN) hello du nœud hello au lieu du nom d’hôte hello.</span><span class="sxs-lookup"><span data-stu-id="3bed5-150">When using hello Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* field returns hello fully qualified domain name (FQDN) of hello node instead of hello host name.</span></span> <span data-ttu-id="3bed5-151">Avant la version de 8/10/2014 hello, cet exemple retourné simplement «**headnode0**».</span><span class="sxs-lookup"><span data-stu-id="3bed5-151">Before hello 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="3bed5-152">Après la mise en production de hello 8/10/2014, vous obtenez hello nom de domaine complet «**headnode0. {} ClusterDNS} .azurehdinsight .net**«, comme illustré dans l’exemple précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="3bed5-152">After hello 10/8/2014 release, you get hello FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in hello previous example.</span></span> <span data-ttu-id="3bed5-153">Cette modification a été requis toofacilitate les scénarios où plusieurs types de cluster (par exemple, HBase et Hadoop) peuvent être déployées dans un réseau virtuel (VNET).</span><span class="sxs-lookup"><span data-stu-id="3bed5-153">This change was required toofacilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="3bed5-154">Cela se produit, par exemple, lors de l'utilisation de HBase en tant que plateforme principale pour Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3bed5-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="3bed5-155">API de surveillance Ambari</span><span class="sxs-lookup"><span data-stu-id="3bed5-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="3bed5-156">Hello tableau suivant répertorie certaines hello courants Ambari analyses d’appels d’API.</span><span class="sxs-lookup"><span data-stu-id="3bed5-156">hello following table lists some of hello most common Ambari monitoring API calls.</span></span> <span data-ttu-id="3bed5-157">Pour plus d’informations sur les API de hello, consultez [référence de l’API Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="3bed5-157">For more information about hello API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="3bed5-158">Appel d'API de surveillance</span><span class="sxs-lookup"><span data-stu-id="3bed5-158">Monitor API call</span></span> | <span data-ttu-id="3bed5-159">URI</span><span class="sxs-lookup"><span data-stu-id="3bed5-159">URI</span></span> | <span data-ttu-id="3bed5-160">Description</span><span class="sxs-lookup"><span data-stu-id="3bed5-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3bed5-161">Obtenir des clusters</span><span class="sxs-lookup"><span data-stu-id="3bed5-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="3bed5-162">Obtenir des infos sur les clusters</span><span class="sxs-lookup"><span data-stu-id="3bed5-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="3bed5-163">clusters, services, hôtes</span><span class="sxs-lookup"><span data-stu-id="3bed5-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="3bed5-164">Obtenir des services</span><span class="sxs-lookup"><span data-stu-id="3bed5-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="3bed5-165">Les services incluent : hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="3bed5-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="3bed5-166">Obtenir des infos sur les services</span><span class="sxs-lookup"><span data-stu-id="3bed5-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="3bed5-167">Obtenir des composants de service</span><span class="sxs-lookup"><span data-stu-id="3bed5-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="3bed5-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="3bed5-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="3bed5-169">Obtenir des infos sur les composants</span><span class="sxs-lookup"><span data-stu-id="3bed5-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="3bed5-170">ServiceComponentInfo, host-components, mesures</span><span class="sxs-lookup"><span data-stu-id="3bed5-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="3bed5-171">Obtenir des hôtes</span><span class="sxs-lookup"><span data-stu-id="3bed5-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="3bed5-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="3bed5-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="3bed5-173">Obtenir des infos sur les hôtes</span><span class="sxs-lookup"><span data-stu-id="3bed5-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="3bed5-174">Obtenir des composants d'hôte</span><span class="sxs-lookup"><span data-stu-id="3bed5-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="3bed5-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="3bed5-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="3bed5-176">Obtenir des informations sur les composants d'hôte</span><span class="sxs-lookup"><span data-stu-id="3bed5-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="3bed5-177">HostRoles, composant, hôte, mesure</span><span class="sxs-lookup"><span data-stu-id="3bed5-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="3bed5-178">Obtenir des configurations</span><span class="sxs-lookup"><span data-stu-id="3bed5-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="3bed5-179">Types de configurations : core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="3bed5-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="3bed5-180">Obtenir des infos sur la configuration</span><span class="sxs-lookup"><span data-stu-id="3bed5-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="3bed5-181">Types de configurations : core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="3bed5-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3bed5-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3bed5-182">Next Steps</span></span>
<span data-ttu-id="3bed5-183">Maintenant que vous avez appris toouse Ambari API d’analyse des appels.</span><span class="sxs-lookup"><span data-stu-id="3bed5-183">Now you have learned how toouse Ambari monitoring API calls.</span></span> <span data-ttu-id="3bed5-184">toolearn, voir :</span><span class="sxs-lookup"><span data-stu-id="3bed5-184">toolearn more, see:</span></span>

* <span data-ttu-id="3bed5-185">[Gérer les clusters HDInsight à l’aide de hello portail Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="3bed5-185">[Manage HDInsight clusters using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="3bed5-186">[Gestion des clusters HDInsight à l’aide d’Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="3bed5-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="3bed5-187">[Gestion de clusters HDInsight à l’aide de l’interface de ligne de commande][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="3bed5-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="3bed5-188">[Documentation HDInsight][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="3bed5-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="3bed5-189">[Prise en main de HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="3bed5-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

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
