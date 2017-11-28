---
title: "Gérer les clusters Hadoop dans HDInsight avec le Kit de développement logiciel (SDK) .NET - Azure | Microsoft Docs"
description: "Découvrez comment effectuer des tâches d’administration pour les clusters Hadoop dans HDInsight au moyen du Kit de développement logiciel (SDK) .NET HDInsight."
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
ms.openlocfilehash: c10471425fa1202ddb7fe35d0adf4ef33509f268
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="70f3a-103">Gestion des clusters Hadoop dans HDInsight au moyen du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="70f3a-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="70f3a-104">Apprenez à gérer des clusters HDInsight à l’aide du [Kit de développement logiciel (SDK) HDInsight.NET](https://msdn.microsoft.com/library/mt271028.aspx)</span><span class="sxs-lookup"><span data-stu-id="70f3a-104">Learn how to manage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="70f3a-105">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="70f3a-105">**Prerequisites**</span></span>

<span data-ttu-id="70f3a-106">Avant de commencer cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="70f3a-106">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="70f3a-107">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="70f3a-107">**An Azure subscription**.</span></span> <span data-ttu-id="70f3a-108">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="70f3a-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-to-azure-hdinsight"></a><span data-ttu-id="70f3a-109">Se connecter à Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="70f3a-109">Connect to Azure HDInsight</span></span>

