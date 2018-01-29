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
ms.date: 12/15/2017
ms.author: jgao
ms.openlocfilehash: d881d47e26460d3fff89c01245bba4c608dc8b08
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/18/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a>Gestion des clusters Hadoop dans HDInsight au moyen du Kit de développement logiciel (SDK) .NET
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Apprenez à gérer des clusters HDInsight à l’aide du [Kit de développement logiciel (SDK) HDInsight.NET](https://msdn.microsoft.com/library/mt271028.aspx)

**Composants requis**

Avant de commencer cet article, vous devez disposer des éléments suivants :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="connect-to-azure-hdinsight"></a>Se connecter à Azure HDInsight

Les packages NuGet suivants doivent être installés :

```
Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
Install-Package Microsoft.Azure.Management.ResourceManager -Pre
Install-Package Microsoft.Azure.Management.HDInsight
```

L’exemple de code suivant montre comment vous connecter à Azure avant que vous puissiez gérer les clusters HDInsight dans votre abonnement Azure.

```csharp
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
```

Vous devriez voir une invite de commandes lorsque vous exécutez ce programme.  Si vous ne voulez pas que l’invite s’affiche, consultez [Créer des applications .NET HDInsight d’authentification non interactive](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

## <a name="create-clusters"></a>Créer des clusters
Consultez [Créer des clusters basés sur Linux dans HDInsight à l’aide du Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)

## <a name="list-clusters"></a>Énumérer les clusters
L’extrait de code suivant répertorie les clusters et certaines propriétés :

```csharp
var results = _hdiManagementClient.Clusters.List();
foreach (var name in results.Clusters) {
    Console.WriteLine("Cluster Name: " + name.Name);
    Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
    Console.WriteLine("\t Cluster location: " + name.Location);
    Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
}
```

## <a name="delete-clusters"></a>Suppression des clusters
Pour supprimer un cluster de façon synchrone ou asynchrone, utilisez l’extrait de code suivant : 

```csharp
_hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
_hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");
```

## <a name="scale-clusters"></a>Mise à l’échelle des clusters
La fonctionnalité de mise à l’échelle d’un cluster vous permet de modifier le nombre de nœuds de travail utilisés par un cluster exécuté dans Azure HDInsight sans avoir à recréer ce cluster.

> [!NOTE]
> Seuls les clusters ayant la version 3.1.3 de HDInsight ou une version ultérieure sont pris en charge. Si vous n’êtes pas sûr de la version de votre cluster, vous pouvez consulter la page Propriétés.  Voir [Énumération et affichage des clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
> 
> 

Impact de la modification du nombre de nœuds de données pour chaque type de cluster pris en charge par HDInsight :

* Hadoop
  
    Vous pouvez augmenter de façon continue le nombre de nœuds de travail dans un cluster Hadoop exécuté sans affecter aucune tâche en attente ou en cours. De nouvelles tâches peuvent également être soumises lorsque l'opération est en cours. Les défaillances dans l'opération de mise à l'échelle sont correctement gérées de sorte que le cluster reste toujours fonctionnel.
  
    Lorsqu’un cluster Hadoop est diminué par la réduction du nombre de nœuds de données, certains services du cluster sont redémarrés. Pour cette raison, toutes les tâches en cours ou en attente échouent lors de la réalisation de l'opération de mise à l'échelle. Toutefois, vous pouvez soumettre à nouveau les tâches une fois l'opération terminée.
* hbase
  
    Vous pouvez ajouter ou supprimer des nœuds en continu dans votre cluster HBase lorsque celui-ci s’exécute. Les serveurs régionaux sont équilibrés automatiquement quelques minutes après la fin de l’opération de mise à l’échelle. Cependant, vous pouvez équilibrer manuellement des serveurs régionaux en vous connectant au nœud principal du cluster et en exécutant les commandes suivantes à partir d’une fenêtre d’invite de commandes :
  
    ```bash
    >pushd %HBASE_HOME%\bin
    >hbase shell
    >balancer
    ```
* Storm
  
    Vous pouvez ajouter ou supprimer des nœuds de données en continu dans votre cluster Storm lorsque celui-ci s'exécute. Mais une fois l’opération de mise à l’échelle terminée avec succès, vous devrez rééquilibrer la topologie.
  
    Cela peut se faire de deux façons à l’aide de :
  
  * l'interface utilisateur Web de Storm
  * l’outil d’interface de ligne de commande (CLI)
    
    Pour plus d’informations, consultez la documentation [Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) .
    
    L’interface utilisateur web de Storm est disponible dans le cluster HDInsight :
    
    ![Rééquilibrage de mise à l’échelle HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    Voici un exemple relatif à l'utilisation de la commande de l'interface en ligne de commande pour rééquilibrer la topologie Storm :
    
    ```cli
    ## Reconfigure the topology "mytopology" to use 5 worker processes,
    ## the spout "blue-spout" to use 3 executors, and
    ## the bolt "yellow-bolt" to use 10 executors
    $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10
    ```

Pour redimensionner un cluster de façon synchrone ou asynchrone, utilisez l’extrait de code suivant :

```csharp
_hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
_hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   
```

## <a name="grantrevoke-access"></a>Octroyer/Révoquer l’accès
Les clusters HDInsight disposent des services web HTTP suivants (tous ces services ont des points de terminaison RESTful) :

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Par défaut, l'accès à ces services est octroyé. Vous avez la possibilité de supprimer/octroyer l'accès. Pour révoquer :

```csharp
var httpParams = new HttpSettingsParameters
{
    HttpUserEnabled = false,
    HttpUsername = "admin",
    HttpPassword = "*******",
};
_hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);
```

Pour octroyer :

```csharp
var httpParams = new HttpSettingsParameters
{
    HttpUserEnabled = enable,
    HttpUsername = "admin",
    HttpPassword = "*******",
};
_hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);
```

> [!NOTE]
> En octroyant/révoquant l’accès, vous réinitialisez le nom d’utilisateur et le mot de passe du cluster.
> 
> 

Vous pouvez également le faire via le portail Azure. Consultez [Administration de HDInsight à l’aide du portail Azure][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Mettre à jour les informations d’identification de l’utilisateur HTTP
Il s’agit de la même procédure que [l’octroi et la révocation de l’accès HTTP](#grant/revoke-access). Si l’accès HTTP a été octroyé au cluster, vous devez tout d’abord le révoquer.  Octroyez ensuite l’accès avec les informations d’identification de l’utilisateur HTTP.

## <a name="find-the-default-storage-account"></a>Trouvez le compte de stockage par défaut
L’extrait de code suivant montre comment obtenir le nom de compte de stockage par défaut et la clé de compte de stockage par défaut pour un cluster.

```csharp
var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
foreach (var key in results.Configuration.Keys)
{
    Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
}
```

## <a name="submit-jobs"></a>Soumettre les travaux
**Pour envoyer des tâches MapReduce**

Consultez [Exécution des exemples Hadoop MapReduce dans HDInsight](hadoop/apache-hadoop-run-samples-linux.md).

**Pour envoyer des tâches Hive** 

Consultez [Exécution de requêtes Hive avec le Kit de développement logiciel (SDK) .NET](hadoop/apache-hadoop-use-hive-dotnet-sdk.md).

**Pour envoyer des tâches Pig**

Consultez [Exécution de tâches Pig avec le Kit de développement logiciel (SDK) .NET](hadoop/apache-hadoop-use-pig-dotnet-sdk.md).

**Pour envoyer des tâches Sqoop**

Consultez l'article [Utilisation de Sqoop avec HDInsight](hadoop/apache-hadoop-use-sqoop-dotnet-sdk.md).

**Pour envoyer des tâches Oozie**

Consultez [Utilisation d’Oozie avec Hadoop pour définir et exécuter un workflow dans HDInsight](hdinsight-use-oozie-linux-mac.md).

## <a name="upload-data-to-azure-blob-storage"></a>Téléchargement de données vers le stockage d'objets blob Azure
Consultez la rubrique [Téléchargement de données vers HDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Voir aussi
* [Documentation de référence sur le Kit de développement logiciel (SDK) .NET HDInsight](https://msdn.microsoft.com/library/mt271028.aspx)
* [Administration de HDInsight à l’aide du portail Azure][hdinsight-admin-portal]
* [Administration de HDInsight à l’aide de l’interface de ligne de commande][hdinsight-admin-cli]
* [Création de clusters HDInsight][hdinsight-provision]
* [Téléchargement de données vers HDInsight][hdinsight-upload-data]
* [Prise en main d’Azure HDInsight][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]:hadoop/apache-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]:hadoop/submit-apache-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]:hadoop/hdinsight-use-hive.md
[hdinsight-use-mapreduce]:hadoop/hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


