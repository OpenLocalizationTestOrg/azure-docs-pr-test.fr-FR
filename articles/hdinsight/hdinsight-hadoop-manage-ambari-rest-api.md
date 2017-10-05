---
title: "Surveiller et gérer Hadoop avec l’API REST Ambari - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment utiliser Ambari pour surveiller et gérer les clusters Hadoop dans Azure HDInsight. Dans ce document, vous allez apprendre à utiliser l'API REST d'Ambari incluse avec les clusters HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 7960d83bce22d4f671d61e9aaf55561bc24308f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-rest-api"></a><span data-ttu-id="f95fc-104">Gérer des clusters HDInsight à l'aide de l'API REST d'Ambari</span><span class="sxs-lookup"><span data-stu-id="f95fc-104">Manage HDInsight clusters by using the Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="f95fc-105">Découvrez comment utiliser l’API REST Ambari pour gérer et surveiller les clusters Hadoop dans Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f95fc-105">Learn how to use the Ambari REST API to manage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="f95fc-106">Apache Ambari simplifie la gestion et la surveillance d'un cluster Hadoop en fournissant une interface utilisateur web et une API REST faciles à utiliser.</span><span class="sxs-lookup"><span data-stu-id="f95fc-106">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="f95fc-107">Ambari est inclus dans les clusters HDInsight qui utilisent le système d’exploitation Linux.</span><span class="sxs-lookup"><span data-stu-id="f95fc-107">Ambari is included on HDInsight clusters that use the Linux operating system.</span></span> <span data-ttu-id="f95fc-108">Vous pouvez utiliser Ambari pour surveiller le cluster et apporter des modifications de configuration.</span><span class="sxs-lookup"><span data-stu-id="f95fc-108">You can use Ambari to monitor the cluster and make configuration changes.</span></span>

## <span data-ttu-id="f95fc-109"><a id="whatis"></a>Présentation d'Ambari</span><span class="sxs-lookup"><span data-stu-id="f95fc-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="f95fc-110">[Apache Ambari](http://ambari.apache.org) fournit l’interface utilisateur web qui peut être utilisée pour approvisionner, gérer et surveiller les clusters Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f95fc-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used to provision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="f95fc-111">Les développeurs peuvent intégrer ces fonctionnalités dans leurs applications à l’aide des [API REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="f95fc-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="f95fc-112">Ambari est fourni par défaut avec les clusters HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="f95fc-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-to-use-the-ambari-rest-api"></a><span data-ttu-id="f95fc-113">Comment utiliser l’API REST Ambari</span><span class="sxs-lookup"><span data-stu-id="f95fc-113">How to use the Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f95fc-114">Les informations et exemples décrits dans ce document nécessitent un cluster HDInsight utilisant Linux comme système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f95fc-114">The information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="f95fc-115">Pour plus d'informations, consultez [Prise en main de HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f95fc-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="f95fc-116">Les exemples contenus dans ce document s’appliquent au Bourne shell (Bash) et à PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f95fc-116">The examples in this document are provided for both the Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="f95fc-117">Les exemples d’interpréteur de commandes ont été testés avec GNU bash 4.3.11, mais devraient fonctionner avec d’autres interpréteurs de commandes Unix.</span><span class="sxs-lookup"><span data-stu-id="f95fc-117">The bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="f95fc-118">Les exemples PowerShell ont été testés avec PowerShell 5.0, mais devraient fonctionner avec PowerShell 3.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f95fc-118">The PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="f95fc-119">Si vous utilisez le __Bourne shell__ (Bash), les éléments suivants doivent être installés :</span><span class="sxs-lookup"><span data-stu-id="f95fc-119">If using the __Bourne shell__ (Bash), you must have the following installed:</span></span>

