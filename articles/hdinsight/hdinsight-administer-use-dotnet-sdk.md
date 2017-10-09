---
title: "les clusters aaaManage Hadoop dans HDInsight avec le Kit de développement .NET - Azure | Documents Microsoft"
description: "Découvrez comment tooperform administration tâches pour hello clusters Hadoop dans HDInsight à l’aide du Kit de développement logiciel HDInsight .NET."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: fd134765-c2a0-488a-bca6-184d814d78e9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d8bbf966b7eba3e943dfb2f764d15d8e52b9be71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="6e71a-103">Gestion des clusters Hadoop dans HDInsight au moyen du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="6e71a-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="6e71a-104">Découvrez comment toomanage HDInsight clusters à l’aide de [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e71a-104">Learn how toomanage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="6e71a-105">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="6e71a-105">**Prerequisites**</span></span>

<span data-ttu-id="6e71a-106">Avant de commencer cet article, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="6e71a-106">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="6e71a-107">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="6e71a-107">**An Azure subscription**.</span></span> <span data-ttu-id="6e71a-108">Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="6e71a-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-tooazure-hdinsight"></a><span data-ttu-id="6e71a-109">Se connecter tooAzure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6e71a-109">Connect tooAzure HDInsight</span></span>

<span data-ttu-id="6e71a-110">Vous devez hello suivant les packages Nuget :</span><span class="sxs-lookup"><span data-stu-id="6e71a-110">You need hello following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="6e71a-111">Hello exemple de code suivant vous montre comment les clusters tooconnect tooAzure avant de pouvoir administrer HDInsight sous votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6e71a-111">hello following code sample shows you how tooconnect tooAzure before you can administer HDInsight clusters under your Azure subscription.</span></span>

    using System;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;

    namespace HDInsightManagement
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            static void Main(string[] args)
            {
                // Authenticate and get a token
                var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // insert code here

                System.Console.WriteLine("Press ENTER toocontinue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate tooan Azure subscription and retrieve an authentication token
            /// </summary>
            static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
            {
                var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
                var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/", 
                    ClientId, 
                    new Uri("urn:ietf:wg:oauth:2.0:oob"), 
                    PromptBehavior.Always, 
                    UserIdentifier.AnyUser);
                return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
            }
            /// <summary>
            /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
            /// </summary>
            /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
            /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
            /// <param name="authToken">An authentication token for your Azure subscription</param>
            static void EnableHDInsight(TokenCloudCredentials authToken)
            {
                // Create a client for hello Resource manager and set hello subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register hello HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

<span data-ttu-id="6e71a-112">Vous devriez voir une invite de commandes lorsque vous exécutez ce programme.</span><span class="sxs-lookup"><span data-stu-id="6e71a-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="6e71a-113">Si vous ne souhaitez pas invite de commandes toosee hello, consultez [créer une authentification non interactive les applications .NET HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="6e71a-113">If you don't want toosee hello prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="6e71a-114">Créer des clusters</span><span class="sxs-lookup"><span data-stu-id="6e71a-114">Create clusters</span></span>
<span data-ttu-id="6e71a-115">Consultez [basés sur Linux de créer des clusters HDInsight à l’aide hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="6e71a-115">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="6e71a-116">Énumérer les clusters</span><span class="sxs-lookup"><span data-stu-id="6e71a-116">List clusters</span></span>
<span data-ttu-id="6e71a-117">Hello extrait de code suivant répertorie les clusters et certaines propriétés :</span><span class="sxs-lookup"><span data-stu-id="6e71a-117">hello following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="6e71a-118">Suppression des clusters</span><span class="sxs-lookup"><span data-stu-id="6e71a-118">Delete clusters</span></span>
<span data-ttu-id="6e71a-119">Hello suivant extrait de code toodelete un cluster de façon synchrone ou asynchrone, utilisez :</span><span class="sxs-lookup"><span data-stu-id="6e71a-119">Use hello following code snippet toodelete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="6e71a-120">Mise à l’échelle des clusters</span><span class="sxs-lookup"><span data-stu-id="6e71a-120">Scale clusters</span></span>
<span data-ttu-id="6e71a-121">cluster Hello fonctionnalité de mise à l’échelle permet un nombre de hello toochange de nœuds de travail utilisé par un cluster qui s’exécute dans Azure HDInsight sans avoir toore-créer le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6e71a-121">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="6e71a-122">Seuls les clusters ayant la version 3.1.3 de HDInsight ou une version ultérieure sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="6e71a-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="6e71a-123">Si vous ne savez pas de version hello de votre cluster, vous pouvez vérifier la page de propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="6e71a-123">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="6e71a-124">Voir [Énumération et affichage des clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="6e71a-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="6e71a-125">impact Hello modifiant nombre hello de nœuds de données pour chaque type de cluster pris en charge par HDInsight :</span><span class="sxs-lookup"><span data-stu-id="6e71a-125">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="6e71a-126">Hadoop</span><span class="sxs-lookup"><span data-stu-id="6e71a-126">Hadoop</span></span>
  
    <span data-ttu-id="6e71a-127">Vous pouvez augmenter de façon transparente nombre hello de nœuds de travail dans un cluster Hadoop qui est en cours d’exécution sans impact sur toutes les tâches en attente ou en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6e71a-127">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="6e71a-128">Nouvelles tâches peuvent également être soumises pendant que l’opération de hello est en cours.</span><span class="sxs-lookup"><span data-stu-id="6e71a-128">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="6e71a-129">Échecs dans une opération de mise à l’échelle sont correctement gérés afin que hello cluster est toujours conservé dans un état fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="6e71a-129">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="6e71a-130">Lorsqu’un cluster Hadoop est réduite en réduisant le nombre de hello de nœuds de données, certains services hello dans un cluster de hello sont redémarrés.</span><span class="sxs-lookup"><span data-stu-id="6e71a-130">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="6e71a-131">Ainsi, en cours d’exécution et en attente de toofail de travaux à l’achèvement de hello Hello opération de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="6e71a-131">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="6e71a-132">Vous pouvez, toutefois, renvoyer des tâches de hello une fois l’opération hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="6e71a-132">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="6e71a-133">HBase</span><span class="sxs-lookup"><span data-stu-id="6e71a-133">HBase</span></span>
  
    <span data-ttu-id="6e71a-134">Vous pouvez accéder en toute transparence ajouter ou supprimer le cluster de nœuds tooyour HBase pendant son exécution.</span><span class="sxs-lookup"><span data-stu-id="6e71a-134">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="6e71a-135">Serveurs régionaux sont équilibrés automatiquement après quelques minutes d’achèvement hello opération de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="6e71a-135">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="6e71a-136">Toutefois, vous pouvez équilibrer manuellement les serveurs régionaux hello en vous connectant à un nœud principal de hello du cluster et hello en cours d’exécution suivant des commandes dans une fenêtre d’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="6e71a-136">However, you can also manually balance hello regional servers by logging into hello headnode of cluster and running hello following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="6e71a-137">Storm</span><span class="sxs-lookup"><span data-stu-id="6e71a-137">Storm</span></span>
  
    <span data-ttu-id="6e71a-138">Vous pouvez accéder en toute transparence ajouter ou supprimer le cluster de données nœuds tooyour Storm pendant son exécution.</span><span class="sxs-lookup"><span data-stu-id="6e71a-138">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="6e71a-139">Mais après la réussite de l’opération de mise à l’échelle de hello, vous devrez topologie de hello toorebalance.</span><span class="sxs-lookup"><span data-stu-id="6e71a-139">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>
  
    <span data-ttu-id="6e71a-140">Cela peut se faire de deux façons à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="6e71a-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="6e71a-141">l'interface utilisateur Web de Storm</span><span class="sxs-lookup"><span data-stu-id="6e71a-141">Storm web UI</span></span>
  * <span data-ttu-id="6e71a-142">l’outil d’interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="6e71a-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="6e71a-143">Reportez-vous toohello [documentation d’Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="6e71a-143">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="6e71a-144">interface utilisateur web de Storm Hello est disponible sur le cluster HDInsight de hello :</span><span class="sxs-lookup"><span data-stu-id="6e71a-144">hello Storm web UI is available on hello HDInsight cluster:</span></span>
    
    ![Rééquilibrage de mise à l’échelle HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="6e71a-146">Voici un exemple comment toouse hello CLI commande topologie de Storm toorebalance hello :</span><span class="sxs-lookup"><span data-stu-id="6e71a-146">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="6e71a-147">Hello suivant extrait de code montre comment tooresize un cluster de façon synchrone ou asynchrone :</span><span class="sxs-lookup"><span data-stu-id="6e71a-147">hello following code snippet shows how tooresize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="6e71a-148">Octroyer/Révoquer l’accès</span><span class="sxs-lookup"><span data-stu-id="6e71a-148">Grant/revoke access</span></span>
<span data-ttu-id="6e71a-149">Clusters HDInsight ont hello suivant (tous ces services ont des points de terminaison RESTful) des services web HTTP :</span><span class="sxs-lookup"><span data-stu-id="6e71a-149">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="6e71a-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="6e71a-150">ODBC</span></span>
* <span data-ttu-id="6e71a-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="6e71a-151">JDBC</span></span>
* <span data-ttu-id="6e71a-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="6e71a-152">Ambari</span></span>
* <span data-ttu-id="6e71a-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="6e71a-153">Oozie</span></span>
* <span data-ttu-id="6e71a-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="6e71a-154">Templeton</span></span>

<span data-ttu-id="6e71a-155">Par défaut, l'accès à ces services est octroyé.</span><span class="sxs-lookup"><span data-stu-id="6e71a-155">By default, these services are granted for access.</span></span> <span data-ttu-id="6e71a-156">Vous pouvez révoquer ou octroyer l’accès de hello.</span><span class="sxs-lookup"><span data-stu-id="6e71a-156">You can revoke/grant hello access.</span></span> <span data-ttu-id="6e71a-157">toorevoke :</span><span class="sxs-lookup"><span data-stu-id="6e71a-157">toorevoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="6e71a-158">toogrant :</span><span class="sxs-lookup"><span data-stu-id="6e71a-158">toogrant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="6e71a-159">Par attribution/révocation de l’accès hello, vous allez réinitialiser le mot de passe et le nom d’utilisateur de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6e71a-159">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="6e71a-160">Peut également être cela via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="6e71a-160">This can also be done via hello Portal.</span></span> <span data-ttu-id="6e71a-161">Consultez [HDInsight de gérer à l’aide de hello portail Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="6e71a-161">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="6e71a-162">Mettre à jour les informations d’identification de l’utilisateur HTTP</span><span class="sxs-lookup"><span data-stu-id="6e71a-162">Update HTTP user credentials</span></span>
<span data-ttu-id="6e71a-163">Il est même hello procédure en tant que [Grant/revoke HTTP accès](#grant/revoke-access). Si le cluster de hello a été accordée hello accès HTTP, vous devez d’abord la révoquer.</span><span class="sxs-lookup"><span data-stu-id="6e71a-163">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="6e71a-164">Et accorder l’accès hello avec nouvelles informations d’identification utilisateur HTTP.</span><span class="sxs-lookup"><span data-stu-id="6e71a-164">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="6e71a-165">Recherchez le compte de stockage par défaut hello</span><span class="sxs-lookup"><span data-stu-id="6e71a-165">Find hello default storage account</span></span>
<span data-ttu-id="6e71a-166">Hello suivant extrait de code montre comment les tooget hello nom de compte de stockage par défaut et hello clé de compte de stockage par défaut pour un cluster.</span><span class="sxs-lookup"><span data-stu-id="6e71a-166">hello following code snippet demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="6e71a-167">Soumettre les travaux</span><span class="sxs-lookup"><span data-stu-id="6e71a-167">Submit jobs</span></span>
<span data-ttu-id="6e71a-168">**tâches MapReduce toosubmit**</span><span class="sxs-lookup"><span data-stu-id="6e71a-168">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="6e71a-169">Consultez [Exécution des exemples Hadoop MapReduce dans HDInsight](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6e71a-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="6e71a-170">**travaux de ruche toosubmit**</span><span class="sxs-lookup"><span data-stu-id="6e71a-170">**toosubmit Hive jobs**</span></span> 

<span data-ttu-id="6e71a-171">Consultez [Exécution de requêtes Hive avec le Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="6e71a-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="6e71a-172">**travaux de Pig toosubmit**</span><span class="sxs-lookup"><span data-stu-id="6e71a-172">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="6e71a-173">Consultez [Exécution de tâches Pig avec le Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="6e71a-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="6e71a-174">**travaux de Sqoop toosubmit**</span><span class="sxs-lookup"><span data-stu-id="6e71a-174">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="6e71a-175">Consultez l'article [Utilisation de Sqoop avec HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="6e71a-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="6e71a-176">**travaux de Oozie toosubmit**</span><span class="sxs-lookup"><span data-stu-id="6e71a-176">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="6e71a-177">Consultez [Oozie utilisation avec Hadoop toodefine et exécuter un flux de travail dans HDInsight](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="6e71a-177">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="6e71a-178">Télécharger le stockage d’objets Blob de données tooAzure</span><span class="sxs-lookup"><span data-stu-id="6e71a-178">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="6e71a-179">Consultez [télécharger des données tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="6e71a-179">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="6e71a-180">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6e71a-180">See Also</span></span>
* [<span data-ttu-id="6e71a-181">Documentation de référence sur le Kit de développement logiciel (SDK) .NET HDInsight</span><span class="sxs-lookup"><span data-stu-id="6e71a-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="6e71a-182">[Administrer HDInsight à l’aide de hello portail Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="6e71a-182">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="6e71a-183">[Administration de HDInsight à l’aide de l’interface de ligne de commande][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="6e71a-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="6e71a-184">[Création de clusters HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="6e71a-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="6e71a-185">[Télécharger des données tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="6e71a-185">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="6e71a-186">[Prise en main d’Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="6e71a-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


