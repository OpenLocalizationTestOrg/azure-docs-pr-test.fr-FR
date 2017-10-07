---
title: "aaaMonitor et gérer Hadoop avec l’API REST de Ambari - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toouse Ambari toomonitor et gérer des clusters Hadoop dans HDInsight de Azure. Dans ce document, vous allez apprendre comment toouse hello API REST de Ambari inclus avec HDInsight clusters."
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
ms.openlocfilehash: 1866a77c8e402231bccbcfba7174253aca41339b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a><span data-ttu-id="dc26d-104">Gérer des clusters HDInsight à l’aide de hello API REST de Ambari</span><span class="sxs-lookup"><span data-stu-id="dc26d-104">Manage HDInsight clusters by using hello Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="dc26d-105">Découvrez comment toouse hello API REST de Ambari toomanage et analyser les clusters Hadoop dans HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc26d-105">Learn how toouse hello Ambari REST API toomanage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="dc26d-106">Apache Ambari simplifie la gestion de hello et la surveillance d’un cluster Hadoop en fournissant un web toouse simple API REST et de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dc26d-106">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="dc26d-107">Ambari est inclus dans les clusters HDInsight qui utilisent le système d’exploitation de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-107">Ambari is included on HDInsight clusters that use hello Linux operating system.</span></span> <span data-ttu-id="dc26d-108">Vous pouvez utiliser Ambari toomonitor hello cluster et apporter des modifications de configuration.</span><span class="sxs-lookup"><span data-stu-id="dc26d-108">You can use Ambari toomonitor hello cluster and make configuration changes.</span></span>

## <span data-ttu-id="dc26d-109"><a id="whatis"></a>Présentation d'Ambari</span><span class="sxs-lookup"><span data-stu-id="dc26d-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="dc26d-110">[Apache Ambari](http://ambari.apache.org) fournit l’interface utilisateur web qui peut être utilisée tooprovision, gérer et surveiller les clusters Hadoop.</span><span class="sxs-lookup"><span data-stu-id="dc26d-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used tooprovision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="dc26d-111">Les développeurs peuvent intégrer ces fonctionnalités dans leurs applications à l’aide de hello [API REST de Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="dc26d-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="dc26d-112">Ambari est fourni par défaut avec les clusters HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="dc26d-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-toouse-hello-ambari-rest-api"></a><span data-ttu-id="dc26d-113">Comment toouse hello API REST de Ambari</span><span class="sxs-lookup"><span data-stu-id="dc26d-113">How toouse hello Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc26d-114">informations de Hello et d’exemples dans ce document nécessitent un cluster HDInsight qui utilise le système d’exploitation Linux.</span><span class="sxs-lookup"><span data-stu-id="dc26d-114">hello information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="dc26d-115">Pour plus d'informations, consultez [Prise en main de HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dc26d-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="dc26d-116">exemples de Hello dans ce document sont fournies pour hello Bourne shell (interpréteur de commandes) et PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc26d-116">hello examples in this document are provided for both hello Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="dc26d-117">bash Hello exemples ont été testés avec GNU bash 4.3.11, mais doit fonctionner avec d’autres interpréteurs de commandes Unix.</span><span class="sxs-lookup"><span data-stu-id="dc26d-117">hello bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="dc26d-118">exemples de PowerShell Hello ont été testés avec PowerShell 5.0, mais doivent fonctionner avec PowerShell 3.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="dc26d-118">hello PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="dc26d-119">Si vous utilisez hello __Bourne shell__ (interpréteur de commandes), vous devez disposer de hello installé :</span><span class="sxs-lookup"><span data-stu-id="dc26d-119">If using hello __Bourne shell__ (Bash), you must have hello following installed:</span></span>