* <span data-ttu-id="f95fc-120">[cURL](http://curl.haxx.se/) : cURL est un utilitaire utilisable pour travailler en ligne de commande avec les API REST.</span><span class="sxs-lookup"><span data-stu-id="f95fc-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used to work with REST APIs from the command line.</span></span> <span data-ttu-id="f95fc-121">Dans ce document, il est utilisé pour communiquer avec l'API REST d'Ambari.</span><span class="sxs-lookup"><span data-stu-id="f95fc-121">In this document, it is used to communicate with the Ambari REST API.</span></span>

<span data-ttu-id="f95fc-122">Que vous utilisiez Bash ou PowerShell, vous devez également avoir installé [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="f95fc-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="f95fc-123">Jq est un utilitaire permettant de travailler avec des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="f95fc-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="f95fc-124">Il est utilisé dans **tous** les exemples de Bash et dans l’**un** des exemples de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f95fc-124">It is used in **all** the Bash examples, and **one** of the PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="f95fc-125">URI de base pour l’API Rest Ambari</span><span class="sxs-lookup"><span data-stu-id="f95fc-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="f95fc-126">L’URI de base pour l’API REST sur les clusters HDInsight est https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, où **CLUSTERNAME** est le nom de votre Storm sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f95fc-126">The base URI for the Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f95fc-127">Bien que le nom du cluster dans la partie du nom de domaine complet (FQDN) de l’URI (CLUSTERNAME.azurehdinsight.net) ne respecte pas la casse, les autres occurrences dans l’URI respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="f95fc-127">While the cluster name in the fully qualified domain name (FQDN) part of the URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in the URI are case-sensitive.</span></span> <span data-ttu-id="f95fc-128">Par exemple, si le nom de votre cluster est `MyCluster`, les éléments suivants sont des URI valides :</span><span class="sxs-lookup"><span data-stu-id="f95fc-128">For example, if your cluster is named `MyCluster`, the following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="f95fc-129">Les URI suivantes renvoient une erreur, car la deuxième occurrence du nom n’utilise pas la casse correcte.</span><span class="sxs-lookup"><span data-stu-id="f95fc-129">The following URIs return an error because the second occurrence of the name is not the correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="f95fc-130">Authentification</span><span class="sxs-lookup"><span data-stu-id="f95fc-130">Authentication</span></span>

<span data-ttu-id="f95fc-131">Une connexion à Ambari sur HDInsight requiert HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f95fc-131">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="f95fc-132">Utilisez le nom du compte Administrateur (la valeur par défaut est **admin**) et le mot de passe fournis lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-132">Use the admin account name (the default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="f95fc-133">Exemples : Authentification et analyse de JSON</span><span class="sxs-lookup"><span data-stu-id="f95fc-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="f95fc-134">Les exemples suivants montrent comment effectuer une demande GET sur l’API REST Ambari de base :</span><span class="sxs-lookup"><span data-stu-id="f95fc-134">The following examples demonstrate how to make a GET request against the base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="f95fc-135">Les exemples de Bash dans ce document partent des hypothèses suivantes :</span><span class="sxs-lookup"><span data-stu-id="f95fc-135">The Bash examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="f95fc-136">Le nom de connexion du cluster est la valeur par défaut de `admin`.</span><span class="sxs-lookup"><span data-stu-id="f95fc-136">The login name for the cluster is the default value of `admin`.</span></span>
> * <span data-ttu-id="f95fc-137">`$PASSWORD` contient le mot de passe de la commande de connexion HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f95fc-137">`$PASSWORD` contains the password for the HDInsight login command.</span></span> <span data-ttu-id="f95fc-138">Vous pouvez définir cette valeur à l’aide de `PASSWORD='mypassword'`.</span><span class="sxs-lookup"><span data-stu-id="f95fc-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="f95fc-139">`$CLUSTERNAME` contient le nom du cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-139">`$CLUSTERNAME` contains the name of the cluster.</span></span> <span data-ttu-id="f95fc-140">Vous pouvez définir cette valeur à l’aide de `set CLUSTERNAME='clustername'`.</span><span class="sxs-lookup"><span data-stu-id="f95fc-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="f95fc-141">Les exemples de PowerShell dans ce document partent des hypothèses suivantes :</span><span class="sxs-lookup"><span data-stu-id="f95fc-141">The PowerShell examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="f95fc-142">`$creds` est un objet d’informations d’identification qui contient l’identifiant et le mot de passe de l’administrateur pour l’accès au cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-142">`$creds` is a credential object that contains the admin login and password for the cluster.</span></span> <span data-ttu-id="f95fc-143">Vous pouvez définir cette valeur à l’aide de `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` et en fournissant les informations d’identification lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="f95fc-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` and providing the credentials when prompted.</span></span>
> * <span data-ttu-id="f95fc-144">`$clusterName` est une chaîne qui contient le nom du cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-144">`$clusterName` is a string that contains the name of the cluster.</span></span> <span data-ttu-id="f95fc-145">Vous pouvez définir cette valeur à l’aide de `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="f95fc-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="f95fc-146">Les deux exemples renvoient un document JSON qui commence avec des informations similaires à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="f95fc-146">Both examples return a JSON document that begins with information similar to the following example:</span></span>

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a><span data-ttu-id="f95fc-147">Analyse des données JSON</span><span class="sxs-lookup"><span data-stu-id="f95fc-147">Parsing JSON data</span></span>

<span data-ttu-id="f95fc-148">L’exemple suivant utilise `jq` pour analyser le document de réponse JSON et afficher uniquement les informations `health_report` à partir des résultats.</span><span class="sxs-lookup"><span data-stu-id="f95fc-148">The following example uses `jq` to parse the JSON response document and display only the `health_report` information from the results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="f95fc-149">PowerShell 3.0 et versions ultérieures fournissent l’applet de commande `ConvertFrom-Json` qui convertit le document JSON en un objet plus facile à utiliser avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f95fc-149">PowerShell 3.0 and higher provides the `ConvertFrom-Json` cmdlet, which converts the JSON document into an object that is easier to work with from PowerShell.</span></span> <span data-ttu-id="f95fc-150">L’exemple suivant utilise `ConvertFrom-Json` pour afficher uniquement les informations `health_report` à partir des résultats.</span><span class="sxs-lookup"><span data-stu-id="f95fc-150">The following example uses `ConvertFrom-Json` to display only the `health_report` information from the results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="f95fc-151">Alors que la plupart des exemples de ce document utilisent `ConvertFrom-Json` pour afficher les éléments du document de réponse, l’exemple [Mise à jour de la configuration Ambari](#example-update-ambari-configuration) utilise jq.</span><span class="sxs-lookup"><span data-stu-id="f95fc-151">While most examples in this document use `ConvertFrom-Json` to display elements from the response document, the [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="f95fc-152">Jq est utilisé dans cet exemple pour construire un nouveau modèle à partir du document de réponse JSON.</span><span class="sxs-lookup"><span data-stu-id="f95fc-152">Jq is used in this example to construct a new template from the JSON response document.</span></span>

<span data-ttu-id="f95fc-153">Pour obtenir une référence complète de l'API REST, consultez la page [Référence V1 de l'API d'Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="f95fc-153">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-the-fqdn-of-cluster-nodes"></a><span data-ttu-id="f95fc-154">Exemple : Obtenir le nom de domaine complet de nœuds de cluster</span><span class="sxs-lookup"><span data-stu-id="f95fc-154">Example: Get the FQDN of cluster nodes</span></span>

<span data-ttu-id="f95fc-155">Lorsque vous travaillez avec HDInsight, vous pouvez avoir besoin de connaître le nom de domaine complet (FQDN) d'un nœud de cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-155">When working with HDInsight, you may need to know the fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="f95fc-156">Vous pouvez facilement récupérer le nom de domaine complet des différents nœuds du cluster à l’aide des exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="f95fc-156">You can easily retrieve the FQDN for the various nodes in the cluster using the following examples:</span></span>

* <span data-ttu-id="f95fc-157">**Tous les nœuds**</span><span class="sxs-lookup"><span data-stu-id="f95fc-157">**All nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* <span data-ttu-id="f95fc-158">**Nœuds principaux**</span><span class="sxs-lookup"><span data-stu-id="f95fc-158">**Head nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="f95fc-159">**Nœuds de travail**</span><span class="sxs-lookup"><span data-stu-id="f95fc-159">**Worker nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="f95fc-160">**Nœuds Zookeeper**</span><span class="sxs-lookup"><span data-stu-id="f95fc-160">**Zookeeper nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-the-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="f95fc-161">Exemple : Obtenir l’adresse IP interne de nœuds de cluster</span><span class="sxs-lookup"><span data-stu-id="f95fc-161">Example: Get the internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f95fc-162">Les adresses IP renvoyées par les exemples de cette section ne sont pas directement accessibles sur Internet.</span><span class="sxs-lookup"><span data-stu-id="f95fc-162">The IP addresses returned by the examples in this section are not directly accessible over the internet.</span></span> <span data-ttu-id="f95fc-163">Elles sont uniquement accessibles au sein du réseau virtuel Azure qui contient le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f95fc-163">They are only accessible within the Azure Virtual Network that contains the HDInsight cluster.</span></span>
>
> <span data-ttu-id="f95fc-164">Pour plus d’informations sur l’utilisation de HDInsight et des réseaux virtuels, consultez [Étendre les fonctionnalités HDInsight à l’aide d’un réseau virtuel Azure personnalisé](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="f95fc-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="f95fc-165">Pour rechercher l’adresse IP, vous devez connaître le nom de domaine complet interne des nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-165">To find the IP address, you must know the internal fully qualified domain name (FQDN) of the cluster nodes.</span></span> <span data-ttu-id="f95fc-166">Lorsque cela est fait, vous pouvez ensuite obtenir l’adresse IP de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="f95fc-166">Once you have the FQDN, you can then get the IP address of the host.</span></span> <span data-ttu-id="f95fc-167">Les exemples suivants interrogent d’abord Ambari pour connaître le nom de domaine complet de tous les nœuds de l’hôte, puis l’adresse IP de chaque hôte.</span><span class="sxs-lookup"><span data-stu-id="f95fc-167">The following examples first query Ambari for the FQDN of all the host nodes, then query Ambari for the IP address of each host.</span></span>

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-the-default-storage"></a><span data-ttu-id="f95fc-168">Exemple : Obtenir le stockage par défaut</span><span class="sxs-lookup"><span data-stu-id="f95fc-168">Example: Get the default storage</span></span>

<span data-ttu-id="f95fc-169">Lorsque vous créez un cluster HDInsight, vous devez utiliser un compte de stockage Azure ou Data Lake Store comme stockage par défaut du cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as the default storage for the cluster.</span></span> <span data-ttu-id="f95fc-170">Vous pouvez utiliser Ambari pour récupérer ces informations après avoir créé le cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-170">You can use Ambari to retrieve this information after the cluster has been created.</span></span> <span data-ttu-id="f95fc-171">Par exemple, si vous voulez lire/écrire des données sur le conteneur en dehors de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f95fc-171">For example, if you want to read/write data to the container outside HDInsight.</span></span>

<span data-ttu-id="f95fc-172">Les exemples suivants récupèrent la configuration de stockage par défaut du cluster :</span><span class="sxs-lookup"><span data-stu-id="f95fc-172">The following examples retrieve the default storage configuration from the cluster:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> <span data-ttu-id="f95fc-173">Ces exemples renvoient la première configuration appliquée au serveur (`service_config_version=1`), qui contient ces informations.</span><span class="sxs-lookup"><span data-stu-id="f95fc-173">These examples return the first configuration applied to the server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="f95fc-174">Si vous récupérez une valeur qui a été modifiée après la création du cluster, vous devrez peut-être lister les versions de configuration et récupérer la plus récente.</span><span class="sxs-lookup"><span data-stu-id="f95fc-174">If you retrieve a value that has been modified after cluster creation, you may need to list the configuration versions and retrieve the latest one.</span></span>

<span data-ttu-id="f95fc-175">La valeur de retour est similaire à l’un des exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="f95fc-175">The return value is similar to one of the following examples:</span></span>

* <span data-ttu-id="f95fc-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - Cette valeur indique que le cluster utilise un compte de stockage Azure pour le stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="f95fc-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that the cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="f95fc-177">La valeur `ACCOUNTNAME` est le nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f95fc-177">The `ACCOUNTNAME` value is the name of the storage account.</span></span> <span data-ttu-id="f95fc-178">La partie `CONTAINER` est le nom du conteneur d’objets blob dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f95fc-178">The `CONTAINER` portion is the name of the blob container in the storage account.</span></span> <span data-ttu-id="f95fc-179">Le conteneur est la racine du stockage compatible HDFS du cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-179">The container is the root of the HDFS compatible storage for the cluster.</span></span>

* <span data-ttu-id="f95fc-180">`adl://home` - Cette valeur indique que le cluster utilise Azure Data Lake Store pour le stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="f95fc-180">`adl://home` - This value indicates that the cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="f95fc-181">Pour rechercher le nom du compte Data Lake Store, utilisez les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="f95fc-181">To find the Data Lake Store account name, use the following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    <span data-ttu-id="f95fc-182">La valeur de retour est similaire à `ACCOUNTNAME.azuredatalakestore.net`, où `ACCOUNTNAME` est le nom du compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f95fc-182">The return value is similar to `ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is the name of the Data Lake Store account.</span></span>

    <span data-ttu-id="f95fc-183">Pour rechercher le répertoire dans Data Lake Store qui contient le stockage du cluster, utilisez les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="f95fc-183">To find the directory within Data Lake Store that contains the storage for the cluster, use the following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    <span data-ttu-id="f95fc-184">La valeur de retour est similaire à `/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="f95fc-184">The return value is similar to `/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="f95fc-185">Cette valeur est un chemin d’accès au sein du compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f95fc-185">This value is a path within the Data Lake Store account.</span></span> <span data-ttu-id="f95fc-186">Ce chemin d’accès est la racine du système de fichiers compatible HDFS du cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-186">This path is the root of the HDFS compatible file system for the cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="f95fc-187">L’applet de commande `Get-AzureRmHDInsightCluster` fournie par [Azure PowerShell](/powershell/azure/overview) retourne également les informations de stockage du cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-187">The `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns the storage information for the cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="f95fc-188">Exemple : obtenir la configuration</span><span class="sxs-lookup"><span data-stu-id="f95fc-188">Example: Get configuration</span></span>

1. <span data-ttu-id="f95fc-189">Récupérez les configurations disponibles pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-189">Get the configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="f95fc-190">Cet exemple renvoie un document JSON avec la configuration actuelle (identifiée par la valeur *tag* ) pour les composants installés sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-190">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="f95fc-191">L’exemple suivant est un extrait des données renvoyées à partir d’un type de cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="f95fc-191">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. <span data-ttu-id="f95fc-192">Récupérez la configuration du composant qui vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="f95fc-192">Get the configuration for the component that you are interested in.</span></span> <span data-ttu-id="f95fc-193">Dans l’exemple suivant, remplacez `INITIAL` par la valeur de balise retournée à partir de la requête précédente.</span><span class="sxs-lookup"><span data-stu-id="f95fc-193">In the following example, replace `INITIAL` with the tag value returned from the previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="f95fc-194">Cet exemple renvoie un document JSON qui contient la configuration actuelle pour le composant `core-site`.</span><span class="sxs-lookup"><span data-stu-id="f95fc-194">This example returns a JSON document containing the current configuration for the `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="f95fc-195">Exemple : mettre à jour la configuration</span><span class="sxs-lookup"><span data-stu-id="f95fc-195">Example: Update configuration</span></span>

1. <span data-ttu-id="f95fc-196">Obtenir la configuration actuelle, qu’Ambari enregistre comme « configuration souhaitée » :</span><span class="sxs-lookup"><span data-stu-id="f95fc-196">Get the current configuration, which Ambari stores as the "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="f95fc-197">Cet exemple renvoie un document JSON avec la configuration actuelle (identifiée par la valeur *tag* ) pour les composants installés sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-197">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="f95fc-198">L’exemple suivant est un extrait des données renvoyées à partir d’un type de cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="f95fc-198">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    <span data-ttu-id="f95fc-199">Dans cette liste, vous devez copier le nom du composant (par exemple, **spark\_thrift\_sparkconf** et la valeur **tag**).</span><span class="sxs-lookup"><span data-stu-id="f95fc-199">From this list, you need to copy the name of the component (for example, **spark\_thrift\_sparkconf** and the **tag** value.</span></span>

2. <span data-ttu-id="f95fc-200">Récupérez la configuration du composant et de la balise à l’aide des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f95fc-200">Retrieve the configuration for the component and tag by using the following commands:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > <span data-ttu-id="f95fc-201">Remplacez **spark-thrift-sparkconf** et **INITIAL** par le composant et la balise dont vous souhaitez récupérer la configuration.</span><span class="sxs-lookup"><span data-stu-id="f95fc-201">Replace **spark-thrift-sparkconf** and **INITIAL** with the component and tag that you want to retrieve the configuration for.</span></span>
   
    <span data-ttu-id="f95fc-202">Jq est utilisé pour convertir les données récupérées à partir de HDInsight dans un nouveau modèle de configuration.</span><span class="sxs-lookup"><span data-stu-id="f95fc-202">Jq is used to turn the data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="f95fc-203">Plus précisément, ces exemples permettent d’effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="f95fc-203">Specifically, these examples perform the following actions:</span></span>
   
    * <span data-ttu-id="f95fc-204">Il crée une valeur unique qui contient la chaîne « version » et la date, qui est stockée dans `newtag`.</span><span class="sxs-lookup"><span data-stu-id="f95fc-204">Creates a unique value containing the string "version" and the date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="f95fc-205">Il crée un document racine pour la nouvelle configuration souhaitée.</span><span class="sxs-lookup"><span data-stu-id="f95fc-205">Creates a root document for the new desired configuration.</span></span>

    * <span data-ttu-id="f95fc-206">Il récupère le contenu du tableau `.items[]` et l’ajoute à l’élément **desired_config**.</span><span class="sxs-lookup"><span data-stu-id="f95fc-206">Gets the contents of the `.items[]` array and adds it under the **desired_config** element.</span></span>

    * <span data-ttu-id="f95fc-207">Il supprime les éléments `href`, `version` et `Config`, car ils ne sont pas nécessaires à l’envoi d’une nouvelle configuration.</span><span class="sxs-lookup"><span data-stu-id="f95fc-207">Deletes the `href`, `version`, and `Config` elements, as these elements aren't needed to submit a new configuration.</span></span>

    * <span data-ttu-id="f95fc-208">Ajoute un élément `tag` avec une valeur de `version#################`.</span><span class="sxs-lookup"><span data-stu-id="f95fc-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="f95fc-209">La partie numérique est basée sur la date actuelle.</span><span class="sxs-lookup"><span data-stu-id="f95fc-209">The numeric portion is based on the current date.</span></span> <span data-ttu-id="f95fc-210">Chaque configuration doit avoir une balise unique.</span><span class="sxs-lookup"><span data-stu-id="f95fc-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="f95fc-211">Enfin, les données sont enregistrées dans le document `newconfig.json`.</span><span class="sxs-lookup"><span data-stu-id="f95fc-211">Finally, the data is saved to the `newconfig.json` document.</span></span> <span data-ttu-id="f95fc-212">La structure du document doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="f95fc-212">The document structure should appear similar to the following example:</span></span>
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. <span data-ttu-id="f95fc-213">Ouvrez le document `newconfig.json` et modifiez/ajoutez des valeurs dans l’objet `properties`.</span><span class="sxs-lookup"><span data-stu-id="f95fc-213">Open the `newconfig.json` document and modify/add values in the `properties` object.</span></span> <span data-ttu-id="f95fc-214">L’exemple suivant modifie la valeur de `"spark.yarn.am.memory"` de `"1g"` en `"3g"`.</span><span class="sxs-lookup"><span data-stu-id="f95fc-214">The following example changes the value of `"spark.yarn.am.memory"` from `"1g"` to `"3g"`.</span></span> <span data-ttu-id="f95fc-215">Il ajoute également `"spark.kryoserializer.buffer.max"` avec une valeur de `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="f95fc-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="f95fc-216">Enregistrez le fichier une fois que vous avez apporté des modifications.</span><span class="sxs-lookup"><span data-stu-id="f95fc-216">Save the file once you are done making modifications.</span></span>

4. <span data-ttu-id="f95fc-217">Utilisez les commandes suivantes pour envoyer la configuration mise à jour à Ambari.</span><span class="sxs-lookup"><span data-stu-id="f95fc-217">Use the following commands to submit the updated configuration to Ambari.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    <span data-ttu-id="f95fc-218">Ces commandes envoient le contenu du fichier **newconfig.json** au cluster en tant que nouvelle configuration souhaitée.</span><span class="sxs-lookup"><span data-stu-id="f95fc-218">These commands submit the contents of the **newconfig.json** file to the cluster as the new desired configuration.</span></span> <span data-ttu-id="f95fc-219">La demande renvoie un document JSON.</span><span class="sxs-lookup"><span data-stu-id="f95fc-219">The request returns a JSON document.</span></span> <span data-ttu-id="f95fc-220">L’élément **versionTag** de ce document doit correspondre à la version que vous avez envoyée et l’objet **configs** contient les modifications de configuration que vous avez demandées.</span><span class="sxs-lookup"><span data-stu-id="f95fc-220">The **versionTag** element in this document should match the version you submitted, and the **configs** object contains the configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="f95fc-221">Exemple : redémarrer un composant de service</span><span class="sxs-lookup"><span data-stu-id="f95fc-221">Example: Restart a service component</span></span>

<span data-ttu-id="f95fc-222">À ce stade, si vous regardez l’interface web d’Ambari, le service Spark indique qu’il doit être redémarré pour que la nouvelle configuration prenne effet.</span><span class="sxs-lookup"><span data-stu-id="f95fc-222">At this point, if you look at the Ambari web UI, the Spark service indicates that it needs to be restarted before the new configuration can take effect.</span></span> <span data-ttu-id="f95fc-223">Procédez comme suit pour redémarrer le service.</span><span class="sxs-lookup"><span data-stu-id="f95fc-223">Use the following steps to restart the service.</span></span>

1. <span data-ttu-id="f95fc-224">Utilisez ce qui suit pour activer le mode de maintenance du service Spark :</span><span class="sxs-lookup"><span data-stu-id="f95fc-224">Use the following to enable maintenance mode for the Spark service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    <span data-ttu-id="f95fc-225">Ces commandes envoient un document JSON au serveur qui active le mode de maintenance.</span><span class="sxs-lookup"><span data-stu-id="f95fc-225">These commands send a JSON document to the server that turns on maintenance mode.</span></span> <span data-ttu-id="f95fc-226">Vous pouvez vérifier que le service est désormais en mode maintenance à l’aide de la demande suivante :</span><span class="sxs-lookup"><span data-stu-id="f95fc-226">You can verify that the service is now in maintenance mode using the following request:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    <span data-ttu-id="f95fc-227">La valeur de retour est `ON`.</span><span class="sxs-lookup"><span data-stu-id="f95fc-227">The return value is `ON`.</span></span>

2. <span data-ttu-id="f95fc-228">Ensuite, utilisez ce qui suit pour désactiver le service :</span><span class="sxs-lookup"><span data-stu-id="f95fc-228">Next, use the following to turn off the service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    <span data-ttu-id="f95fc-229">La réponse ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="f95fc-229">The response is similar to the following example:</span></span>
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > <span data-ttu-id="f95fc-230">La valeur `href` retournée par cet URI à l’aide de l’adresse IP interne du nœud du cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-230">The `href` value returned by this URI is using the internal IP address of the cluster node.</span></span> <span data-ttu-id="f95fc-231">Pour l’utiliser depuis l’extérieur du cluster, remplacez la partie « 10.0.0.18:8080 » par le nom de domaine complet du cluster.</span><span class="sxs-lookup"><span data-stu-id="f95fc-231">To use it from outside the cluster, replace the \`10.0.0.18:8080' portion with the FQDN of the cluster.</span></span> 
    
    <span data-ttu-id="f95fc-232">Les commandes suivantes récupèrent l’état de la demande :</span><span class="sxs-lookup"><span data-stu-id="f95fc-232">The following commands retrieve the status of the request:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    <span data-ttu-id="f95fc-233">Une réponse de `COMPLETED` indique que la demande est terminée.</span><span class="sxs-lookup"><span data-stu-id="f95fc-233">A response of `COMPLETED` indicates that the request has finished.</span></span>

3. <span data-ttu-id="f95fc-234">Une fois la demande précédente terminée, utilisez ce qui suit pour démarrer le service.</span><span class="sxs-lookup"><span data-stu-id="f95fc-234">Once the previous request completes, use the following to start the service.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    <span data-ttu-id="f95fc-235">Le service utilise désormais la nouvelle configuration.</span><span class="sxs-lookup"><span data-stu-id="f95fc-235">The service is now using the new configuration.</span></span>

4. <span data-ttu-id="f95fc-236">Enfin, utilisez les éléments suivants pour désactiver le mode de maintenance.</span><span class="sxs-lookup"><span data-stu-id="f95fc-236">Finally, use the following to turn off maintenance mode.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a><span data-ttu-id="f95fc-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f95fc-237">Next steps</span></span>

<span data-ttu-id="f95fc-238">Pour obtenir une référence complète de l'API REST, consultez la page [Référence V1 de l'API d'Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="f95fc-238">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

