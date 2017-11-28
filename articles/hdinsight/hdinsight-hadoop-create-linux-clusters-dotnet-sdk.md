---
title: "aaaCreate Hadoop clusters à l’aide de .NET - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toocreate Hadoop, HBase, tempête ou Spark clusters sur Linux pour l’utilisation de HDInsight hello HDInsight .NET SDK."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9c74e3dc-837f-4c90-bbb1-489bc7124a3d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: 9460b0d27143c97860b3540fcec26851d755aa28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-net-sdk"></a><span data-ttu-id="d98d7-103">Créer des clusters basés sur Linux dans HDInsight à l’aide de hello .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d98d7-103">Create Linux-based clusters in HDInsight using hello .NET SDK</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]


<span data-ttu-id="d98d7-104">Découvrez comment toocreate un cluster Hadoop dans l’aide de cluster Azure HDInsight hello du SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="d98d7-104">Learn how toocreate a Hadoop cluster in Azure HDInsight cluster using hello .NET SDK.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d98d7-105">étapes Hello dans ce document créent un cluster avec un nœud d’un travail.</span><span class="sxs-lookup"><span data-stu-id="d98d7-105">hello steps in this document create a cluster with one worker node.</span></span> <span data-ttu-id="d98d7-106">Si vous prévoyez plus de 32 nœuds de travail, à la création du cluster ou par mise à l’échelle de cluster de hello après sa création, vous devez tooselect une taille de nœud principal avec au moins 8 cœurs et 14 Go de ram.</span><span class="sxs-lookup"><span data-stu-id="d98d7-106">If you plan on more than 32 worker nodes, either at cluster creation or by scaling hello cluster after creation, you need tooselect a head node size with at least 8 cores and 14GB ram.</span></span>
>
> <span data-ttu-id="d98d7-107">Pour plus d’informations sur les tailles de nœud et les coûts associés, consultez [Tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d98d7-107">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d98d7-108">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="d98d7-108">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="d98d7-109">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="d98d7-109">**An Azure subscription**.</span></span> <span data-ttu-id="d98d7-110">Consultez [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d98d7-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="d98d7-111">**Un compte de stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="d98d7-111">**An Azure storage account**.</span></span> <span data-ttu-id="d98d7-112">Voir [Créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d98d7-112">See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="d98d7-113">**Visual Studio 2013, Visual Studio 2015 ou Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="d98d7-113">**Visual Studio 2013, Visual Studio 2015 or Visual Studio 2017**.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="d98d7-114">Créer des clusters</span><span class="sxs-lookup"><span data-stu-id="d98d7-114">Create clusters</span></span>

1. <span data-ttu-id="d98d7-115">Ouvrez Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d98d7-115">Open Visual Studio 2017.</span></span>
2. <span data-ttu-id="d98d7-116">Créez une application console Visual C#.</span><span class="sxs-lookup"><span data-stu-id="d98d7-116">Create a new Visual C# console application.</span></span>
3. <span data-ttu-id="d98d7-117">À partir de hello **outils** menu, cliquez sur **Gestionnaire de Package NuGet**, puis cliquez sur **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="d98d7-117">From hello **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
4. <span data-ttu-id="d98d7-118">Exécutez hello commande dans les packages de hello hello console tooinstall suivante :</span><span class="sxs-lookup"><span data-stu-id="d98d7-118">Run hello following command in hello console tooinstall hello packages:</span></span>

    ```powershell
    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight
    ```

    <span data-ttu-id="d98d7-119">Ces commandes ajoutent .NET bibliothèques et les références toothem toohello projet Visual Studio actuel.</span><span class="sxs-lookup"><span data-stu-id="d98d7-119">These commands add .NET libraries and references toothem toohello current Visual Studio project.</span></span>
5. <span data-ttu-id="d98d7-120">Dans l’Explorateur de solutions, double-cliquez sur **Program.cs** tooopen, collez hello suivant de code et fournir des valeurs pour les variables de hello :</span><span class="sxs-lookup"><span data-stu-id="d98d7-120">From Solution Explorer, double-click **Program.cs** tooopen it, paste hello following code, and provide values for hello variables:</span></span>

    ```csharp
    using System;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    namespace CreateHDInsightCluster
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;

            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            private const string ExistingResourceGroupName = "<Enter Resource Group Name>";
            private const string ExistingStorageName = "<Enter Default Storage Account Name>.blob.core.windows.net";
            private const string ExistingStorageKey = "<Enter Default Storage Account Key>";
            private const string ExistingBlobContainer = "<Enter Default Bob Container Name>";

            private const string NewClusterName = "<Enter HDInsight Cluster Name>";
            private const int NewClusterNumNodes = 2;
            private const string NewClusterLocation = "EAST US 2";     // Must be hello same as hello default Storage account
            private const OSType NewClusterOSType = OSType.Linux;
            private const string NewClusterType = "Hadoop";
            private const string NewClusterVersion = "3.5";
            private const string NewClusterUsername = "admin";
            private const string NewClusterPassword = "<Enter HTTP User Password>";
            private const string NewClusterSshUserName = "sshuser";

            // You can use eitehr password or public key. See https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix
            private const string NewClusterSshPassword = "<Enter SSH User Password>";
            private const string NewClusterSshPublicKey = @"---- BEGIN SSH2 PUBLIC KEY ----
                Comment: ""rsa-key-20150731""
                AAAAB3NzaC1yc2EAAAABJQAAAQEA4QiCRLqT7fnmUA5OhYWZNlZo6lLaY1c+IRsp
                gmPCsJVGQLu6O1wqcxRqiKk7keYq8bP5s30v6bIljsLZYTnyReNUa5LtFw7eauGr
                yVt3Pve6ejfWELhbVpi0iq8uJNFA9VvRkz8IP1JmjC5jsdnJhzQZtgkIrdn3w0e6
                WVfu15kKyY8YAiynVbdV51EB0SZaSLdMZkZQ81xi4DDtCZD7qvdtWEFwLa+EHdkd
                pzO36Mtev5XvseLQqzXzZ6aVBdlXoppGHXkoGHAMNOtEWRXpAUtEccjpATsaZhQR
                zZdZlzHduhM10ofS4YOYBADt9JohporbQVHM5w6qUhIgyiPo7w==
                ---- END SSH2 PUBLIC KEY ----"; //replace hello public key with your own

            static void Main(string[] args)
            {
                System.Console.WriteLine("Creating a cluster.  hello process takes 10 too20 minutes ...");

                // Authenticate and get a token
                var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // Set parameters for hello new cluster
                var parameters = new ClusterCreateParameters
                {
                    ClusterSizeInNodes = NewClusterNumNodes,
                    UserName = NewClusterUsername,
                    ClusterType = NewClusterType,
                    OSType = NewClusterOSType,
                    Version = NewClusterVersion,

                    // Use an Azure storage account as hello default storage
                    DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingBlobContainer),

                    // Is hello cluster type RServer? If so, you can set hello EdgeNodeSize.
                    // Otherwise, hello default VM size is used.
                    //EdgeNodeSize = "Standard_D12_v2",

                    Password = NewClusterPassword,
                    Location = NewClusterLocation,

                    SshUserName = NewClusterSshUserName,
                    SshPassword = NewClusterSshPassword,
                    //SshPublicKey = NewClusterSshPublicKey
                };

                // Is hello cluster type RServer? If so, add hello RStudio configuration option.
                /*
                parameters.Configurations.Add(
                    "rserver",
                    new Dictionary<string, string>()
                    {
                        { "rstudio", "true" }
                    }
                );
                */

                // Create hello cluster
                _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, parameters);

                System.Console.WriteLine("hello cluster has been created. Press ENTER toocontinue ...");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate tooan Azure subscription and retrieve an authentication token
            /// </summary>
            static TokenCloudCredentials GetTokenCloudCredentials(string TenantId, string ClientId, string SubscriptionId)
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
    ```

6. <span data-ttu-id="d98d7-121">Remplacez les valeurs de membre de classe hello.</span><span class="sxs-lookup"><span data-stu-id="d98d7-121">Replace hello class member values.</span></span>
7. <span data-ttu-id="d98d7-122">Appuyez sur **F5** application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="d98d7-122">Press **F5** toorun hello application.</span></span> <span data-ttu-id="d98d7-123">Une fenêtre de console doit ouvrir et afficher l’état de hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="d98d7-123">A console window should open and display hello status of hello application.</span></span> <span data-ttu-id="d98d7-124">Vous est demandée tooenter vos informations d’identification de compte Azure.</span><span class="sxs-lookup"><span data-stu-id="d98d7-124">You are prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="d98d7-125">Il peut prendre plusieurs minutes toocreate un cluster HDInsight, normalement environ 15.</span><span class="sxs-lookup"><span data-stu-id="d98d7-125">It can take several minutes toocreate an HDInsight cluster, normally around 15.</span></span>

## <a name="use-bootstrap"></a><span data-ttu-id="d98d7-126">Utilisation de Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d98d7-126">Use bootstrap</span></span>

<span data-ttu-id="d98d7-127">À l’aide des données d’amorçage, vous pouvez configurer les paramètres de l’ajout au cours des créations de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d98d7-127">Using bootstrap, you can configure addition settings during hello cluster creations.</span></span>  <span data-ttu-id="d98d7-128">Pour plus d’informations, consultez [Personnalisation de clusters HDInsight à l’aide de Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).</span><span class="sxs-lookup"><span data-stu-id="d98d7-128">For more information, see [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).</span></span>

<span data-ttu-id="d98d7-129">Modifier l’exemple hello dans [créer des clusters](#create-clusters) tooconfigure un paramètre Hive :</span><span class="sxs-lookup"><span data-stu-id="d98d7-129">Modify hello sample in [Create clusters](#create-clusters) tooconfigure a Hive setting:</span></span>

```csharp
static void Main(string[] args)
{
    System.Console.WriteLine("Creating a cluster.  hello process takes 10 too20 minutes ...");

    // Authenticate and get a token
    var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
    // Flag subscription for HDInsight, if it isn't already.
    EnableHDInsight(authToken);
    // Get an HDInsight management client
    _hdiManagementClient = new HDInsightManagementClient(authToken);

    // Set parameters for hello new cluster
    var extendedParameters = new ClusterCreateParametersExtended
    {
        Location = NewClusterLocation,
        Properties = new ClusterCreateProperties
        {
            ClusterDefinition = new ClusterDefinition
            {
                ClusterType = NewClusterType.ToString()
            },
            ClusterVersion = NewClusterVersion,
            OperatingSystemType = NewClusterOSType
        }
    };

    var coreConfigs = new Dictionary<string, string>
    {
        {"fs.defaultFS", string.Format("wasb://{0}@{1}", ExistingBlobContainer, ExistingStorageName)},
        {
            string.Format("fs.azure.account.key.{0}", ExistingStorageName),
            ExistingStorageKey
        }
    };

    // bootstrap
    var hiveConfigs = new Dictionary<string, string>
    {
        { "hive.metastore.client.socket.timeout", "90"}
    };

    var gatewayConfigs = new Dictionary<string, string>
    {
        {"restAuthCredential.isEnabled", "true"},
        {"restAuthCredential.username", NewClusterUsername},
        {"restAuthCredential.password", NewClusterPassword}
    };

    var configurations = new Dictionary<string, Dictionary<string, string>>
    {
        {"core-site", coreConfigs},
        {"gateway", gatewayConfigs},
        {"hive-site", hiveConfigs}
    };

    var serializedConfig = JsonConvert.SerializeObject(configurations);
    extendedParameters.Properties.ClusterDefinition.Configurations = serializedConfig;

    var sshPublicKeys = new List<SshPublicKey>();
    var sshPublicKey = new SshPublicKey
    {
        CertificateData =
            string.Format("ssh-rsa {0}", NewClusterSshPublicKey)
    };
    sshPublicKeys.Add(sshPublicKey);

    var headNode = new Role
    {
        Name = "headnode",
        TargetInstanceCount = 2,
        HardwareProfile = new HardwareProfile
        {
            VmSize = "Large"
        },
        OsProfile = new OsProfile
        {
            LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
            {
                UserName = NewClusterSshUserName,
                Password = NewClusterSshPassword //,
                // When use a SSH pulbic key, make sure tooremove comments, headers and trailers, and concatenate hello key into one line 
                //SshProfile = new SshProfile
                //{
                //    SshPublicKeys = sshPublicKeys
                //}
            }
        }
    };

    var workerNode = new Role
    {
        Name = "workernode",
        TargetInstanceCount = NewClusterNumNodes,
        HardwareProfile = new HardwareProfile
        {
            VmSize = "Large"
        },
        OsProfile = new OsProfile
        {
            LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
            {
                UserName = NewClusterSshUserName,
                Password = NewClusterSshPassword //,
                //SshProfile = new SshProfile
                //{
                //    SshPublicKeys = sshPublicKeys
                //}
            }
        }
    };

    extendedParameters.Properties.ComputeProfile = new ComputeProfile();
    extendedParameters.Properties.ComputeProfile.Roles.Add(headNode);
    extendedParameters.Properties.ComputeProfile.Roles.Add(workerNode);

    _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, extendedParameters);

    System.Console.WriteLine("hello cluster has been created. Press ENTER toocontinue ...");
    System.Console.ReadLine();
}
```

## <a name="use-script-action"></a><span data-ttu-id="d98d7-130">Utilisation d'une action de script</span><span class="sxs-lookup"><span data-stu-id="d98d7-130">Use Script Action</span></span>

<span data-ttu-id="d98d7-131">Une action de script vous permet de configurer d'autres paramètres lors de la création d'un cluster.</span><span class="sxs-lookup"><span data-stu-id="d98d7-131">Using Script Action, you can configure additional settings during cluster creations.</span></span>  <span data-ttu-id="d98d7-132">Pour plus d’informations, consultez la page [Personnaliser des clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d98d7-132">For more information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="d98d7-133">Modifier l’exemple hello dans [créer des clusters](#create-clusters) toocall un tooinstall d’Action de Script r :</span><span class="sxs-lookup"><span data-stu-id="d98d7-133">Modify hello sample in [Create clusters](#create-clusters) toocall a Script Action tooinstall R:</span></span>

```csharp
static void Main(string[] args)
{
    System.Console.WriteLine("Creating a cluster.  hello process takes 10 too20 minutes ...");

    // Authenticate and get a token
    var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
    // Flag subscription for HDInsight, if it isn't already.
    EnableHDInsight(authToken);
    // Get an HDInsight management client
    _hdiManagementClient = new HDInsightManagementClient(authToken);

    // Set parameters for hello new cluster
    var parameters = new ClusterCreateParameters
    {
        ClusterSizeInNodes = NewClusterNumNodes,
        Location = NewClusterLocation,
        ClusterType = NewClusterType,
        OSType = NewClusterOSType,
        Version = NewClusterVersion,

        DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingBlobContainer),

        UserName = NewClusterUsername,
        Password = NewClusterPassword,
        SshUserName = NewClusterSshUserName,
        SshPublicKey = NewClusterSshPublicKey
    };

    ScriptAction rScriptAction = new ScriptAction("Install R",
        new Uri("https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh"), "");

    parameters.ScriptActions.Add(ClusterNodeType.HeadNode,new System.Collections.Generic.List<ScriptAction> { rScriptAction});
    parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { rScriptAction });

    _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, parameters);

    System.Console.WriteLine("hello cluster has been created. Press ENTER toocontinue ...");
    System.Console.ReadLine();
}
```

## <a name="troubleshoot"></a><span data-ttu-id="d98d7-134">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="d98d7-134">Troubleshoot</span></span>

<span data-ttu-id="d98d7-135">Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="d98d7-135">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d98d7-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d98d7-136">Next steps</span></span>
<span data-ttu-id="d98d7-137">Maintenant que vous avez créé un cluster HDInsight, utilisez hello suivant toolearn comment toowork avec votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d98d7-137">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster.</span></span> 

### <a name="hadoop-clusters"></a><span data-ttu-id="d98d7-138">Clusters Hadoop</span><span class="sxs-lookup"><span data-stu-id="d98d7-138">Hadoop clusters</span></span>
* [<span data-ttu-id="d98d7-139">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="d98d7-139">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d98d7-140">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="d98d7-140">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="d98d7-141">Utilisation de MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="d98d7-141">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="d98d7-142">Clusters HBase</span><span class="sxs-lookup"><span data-stu-id="d98d7-142">HBase clusters</span></span>
* [<span data-ttu-id="d98d7-143">Prise en main de HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d98d7-143">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="d98d7-144">Développement d’applications Java pour HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d98d7-144">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="d98d7-145">Clusters Storm</span><span class="sxs-lookup"><span data-stu-id="d98d7-145">Storm clusters</span></span>
* [<span data-ttu-id="d98d7-146">Développement de topologies Java pour Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d98d7-146">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="d98d7-147">Utilisation de composants Python dans Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d98d7-147">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="d98d7-148">Déploiement et analyse des topologies avec Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d98d7-148">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="d98d7-149">Clusters Spark</span><span class="sxs-lookup"><span data-stu-id="d98d7-149">Spark clusters</span></span>
* [<span data-ttu-id="d98d7-150">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="d98d7-150">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="d98d7-151">Exécution de travaux à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="d98d7-151">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="d98d7-152">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="d98d7-152">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="d98d7-153">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="d98d7-153">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="d98d7-154">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="d98d7-154">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="run-jobs"></a><span data-ttu-id="d98d7-155">Exécuter des tâches</span><span class="sxs-lookup"><span data-stu-id="d98d7-155">Run jobs</span></span>
* [<span data-ttu-id="d98d7-156">Exécuter des tâches Hive dans HDInsight avec le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="d98d7-156">Run Hive jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [<span data-ttu-id="d98d7-157">Exécuter des tâches Pig dans HDInsight avec le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="d98d7-157">Run Pig jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md)
* [<span data-ttu-id="d98d7-158">Exécuter des tâches Sqoop dans HDInsight avec le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="d98d7-158">Run Sqoop jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)
* [<span data-ttu-id="d98d7-159">Exécuter des tâches Oozie dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="d98d7-159">Run Oozie jobs in HDInsight</span></span>](hdinsight-use-oozie.md)