<span data-ttu-id="70f3a-110">Les packages Nuget suivants doivent être installés :</span><span class="sxs-lookup"><span data-stu-id="70f3a-110">You need the following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="70f3a-111">L’exemple de code suivant montre comment vous connecter à Azure avant que vous puissiez gérer les clusters HDInsight dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="70f3a-111">The following code sample shows you how to connect to Azure before you can administer HDInsight clusters under your Azure subscription.</span></span>

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
            // This is the GUID for the PowerShell client. Used for interactive logins in this example.
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

                System.Console.WriteLine("Press ENTER to continue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate to an Azure subscription and retrieve an authentication token
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
                // Create a client for the Resource manager and set the subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register the HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

<span data-ttu-id="70f3a-112">Vous devriez voir une invite de commandes lorsque vous exécutez ce programme.</span><span class="sxs-lookup"><span data-stu-id="70f3a-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="70f3a-113">Si vous ne voulez pas que l’invite s’affiche, consultez [Créer des applications .NET HDInsight d’authentification non interactive](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="70f3a-113">If you don't want to see the prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="70f3a-114">Créer des clusters</span><span class="sxs-lookup"><span data-stu-id="70f3a-114">Create clusters</span></span>
<span data-ttu-id="70f3a-115">Consultez [Créer des clusters basés sur Linux dans HDInsight à l’aide du Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="70f3a-115">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="70f3a-116">Énumérer les clusters</span><span class="sxs-lookup"><span data-stu-id="70f3a-116">List clusters</span></span>
<span data-ttu-id="70f3a-117">L’extrait de code suivant répertorie les clusters et certaines propriétés :</span><span class="sxs-lookup"><span data-stu-id="70f3a-117">The following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="70f3a-118">Suppression des clusters</span><span class="sxs-lookup"><span data-stu-id="70f3a-118">Delete clusters</span></span>
<span data-ttu-id="70f3a-119">Pour supprimer un cluster de façon synchrone ou asynchrone, utilisez l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="70f3a-119">Use the following code snippet to delete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="70f3a-120">Mise à l’échelle des clusters</span><span class="sxs-lookup"><span data-stu-id="70f3a-120">Scale clusters</span></span>
<span data-ttu-id="70f3a-121">La fonctionnalité de mise à l’échelle d’un cluster vous permet de modifier le nombre de nœuds de travail utilisés par un cluster exécuté dans Azure HDInsight sans avoir à recréer ce cluster.</span><span class="sxs-lookup"><span data-stu-id="70f3a-121">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="70f3a-122">Seuls les clusters ayant la version 3.1.3 de HDInsight ou une version ultérieure sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="70f3a-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="70f3a-123">Si vous n’êtes pas sûr de la version de votre cluster, vous pouvez consulter la page Propriétés.</span><span class="sxs-lookup"><span data-stu-id="70f3a-123">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="70f3a-124">Voir [Énumération et affichage des clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="70f3a-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="70f3a-125">Impact de la modification du nombre de nœuds de données pour chaque type de cluster pris en charge par HDInsight :</span><span class="sxs-lookup"><span data-stu-id="70f3a-125">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="70f3a-126">Hadoop</span><span class="sxs-lookup"><span data-stu-id="70f3a-126">Hadoop</span></span>
  
    <span data-ttu-id="70f3a-127">Vous pouvez augmenter de façon continue le nombre de nœuds de travail dans un cluster Hadoop exécuté sans affecter aucune tâche en attente ou en cours.</span><span class="sxs-lookup"><span data-stu-id="70f3a-127">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="70f3a-128">De nouvelles tâches peuvent également être soumises lorsque l'opération est en cours.</span><span class="sxs-lookup"><span data-stu-id="70f3a-128">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="70f3a-129">Les défaillances dans l'opération de mise à l'échelle sont correctement gérées de sorte que le cluster reste toujours fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="70f3a-129">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="70f3a-130">Lorsqu’un cluster Hadoop est diminué par la réduction du nombre de nœuds de données, certains services du cluster sont redémarrés.</span><span class="sxs-lookup"><span data-stu-id="70f3a-130">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="70f3a-131">Pour cette raison, toutes les tâches en cours ou en attente échouent lors de la réalisation de l'opération de mise à l'échelle.</span><span class="sxs-lookup"><span data-stu-id="70f3a-131">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="70f3a-132">Toutefois, vous pouvez soumettre à nouveau les tâches une fois l'opération terminée.</span><span class="sxs-lookup"><span data-stu-id="70f3a-132">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="70f3a-133">HBase</span><span class="sxs-lookup"><span data-stu-id="70f3a-133">HBase</span></span>
  
    <span data-ttu-id="70f3a-134">Vous pouvez ajouter ou supprimer des nœuds en continu dans votre cluster HBase lorsque celui-ci s’exécute.</span><span class="sxs-lookup"><span data-stu-id="70f3a-134">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="70f3a-135">Les serveurs régionaux sont équilibrés automatiquement quelques minutes après la fin de l’opération de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="70f3a-135">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="70f3a-136">Cependant, vous pouvez équilibrer manuellement des serveurs régionaux en vous connectant au nœud principal du cluster et en exécutant les commandes suivantes à partir d’une fenêtre d’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="70f3a-136">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="70f3a-137">Storm</span><span class="sxs-lookup"><span data-stu-id="70f3a-137">Storm</span></span>
  
    <span data-ttu-id="70f3a-138">Vous pouvez ajouter ou supprimer des nœuds de données en continu dans votre cluster Storm lorsque celui-ci s'exécute.</span><span class="sxs-lookup"><span data-stu-id="70f3a-138">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="70f3a-139">Mais une fois l’opération de mise à l’échelle terminée avec succès, vous devrez rééquilibrer la topologie.</span><span class="sxs-lookup"><span data-stu-id="70f3a-139">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>
  
    <span data-ttu-id="70f3a-140">Cela peut se faire de deux façons à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="70f3a-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="70f3a-141">l'interface utilisateur Web de Storm</span><span class="sxs-lookup"><span data-stu-id="70f3a-141">Storm web UI</span></span>
  * <span data-ttu-id="70f3a-142">l’outil d’interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="70f3a-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="70f3a-143">Pour plus d’informations, consultez la documentation [Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) .</span><span class="sxs-lookup"><span data-stu-id="70f3a-143">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="70f3a-144">L’interface utilisateur web de Storm est disponible dans le cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="70f3a-144">The Storm web UI is available on the HDInsight cluster:</span></span>
    
    ![Rééquilibrage de mise à l’échelle HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="70f3a-146">Voici un exemple relatif à l'utilisation de la commande de l'interface en ligne de commande pour rééquilibrer la topologie Storm :</span><span class="sxs-lookup"><span data-stu-id="70f3a-146">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>
    
        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="70f3a-147">Pour redimensionner un cluster de façon synchrone ou asynchrone, utilisez l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="70f3a-147">The following code snippet shows how to resize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="70f3a-148">Octroyer/Révoquer l’accès</span><span class="sxs-lookup"><span data-stu-id="70f3a-148">Grant/revoke access</span></span>
<span data-ttu-id="70f3a-149">Les clusters HDInsight disposent des services web HTTP suivants (tous ces services ont des points de terminaison RESTful) :</span><span class="sxs-lookup"><span data-stu-id="70f3a-149">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="70f3a-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="70f3a-150">ODBC</span></span>
* <span data-ttu-id="70f3a-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="70f3a-151">JDBC</span></span>
* <span data-ttu-id="70f3a-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="70f3a-152">Ambari</span></span>
* <span data-ttu-id="70f3a-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="70f3a-153">Oozie</span></span>
* <span data-ttu-id="70f3a-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="70f3a-154">Templeton</span></span>

<span data-ttu-id="70f3a-155">Par défaut, l'accès à ces services est octroyé.</span><span class="sxs-lookup"><span data-stu-id="70f3a-155">By default, these services are granted for access.</span></span> <span data-ttu-id="70f3a-156">Vous avez la possibilité de supprimer/octroyer l'accès.</span><span class="sxs-lookup"><span data-stu-id="70f3a-156">You can revoke/grant the access.</span></span> <span data-ttu-id="70f3a-157">Pour révoquer :</span><span class="sxs-lookup"><span data-stu-id="70f3a-157">To revoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="70f3a-158">Pour octroyer :</span><span class="sxs-lookup"><span data-stu-id="70f3a-158">To grant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="70f3a-159">En octroyant/révoquant l’accès, vous réinitialisez le nom d’utilisateur et le mot de passe du cluster.</span><span class="sxs-lookup"><span data-stu-id="70f3a-159">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="70f3a-160">Vous pouvez également le faire via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="70f3a-160">This can also be done via the Portal.</span></span> <span data-ttu-id="70f3a-161">Consultez [Administration de HDInsight à l’aide du portail Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="70f3a-161">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="70f3a-162">Mettre à jour les informations d’identification de l’utilisateur HTTP</span><span class="sxs-lookup"><span data-stu-id="70f3a-162">Update HTTP user credentials</span></span>
<span data-ttu-id="70f3a-163">Il s’agit de la même procédure que [l’octroi et la révocation de l’accès HTTP](#grant/revoke-access). Si l’accès HTTP a été octroyé au cluster, vous devez tout d’abord le révoquer.</span><span class="sxs-lookup"><span data-stu-id="70f3a-163">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="70f3a-164">Octroyez ensuite l’accès avec les informations d’identification de l’utilisateur HTTP.</span><span class="sxs-lookup"><span data-stu-id="70f3a-164">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="70f3a-165">Trouvez le compte de stockage par défaut</span><span class="sxs-lookup"><span data-stu-id="70f3a-165">Find the default storage account</span></span>
<span data-ttu-id="70f3a-166">L’extrait de code suivant montre comment obtenir le nom de compte de stockage par défaut et la clé de compte de stockage par défaut pour un cluster.</span><span class="sxs-lookup"><span data-stu-id="70f3a-166">The following code snippet demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="70f3a-167">Soumettre les travaux</span><span class="sxs-lookup"><span data-stu-id="70f3a-167">Submit jobs</span></span>
<span data-ttu-id="70f3a-168">**Pour envoyer des tâches MapReduce**</span><span class="sxs-lookup"><span data-stu-id="70f3a-168">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="70f3a-169">Consultez [Exécution des exemples Hadoop MapReduce dans HDInsight](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="70f3a-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="70f3a-170">**Pour envoyer des tâches Hive**</span><span class="sxs-lookup"><span data-stu-id="70f3a-170">**To submit Hive jobs**</span></span> 

<span data-ttu-id="70f3a-171">Consultez [Exécution de requêtes Hive avec le Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="70f3a-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="70f3a-172">**Pour envoyer des tâches Pig**</span><span class="sxs-lookup"><span data-stu-id="70f3a-172">**To submit Pig jobs**</span></span>

<span data-ttu-id="70f3a-173">Consultez [Exécution de tâches Pig avec le Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="70f3a-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="70f3a-174">**Pour envoyer des tâches Sqoop**</span><span class="sxs-lookup"><span data-stu-id="70f3a-174">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="70f3a-175">Consultez l'article [Utilisation de Sqoop avec HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="70f3a-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="70f3a-176">**Pour envoyer des tâches Oozie**</span><span class="sxs-lookup"><span data-stu-id="70f3a-176">**To submit Oozie jobs**</span></span>

<span data-ttu-id="70f3a-177">Consultez [Utilisation d’Oozie avec Hadoop pour définir et exécuter un workflow dans HDInsight](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="70f3a-177">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="70f3a-178">Téléchargement de données vers le stockage d'objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="70f3a-178">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="70f3a-179">Consultez la rubrique [Téléchargement de données vers HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="70f3a-179">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="70f3a-180">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="70f3a-180">See Also</span></span>
* [<span data-ttu-id="70f3a-181">Documentation de référence sur le Kit de développement logiciel (SDK) .NET HDInsight</span><span class="sxs-lookup"><span data-stu-id="70f3a-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="70f3a-182">[Administration de HDInsight à l’aide du portail Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="70f3a-182">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="70f3a-183">[Administration de HDInsight à l’aide de l’interface de ligne de commande][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="70f3a-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="70f3a-184">[Création de clusters HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="70f3a-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="70f3a-185">[Téléchargement de données vers HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="70f3a-185">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="70f3a-186">[Prise en main d’Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="70f3a-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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


