---
title: "à l’aide de Clusters HDInsight aaaCustomize script actions - Azure | Documents Microsoft"
description: "Découvrez comment toocustomize HDInsight clusters à l’aide d’Action de Script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a>Personnalisation de clusters HDInsight basés sur Windows à l'aide d'une action de script
**Action de script** peut être utilisé tooinvoke [des scripts personnalisés](hdinsight-hadoop-script-actions.md) pendant le processus de création de cluster hello pour l’installation des logiciels supplémentaires sur un cluster.

informations de Hello dans cet article sont des clusters HDInsight tooWindows spécifiques. Pour les clusters Linux, consultez la page [Personnaliser des clusters HDInsight Linux à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Clusters HDInsight peuvent être personnalisés de plusieurs autres façons, notamment d’autres comptes de stockage Azure, la modification hello Hadoop (core-site.XML, hive-site.XML, etc.) des fichiers de configuration ou ajout de bibliothèques (par exemple, Hive, Oozie) partagées dans emplacements courants dans un cluster de hello. Ces personnalisations peuvent être effectuées dans Azure PowerShell, hello Azure HDInsight .NET SDK, ou hello portail Azure. Pour plus d’informations, consultez [Création de clusters Hadoop dans HDInsight][hdinsight-provision-cluster].

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a>Action de script dans le processus de création de cluster hello
Action de script est utilisée uniquement lorsqu’un cluster est en processus hello d’en cours de création. Hello diagramme ci-dessous illustre lors de l’Action de Script est exécutée pendant le processus de création de hello :

![Personnalisation du cluster HDInsight et procédure de création d’un cluster][img-hdi-cluster-states]

Lors de l’exécution du script hello, cluster de hello passe hello **ClusterCustomization** étape. À ce stade, hello script est exécuté sous un compte d’administrateur système hello, en parallèle sur tous les hello spécifié des nœuds de cluster de hello et fournit des privilèges d’administrateur complets sur les nœuds hello.

> [!NOTE]
> Étant donné que vous disposez des privilèges d’administrateur sur les nœuds de cluster hello lors de la **ClusterCustomization** étape, vous pouvez utiliser hello script tooperform des opérations telles que l’arrêt et démarrage des services, y compris les services liés à Hadoop. Ainsi, dans le cadre du script de hello, vous devez vous assurer que hello Ambari services et autres services Hadoop sont en cours d’exécution avant la fin de script de hello en cours d’exécution. Ces services sont requis toosuccessfully vérifier l’intégrité de hello et l’état du cluster de hello lors de sa création. Si vous changez de configuration sur le cluster qui a une incidence sur ces services, vous devez utiliser les fonctions d’assistance hello fournis. Pour plus d’informations sur les fonctions d’assistance, consultez [Développer des scripts d’action de script pour HDInsight][hdinsight-write-script].
>
>

sortie de Hello et journaux d’erreurs hello pour le script de hello sont stockés dans le compte de stockage par défaut hello que vous avez spécifié pour le cluster de hello. Hello journaux sont stockés dans une table avec le nom de hello **u < \cluster-name-fragment >< \time-stamp > setuplog**. Il s’agit de journaux d’agrégation à partir du script hello s’exécutent sur tous les nœuds hello (nœud principal et nœuds de travail) dans le cluster de hello.

Chaque cluster peut accepter plusieurs actions de script qui sont appelées dans l’ordre de hello dans lequel elles sont spécifiées. Un script peut être exécuté sur le nœud principal de hello, nœuds de travail hello ou les deux.

HDInsight fournit plusieurs hello tooinstall de scripts suivant des composants de clusters HDInsight :

| Nom | Script |
| --- | --- |
| **Installation de Spark** |https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1. Consultez [Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark]. |
| **Installation de R** |https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1. Consultez [Installer et utiliser R sur les clusters HDInsight][hdinsight-install-r]. |
| **Installation de Solr** |https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1. Consultez [Installer et utiliser Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install.md). |
| - **Installation de Giraph** |https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1. Consultez [Installer et utiliser Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install.md). |
| **Précharger les bibliothèques Hive** |https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1. Consultez [Ajouter des bibliothèques Hive sur des clusters HDInsight](hdinsight-hadoop-add-hive-libraries.md) |

## <a name="call-scripts-using-hello-azure-portal"></a>Appeler des scripts à l’aide de hello portail Azure
**À partir de hello portail Azure**

1. Démarrez la création d'un cluster comme décrit dans [Création de clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
2. Sous Configuration facultative, pourquoi **Actions de Script** panneau, cliquez sur **ajouter une action de script** tooprovide des détails sur l’action de script hello, comme indiqué ci-dessous :

    ![Utilisez l’Action de Script toocustomize un cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "toocustomize d’Action de Script d’utiliser un cluster")

    <table border='1'>
        <tr><th>Propriété</th><th>Valeur</th></tr>
        <tr><td>Nom</td>
            <td>Spécifiez un nom pour l’action de script hello.</td></tr>
        <tr><td>URI du script</td>
            <td>Spécifiez hello URI toohello script qui est appelée toocustomize hello cluster. s</td></tr>
        <tr><td>Head/Worker</td>
            <td>Spécifier les nœuds hello (**Head** ou **travail**) sur la personnalisation hello script est exécuté.</b>.
        <tr><td>Paramètres</td>
            <td>Spécifiez des paramètres de hello, si requis par le script de hello.</td></tr>
    </table>

    Appuyez sur entrée tooadd plus de script action tooinstall plusieurs composants de cluster de hello.
3. Cliquez sur **sélectionnez** toosave hello configuration des actions de script et poursuivre la création du cluster.

## <a name="call-scripts-using-azure-powershell"></a>Appel de scripts à l’aide d’Azure PowerShell
Ce script PowerShell suivant montre comment tooinstall Spark sur Windows en fonction de cluster HDInsight.  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


tooinstall autres logiciels, vous devez tooreplace fichier de script hello dans le script de hello :

Lorsque vous y êtes invité, entrez les informations d’identification de l’hello pour le cluster de hello. Il peut prendre plusieurs minutes avant que le cluster de hello est créé.

## <a name="call-scripts-using-net-sdk"></a>Appel de scripts à l'aide du Kit de développement logiciel (SDK) .NET
Hello exemple suivant montre comment tooinstall Spark sur Windows en fonction de cluster HDInsight. tooinstall autres logiciels, vous devez tooreplace fichier de script hello dans le code hello.

**toocreate un cluster HDInsight avec Spark**

1. Créez une application console C# dans Visual Studio.
2. À partir de la Console du Gestionnaire de Package Nuget de hello, exécutez hello commande suivante.

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. Hello utilisation suivant à l’aide des instructions dans le fichier Program.cs de hello :

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. Placez le code de hello dans la classe hello avec les éléments suivants de hello :

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
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
5. Appuyez sur **F5** application hello de toorun.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Prise en charge des logiciels open source utilisés sur les clusters HDInsight
Hello service Microsoft Azure HDInsight est une plate-forme flexible qui vous permet de toobuild des applications de données volumineuses dans le cloud de hello à l’aide d’un écosystème de technologies open source sur Hadoop. Microsoft Azure offre un niveau général de la prise en charge pour les technologies open source, comme indiqué dans hello **prennent en charge l’étendue** section Hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">site Web du Forum aux questions sur Azure prend en charge</a>. Hello service HDInsight fournit un niveau supplémentaire de prise en charge de certains composants de hello, comme décrit ci-dessous.

Il existe deux types de composants open source qui sont disponibles dans hello service HDInsight :

* **Les composants intégrés** -ces composants sont déjà installés sur les clusters HDInsight et fournir des fonctionnalités principales du cluster de hello. Par exemple, fils ResourceManager, langage de requête Hive hello (HiveQL) et la bibliothèque de Mahout hello appartiennent toothis catégorie. Une liste complète des composants de cluster est disponible dans [quelles sont les nouveautés dans les versions de cluster Hadoop hello fournies par HDInsight ?](hdinsight-component-versioning.md) </a>.
* **Les composants personnalisés** -vous, en tant qu’utilisateur de cluster de hello, pourrez installer ou utiliser dans votre charge de travail n’importe quel composant disponible dans la Communauté de hello ou créée par vous.

Charge entièrement les composants intégrés, et permet de tooisolate et résoudre les problèmes connexes toothese composants de Support technique de Microsoft.

> [!WARNING]
> Les composants fournis avec le cluster HDInsight de hello sont entièrement gérés et permet de tooisolate et résoudre les problèmes connexes toothese composants de Support technique de Microsoft.
>
> Les composants personnalisés de réception efforcera toohelp vous toofurther hello de dépannage. Cela peut entraîner hello de résoudre ou demandant que vous tooengage les canaux disponibles pour hello ouvrir technologies source où se trouve une grande expérience pour cette technologie. Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org) ; par exemple, [Hadoop](http://hadoop.apache.org/) ou [Spark](http://spark.apache.org/).
>
>

Hello service HDInsight propose plusieurs manières toouse des composants personnalisés. Quelle que soit la comment un composant est utilisé ou installé sur le cluster de hello, hello même niveau de prise en charge s’applique. Voici une liste des méthodes les plus courantes de hello que les composants personnalisés peuvent être utilisés sur les clusters HDInsight :

1. Envoi de travaux - Hadoop ou autres types de tâches qui s’exécutent, ou utilisent des composants personnalisés peut être soumis toohello cluster.
2. Personnalisation de cluster - lors de la création du cluster, vous pouvez spécifier des paramètres supplémentaires et des composants personnalisés qui seront installés sur les nœuds de cluster hello.
3. Exemples - pour les composants personnalisés populaires, Microsoft et d’autres peuvent fournir des exemples de la façon dont ces composants peuvent être utilisés sur des clusters HDInsight de hello. Ces exemples sont fournis sans support.

## <a name="develop-script-action-scripts"></a>Développer des scripts d’action de script
Consultez [Développer des scripts d’action de script pour HDInsight][hdinsight-write-script].

## <a name="see-also"></a>Voir aussi
* [Créer des clusters Hadoop dans HDInsight] [ hdinsight-provision-cluster] fournit des instructions sur la façon dont toocreate un HDInsight de cluster à l’aide d’autres options personnalisées.
* [Développer des scripts d’action de script pour HDInsight][hdinsight-write-script]
* [Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark]
* [Installer et utiliser R sur les clusters HDInsight][hdinsight-install-r]
* [Installer et utiliser Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install.md)
* [Installez et utilisez Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install.md).

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Procédure de création d’un cluster"