* <span data-ttu-id="dc26d-120">[cURL](http://curl.haxx.se/): cURL est un utilitaire qui peut être toowork utilisé avec l’API REST à partir de la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used toowork with REST APIs from hello command line.</span></span> <span data-ttu-id="dc26d-121">Dans ce document, il est utilisé toocommunicate avec hello Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="dc26d-121">In this document, it is used toocommunicate with hello Ambari REST API.</span></span>

<span data-ttu-id="dc26d-122">Que vous utilisiez Bash ou PowerShell, vous devez également avoir installé [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="dc26d-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="dc26d-123">Jq est un utilitaire permettant de travailler avec des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="dc26d-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="dc26d-124">Il est utilisé dans **tous les** hello des exemples de l’interpréteur de commandes, et **un** des exemples de PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-124">It is used in **all** hello Bash examples, and **one** of hello PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="dc26d-125">URI de base pour l’API Rest Ambari</span><span class="sxs-lookup"><span data-stu-id="dc26d-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="dc26d-126">URI de base pour l’API REST de Ambari sur HDInsight de hello Hello est https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, où **CLUSTERNAME** est le nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="dc26d-126">hello base URI for hello Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc26d-127">Alors que le nom du cluster hello Bonjour complet partie de nom de domaine de hello URI (CLUSTERNAME.azurehdinsight.net) respecte la casse, autres occurrences Bonjour URI respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="dc26d-127">While hello cluster name in hello fully qualified domain name (FQDN) part of hello URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in hello URI are case-sensitive.</span></span> <span data-ttu-id="dc26d-128">Par exemple, si votre cluster est nommé `MyCluster`, hello Voici URI valide :</span><span class="sxs-lookup"><span data-stu-id="dc26d-128">For example, if your cluster is named `MyCluster`, hello following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="dc26d-129">suit Hello URI renvoie une erreur car hello deuxième occurrence du nom de hello n’est pas hello corrige le cas.</span><span class="sxs-lookup"><span data-stu-id="dc26d-129">hello following URIs return an error because hello second occurrence of hello name is not hello correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="dc26d-130">Authentification</span><span class="sxs-lookup"><span data-stu-id="dc26d-130">Authentication</span></span>

<span data-ttu-id="dc26d-131">Connexion tooAmbari sur HDInsight nécessite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="dc26d-131">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="dc26d-132">Nom du compte administrateur utilisez hello (valeur par défaut hello est **admin**) et le mot de passe fourni lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="dc26d-132">Use hello admin account name (hello default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="dc26d-133">Exemples : Authentification et analyse de JSON</span><span class="sxs-lookup"><span data-stu-id="dc26d-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="dc26d-134">Hello suivant exemples montrent comment toomake une demande GET hello Ambari REST API de base :</span><span class="sxs-lookup"><span data-stu-id="dc26d-134">hello following examples demonstrate how toomake a GET request against hello base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="dc26d-135">exemples d’interpréteur de commandes Hello dans ce document apporter hello suivant hypothèses :</span><span class="sxs-lookup"><span data-stu-id="dc26d-135">hello Bash examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="dc26d-136">nom de connexion de Hello pour le cluster de hello est la valeur par défaut hello `admin`.</span><span class="sxs-lookup"><span data-stu-id="dc26d-136">hello login name for hello cluster is hello default value of `admin`.</span></span>
> * <span data-ttu-id="dc26d-137">`$PASSWORD`contient le mot de passe hello hello commande de connexion HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc26d-137">`$PASSWORD` contains hello password for hello HDInsight login command.</span></span> <span data-ttu-id="dc26d-138">Vous pouvez définir cette valeur à l’aide de `PASSWORD='mypassword'`.</span><span class="sxs-lookup"><span data-stu-id="dc26d-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="dc26d-139">`$CLUSTERNAME`contient le nom hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-139">`$CLUSTERNAME` contains hello name of hello cluster.</span></span> <span data-ttu-id="dc26d-140">Vous pouvez définir cette valeur à l’aide de `set CLUSTERNAME='clustername'`.</span><span class="sxs-lookup"><span data-stu-id="dc26d-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="dc26d-141">exemples de PowerShell Hello dans ce document apporter hello suivant hypothèses :</span><span class="sxs-lookup"><span data-stu-id="dc26d-141">hello PowerShell examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="dc26d-142">`$creds`est un objet d’informations d’identification qui contient la connexion d’administration hello et un mot de passe pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-142">`$creds` is a credential object that contains hello admin login and password for hello cluster.</span></span> <span data-ttu-id="dc26d-143">Vous pouvez définir cette valeur à l’aide de `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` et en fournissant des informations d’identification hello lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="dc26d-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` and providing hello credentials when prompted.</span></span>
> * <span data-ttu-id="dc26d-144">`$clusterName`est une chaîne qui contient le nom hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-144">`$clusterName` is a string that contains hello name of hello cluster.</span></span> <span data-ttu-id="dc26d-145">Vous pouvez définir cette valeur à l’aide de `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="dc26d-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="dc26d-146">Les deux exemples de retournent un document JSON qui commence avec les informations toohello semblable l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="dc26d-146">Both examples return a JSON document that begins with information similar toohello following example:</span></span>

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

### <a name="parsing-json-data"></a><span data-ttu-id="dc26d-147">Analyse des données JSON</span><span class="sxs-lookup"><span data-stu-id="dc26d-147">Parsing JSON data</span></span>

<span data-ttu-id="dc26d-148">Hello exemple suivant utilise `jq` tooparse hello document de réponse JSON et afficher uniquement hello `health_report` plus d’informations à partir des résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-148">hello following example uses `jq` tooparse hello JSON response document and display only hello `health_report` information from hello results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="dc26d-149">PowerShell 3.0 et versions ultérieures fournit hello `ConvertFrom-Json` applet de commande, qui convertit le document JSON de hello dans un objet qui est plus facile toowork avec à partir de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc26d-149">PowerShell 3.0 and higher provides hello `ConvertFrom-Json` cmdlet, which converts hello JSON document into an object that is easier toowork with from PowerShell.</span></span> <span data-ttu-id="dc26d-150">Hello exemple suivant utilise `ConvertFrom-Json` hello uniquement de toodisplay `health_report` plus d’informations à partir des résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-150">hello following example uses `ConvertFrom-Json` toodisplay only hello `health_report` information from hello results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="dc26d-151">Alors que la plupart des exemples de ce document, utilisez `ConvertFrom-Json` toodisplay des éléments à partir du document de réponse hello, hello [configuration de la mise à jour Ambari](#example-update-ambari-configuration) exemple utilise jq.</span><span class="sxs-lookup"><span data-stu-id="dc26d-151">While most examples in this document use `ConvertFrom-Json` toodisplay elements from hello response document, hello [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="dc26d-152">Jq est utilisé dans cet exemple tooconstruct un nouveau modèle de document de réponse JSON hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-152">Jq is used in this example tooconstruct a new template from hello JSON response document.</span></span>

<span data-ttu-id="dc26d-153">Pour obtenir une référence complète de hello API REST, consultez [V1 de référence d’API Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="dc26d-153">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a><span data-ttu-id="dc26d-154">Exemple : Obtenir hello FQDN des nœuds de cluster</span><span class="sxs-lookup"><span data-stu-id="dc26d-154">Example: Get hello FQDN of cluster nodes</span></span>

<span data-ttu-id="dc26d-155">Lorsque vous travaillez avec HDInsight, vous devrez peut-être le nom de domaine complet de hello tooknow (FQDN) d’un nœud de cluster.</span><span class="sxs-lookup"><span data-stu-id="dc26d-155">When working with HDInsight, you may need tooknow hello fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="dc26d-156">Vous pouvez facilement récupérer hello nom de domaine complet pour hello différents nœuds dans le cluster hello à l’aide de hello exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="dc26d-156">You can easily retrieve hello FQDN for hello various nodes in hello cluster using hello following examples:</span></span>

* <span data-ttu-id="dc26d-157">**Tous les nœuds**</span><span class="sxs-lookup"><span data-stu-id="dc26d-157">**All nodes**</span></span>

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

* <span data-ttu-id="dc26d-158">**Nœuds principaux**</span><span class="sxs-lookup"><span data-stu-id="dc26d-158">**Head nodes**</span></span>

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

* <span data-ttu-id="dc26d-159">**Nœuds de travail**</span><span class="sxs-lookup"><span data-stu-id="dc26d-159">**Worker nodes**</span></span>

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

* <span data-ttu-id="dc26d-160">**Nœuds Zookeeper**</span><span class="sxs-lookup"><span data-stu-id="dc26d-160">**Zookeeper nodes**</span></span>

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

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="dc26d-161">Exemple : Obtenir l’adresse IP interne de hello des nœuds de cluster</span><span class="sxs-lookup"><span data-stu-id="dc26d-161">Example: Get hello internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc26d-162">adresses IP de Hello retournées par les exemples hello dans cette section sont pas directement accessibles sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="dc26d-162">hello IP addresses returned by hello examples in this section are not directly accessible over hello internet.</span></span> <span data-ttu-id="dc26d-163">Elles sont uniquement accessibles hello réseau virtuel Azure qui contient le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-163">They are only accessible within hello Azure Virtual Network that contains hello HDInsight cluster.</span></span>
>
> <span data-ttu-id="dc26d-164">Pour plus d’informations sur l’utilisation de HDInsight et des réseaux virtuels, consultez [Étendre les fonctionnalités HDInsight à l’aide d’un réseau virtuel Azure personnalisé](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="dc26d-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="dc26d-165">adresse IP de hello toofind, vous devez connaître le nom hello interne de domaine complet (FQDN) de hello des nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="dc26d-165">toofind hello IP address, you must know hello internal fully qualified domain name (FQDN) of hello cluster nodes.</span></span> <span data-ttu-id="dc26d-166">Une fois que vous avez hello nom de domaine complet, vous pouvez ensuite obtenir l’adresse IP de hello d’hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-166">Once you have hello FQDN, you can then get hello IP address of hello host.</span></span> <span data-ttu-id="dc26d-167">Hello exemples suivants tout d’abord interroger Ambari pourquoi le nom de domaine complet de tous les nœuds d’hôte hello, puis interroge Ambari pour l’adresse IP de hello de chaque hôte.</span><span class="sxs-lookup"><span data-stu-id="dc26d-167">hello following examples first query Ambari for hello FQDN of all hello host nodes, then query Ambari for hello IP address of each host.</span></span>

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

## <a name="example-get-hello-default-storage"></a><span data-ttu-id="dc26d-168">Exemple : Obtenir du stockage par défaut hello</span><span class="sxs-lookup"><span data-stu-id="dc26d-168">Example: Get hello default storage</span></span>

<span data-ttu-id="dc26d-169">Lorsque vous créez un cluster HDInsight, vous devez utiliser un compte de stockage Azure ou le Data Lake Store en tant que stockage de hello par défaut pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as hello default storage for hello cluster.</span></span> <span data-ttu-id="dc26d-170">Vous pouvez utiliser ces informations à Ambari tooretrieve après que hello cluster a été créé.</span><span class="sxs-lookup"><span data-stu-id="dc26d-170">You can use Ambari tooretrieve this information after hello cluster has been created.</span></span> <span data-ttu-id="dc26d-171">Par exemple, si vous souhaitez que le conteneur de toohello données tooread/écriture à l’extérieur de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc26d-171">For example, if you want tooread/write data toohello container outside HDInsight.</span></span>

<span data-ttu-id="dc26d-172">Hello exemples suivants extraire configuration de stockage par défaut hello de cluster de hello :</span><span class="sxs-lookup"><span data-stu-id="dc26d-172">hello following examples retrieve hello default storage configuration from hello cluster:</span></span>

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
> <span data-ttu-id="dc26d-173">Les exemples ci-après renvoient hello première configuration appliquée toohello server (`service_config_version=1`) qui contient ces informations.</span><span class="sxs-lookup"><span data-stu-id="dc26d-173">These examples return hello first configuration applied toohello server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="dc26d-174">Si vous récupérez une valeur qui a été modifiée après la création du cluster, vous ont besoin des versions de configuration toolist hello et récupérer la version la plus récente de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-174">If you retrieve a value that has been modified after cluster creation, you may need toolist hello configuration versions and retrieve hello latest one.</span></span>

<span data-ttu-id="dc26d-175">valeur de retour de Hello est similaire tooone Hello exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="dc26d-175">hello return value is similar tooone of hello following examples:</span></span>

* <span data-ttu-id="dc26d-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Cette valeur indique que ce cluster hello utilise un compte de stockage Azure pour le stockage de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="dc26d-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that hello cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="dc26d-177">Hello `ACCOUNTNAME` valeur est le nom hello hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dc26d-177">hello `ACCOUNTNAME` value is hello name of hello storage account.</span></span> <span data-ttu-id="dc26d-178">Hello `CONTAINER` partie est le nom de hello du conteneur d’objets blob hello hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dc26d-178">hello `CONTAINER` portion is hello name of hello blob container in hello storage account.</span></span> <span data-ttu-id="dc26d-179">conteneur de Hello est racine hello hello stockage compatible de HDFS pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-179">hello container is hello root of hello HDFS compatible storage for hello cluster.</span></span>

* <span data-ttu-id="dc26d-180">`adl://home`-Cette valeur indique que le cluster hello utilise une Azure Data Lake Store pour le stockage de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="dc26d-180">`adl://home` - This value indicates that hello cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="dc26d-181">toofind hello nom du compte Data Lake Store, utilisez hello exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="dc26d-181">toofind hello Data Lake Store account name, use hello following examples:</span></span>

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

    <span data-ttu-id="dc26d-182">Hello valeur de retour est similaire trop`ACCOUNTNAME.azuredatalakestore.net`, où `ACCOUNTNAME` est le nom hello Hello compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dc26d-182">hello return value is similar too`ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is hello name of hello Data Lake Store account.</span></span>

    <span data-ttu-id="dc26d-183">répertoire hello toofind Data Lake Store qui contient le stockage hello pour cluster hello, hello utilisez exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="dc26d-183">toofind hello directory within Data Lake Store that contains hello storage for hello cluster, use hello following examples:</span></span>

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

    <span data-ttu-id="dc26d-184">Hello valeur de retour est similaire trop`/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="dc26d-184">hello return value is similar too`/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="dc26d-185">Cette valeur est un chemin d’accès au sein de hello compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dc26d-185">This value is a path within hello Data Lake Store account.</span></span> <span data-ttu-id="dc26d-186">Ce chemin d’accès est la racine hello hello système de fichier compatible HDFS pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-186">This path is hello root of hello HDFS compatible file system for hello cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="dc26d-187">Hello `Get-AzureRmHDInsightCluster` applet de commande fournie par [Azure PowerShell](/powershell/azure/overview) également retourne hello les informations de stockage de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-187">hello `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns hello storage information for hello cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="dc26d-188">Exemple : obtenir la configuration</span><span class="sxs-lookup"><span data-stu-id="dc26d-188">Example: Get configuration</span></span>

1. <span data-ttu-id="dc26d-189">Obtenir des configurations de hello qui sont disponibles pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="dc26d-189">Get hello configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="dc26d-190">Cet exemple retourne un document JSON contenant la configuration actuelle de hello (identifié par hello *balise* valeur) pour les composants hello installés sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-190">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="dc26d-191">Hello exemple suivant est un extrait à partir des données hello retournés à partir d’un type de cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="dc26d-191">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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

2. <span data-ttu-id="dc26d-192">Obtenir la configuration hello pour le composant hello qui vous intéressez.</span><span class="sxs-lookup"><span data-stu-id="dc26d-192">Get hello configuration for hello component that you are interested in.</span></span> <span data-ttu-id="dc26d-193">Bonjour à l’exemple, remplacez `INITIAL` avec la valeur de balise hello retourné à partir de la demande précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-193">In hello following example, replace `INITIAL` with hello tag value returned from hello previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="dc26d-194">Cet exemple retourne un document JSON contenant la configuration actuelle de hello pour hello `core-site` composant.</span><span class="sxs-lookup"><span data-stu-id="dc26d-194">This example returns a JSON document containing hello current configuration for hello `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="dc26d-195">Exemple : mettre à jour la configuration</span><span class="sxs-lookup"><span data-stu-id="dc26d-195">Example: Update configuration</span></span>

1. <span data-ttu-id="dc26d-196">Obtenir la configuration actuelle de hello, qui stocke les Ambari hello souhaitée « configuration » :</span><span class="sxs-lookup"><span data-stu-id="dc26d-196">Get hello current configuration, which Ambari stores as hello "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="dc26d-197">Cet exemple retourne un document JSON contenant la configuration actuelle de hello (identifié par hello *balise* valeur) pour les composants hello installés sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-197">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="dc26d-198">Hello exemple suivant est un extrait à partir des données hello retournés à partir d’un type de cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="dc26d-198">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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
   
    <span data-ttu-id="dc26d-199">Dans cette liste, vous avez besoin d’un nom de hello de toocopy du composant de hello (par exemple, **spark\_thrift\_sparkconf** et hello **balise** valeur.</span><span class="sxs-lookup"><span data-stu-id="dc26d-199">From this list, you need toocopy hello name of hello component (for example, **spark\_thrift\_sparkconf** and hello **tag** value.</span></span>

2. <span data-ttu-id="dc26d-200">Récupérer configuration hello pour le composant de hello et de la balise à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="dc26d-200">Retrieve hello configuration for hello component and tag by using hello following commands:</span></span>
   
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
    > <span data-ttu-id="dc26d-201">Remplacez **spark-thrift-sparkconf** et **initiale** avec le composant de hello et la balise que vous voulez tooretrieve configuration hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-201">Replace **spark-thrift-sparkconf** and **INITIAL** with hello component and tag that you want tooretrieve hello configuration for.</span></span>
   
    <span data-ttu-id="dc26d-202">Jq donnée utilisé tooturn hello récupérées à partir de HDInsight dans un nouveau modèle de configuration.</span><span class="sxs-lookup"><span data-stu-id="dc26d-202">Jq is used tooturn hello data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="dc26d-203">Plus précisément, ces exemples effectuent hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="dc26d-203">Specifically, these examples perform hello following actions:</span></span>
   
    * <span data-ttu-id="dc26d-204">Crée une valeur unique qui contient « version » de chaîne hello et date hello, qui est stocké dans `newtag`.</span><span class="sxs-lookup"><span data-stu-id="dc26d-204">Creates a unique value containing hello string "version" and hello date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="dc26d-205">Crée un document racine pour la nouvelle configuration de votre choix hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-205">Creates a root document for hello new desired configuration.</span></span>

    * <span data-ttu-id="dc26d-206">Obtient hello contenu Hello `.items[]` de tableau et l’ajoute sous hello **desired_config** élément.</span><span class="sxs-lookup"><span data-stu-id="dc26d-206">Gets hello contents of hello `.items[]` array and adds it under hello **desired_config** element.</span></span>

    * <span data-ttu-id="dc26d-207">Suppressions hello `href`, `version`, et `Config` éléments, en tant que ces éléments ne sont pas nécessaire toosubmit une nouvelle configuration.</span><span class="sxs-lookup"><span data-stu-id="dc26d-207">Deletes hello `href`, `version`, and `Config` elements, as these elements aren't needed toosubmit a new configuration.</span></span>

    * <span data-ttu-id="dc26d-208">Ajoute un élément `tag` avec une valeur de `version#################`.</span><span class="sxs-lookup"><span data-stu-id="dc26d-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="dc26d-209">partie numérique de Hello repose sur hello date actuelle.</span><span class="sxs-lookup"><span data-stu-id="dc26d-209">hello numeric portion is based on hello current date.</span></span> <span data-ttu-id="dc26d-210">Chaque configuration doit avoir une balise unique.</span><span class="sxs-lookup"><span data-stu-id="dc26d-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="dc26d-211">Enfin, les données de salutation sont enregistrées toohello `newconfig.json` document.</span><span class="sxs-lookup"><span data-stu-id="dc26d-211">Finally, hello data is saved toohello `newconfig.json` document.</span></span> <span data-ttu-id="dc26d-212">structure du document Hello doit apparaître toohello similaire, l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="dc26d-212">hello document structure should appear similar toohello following example:</span></span>
     
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

3. <span data-ttu-id="dc26d-213">Ouvrez hello `newconfig.json` document et modifier/ajouter des valeurs Bonjour `properties` objet.</span><span class="sxs-lookup"><span data-stu-id="dc26d-213">Open hello `newconfig.json` document and modify/add values in hello `properties` object.</span></span> <span data-ttu-id="dc26d-214">valeur de hello Hello exemple suivant modifie `"spark.yarn.am.memory"` de `"1g"` trop`"3g"`.</span><span class="sxs-lookup"><span data-stu-id="dc26d-214">hello following example changes hello value of `"spark.yarn.am.memory"` from `"1g"` too`"3g"`.</span></span> <span data-ttu-id="dc26d-215">Il ajoute également `"spark.kryoserializer.buffer.max"` avec une valeur de `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="dc26d-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="dc26d-216">Enregistrer le fichier de hello une fois que vous avez terminé d’apporter de modifications.</span><span class="sxs-lookup"><span data-stu-id="dc26d-216">Save hello file once you are done making modifications.</span></span>

4. <span data-ttu-id="dc26d-217">Utilisez hello suivant tooAmbari de configuration de commandes toosubmit hello mis à jour.</span><span class="sxs-lookup"><span data-stu-id="dc26d-217">Use hello following commands toosubmit hello updated configuration tooAmbari.</span></span>
   
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
   
    <span data-ttu-id="dc26d-218">Ces commandes Soumettre contenu hello Hello **newconfig.json** fichier toohello cluster convenance hello nouvelle configuration.</span><span class="sxs-lookup"><span data-stu-id="dc26d-218">These commands submit hello contents of hello **newconfig.json** file toohello cluster as hello new desired configuration.</span></span> <span data-ttu-id="dc26d-219">demande de Hello renvoie un document JSON.</span><span class="sxs-lookup"><span data-stu-id="dc26d-219">hello request returns a JSON document.</span></span> <span data-ttu-id="dc26d-220">Hello **versionTag** élément dans ce document doit correspondre à version hello vous soumis et hello **configurations** objet contient des modifications de configuration hello que vous avez demandée.</span><span class="sxs-lookup"><span data-stu-id="dc26d-220">hello **versionTag** element in this document should match hello version you submitted, and hello **configs** object contains hello configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="dc26d-221">Exemple : redémarrer un composant de service</span><span class="sxs-lookup"><span data-stu-id="dc26d-221">Example: Restart a service component</span></span>

<span data-ttu-id="dc26d-222">À ce stade, si vous examinez l’interface utilisateur web de Ambari hello, hello service Spark indique qu’il doit toobe redémarré pour que la nouvelle configuration de hello puisse prendre effet.</span><span class="sxs-lookup"><span data-stu-id="dc26d-222">At this point, if you look at hello Ambari web UI, hello Spark service indicates that it needs toobe restarted before hello new configuration can take effect.</span></span> <span data-ttu-id="dc26d-223">Utilisez hello après étapes toorestart hello service.</span><span class="sxs-lookup"><span data-stu-id="dc26d-223">Use hello following steps toorestart hello service.</span></span>

1. <span data-ttu-id="dc26d-224">Utilisez hello suivant le mode de maintenance tooenable pour hello service Spark :</span><span class="sxs-lookup"><span data-stu-id="dc26d-224">Use hello following tooenable maintenance mode for hello Spark service:</span></span>

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
   
    <span data-ttu-id="dc26d-225">Ces commandes envoient un serveur de toohello document JSON qui active le mode de maintenance.</span><span class="sxs-lookup"><span data-stu-id="dc26d-225">These commands send a JSON document toohello server that turns on maintenance mode.</span></span> <span data-ttu-id="dc26d-226">Vous pouvez vérifier que hello service est maintenant en mode de maintenance à l’aide de hello demande :</span><span class="sxs-lookup"><span data-stu-id="dc26d-226">You can verify that hello service is now in maintenance mode using hello following request:</span></span>
   
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
   
    <span data-ttu-id="dc26d-227">Hello valeur de retour est `ON`.</span><span class="sxs-lookup"><span data-stu-id="dc26d-227">hello return value is `ON`.</span></span>

2. <span data-ttu-id="dc26d-228">Ensuite, utilisez hello suivant tooturn hors service de hello :</span><span class="sxs-lookup"><span data-stu-id="dc26d-228">Next, use hello following tooturn off hello service:</span></span>

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
    
    <span data-ttu-id="dc26d-229">réponse de Hello est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="dc26d-229">hello response is similar toohello following example:</span></span>
   
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
    > <span data-ttu-id="dc26d-230">Hello `href` valeur retournée par cet URI utilise hello une adresse IP interne hello du nœud de cluster.</span><span class="sxs-lookup"><span data-stu-id="dc26d-230">hello `href` value returned by this URI is using hello internal IP address of hello cluster node.</span></span> <span data-ttu-id="dc26d-231">toouse à partir du cluster en dehors de hello, remplacez partie de hello '10.0.0.18:8080' hello nom de domaine complet du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-231">toouse it from outside hello cluster, replace hello \`10.0.0.18:8080' portion with hello FQDN of hello cluster.</span></span> 
    
    <span data-ttu-id="dc26d-232">Hello suivant les commandes récupérer l’état de hello de demande de hello :</span><span class="sxs-lookup"><span data-stu-id="dc26d-232">hello following commands retrieve hello status of hello request:</span></span>

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

    <span data-ttu-id="dc26d-233">Une réponse de `COMPLETED` indique que la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-233">A response of `COMPLETED` indicates that hello request has finished.</span></span>

3. <span data-ttu-id="dc26d-234">Une fois la demande précédente de hello terminée, utilisez hello après toostart hello service.</span><span class="sxs-lookup"><span data-stu-id="dc26d-234">Once hello previous request completes, use hello following toostart hello service.</span></span>
   
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
    <span data-ttu-id="dc26d-235">service de Hello utilise maintenant la configuration de nouveau hello.</span><span class="sxs-lookup"><span data-stu-id="dc26d-235">hello service is now using hello new configuration.</span></span>

4. <span data-ttu-id="dc26d-236">Enfin, utilisez hello suivant tooturn désactiver le mode maintenance.</span><span class="sxs-lookup"><span data-stu-id="dc26d-236">Finally, use hello following tooturn off maintenance mode.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="dc26d-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dc26d-237">Next steps</span></span>

<span data-ttu-id="dc26d-238">Pour obtenir une référence complète de hello API REST, consultez [V1 de référence d’API Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="dc26d-238">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

