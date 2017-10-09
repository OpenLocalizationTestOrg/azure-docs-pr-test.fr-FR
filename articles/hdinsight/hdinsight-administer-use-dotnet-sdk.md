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
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a>Gestion des clusters Hadoop dans HDInsight au moyen du Kit de développement logiciel (SDK) .NET
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Découvrez comment toomanage HDInsight clusters à l’aide de [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).

**Configuration requise**

Avant de commencer cet article, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="connect-tooazure-hdinsight"></a>Se connecter tooAzure HDInsight

Vous devez hello suivant les packages Nuget :

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

Hello exemple de code suivant vous montre comment les clusters tooconnect tooAzure avant de pouvoir administrer HDInsight sous votre abonnement Azure.

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

Vous devriez voir une invite de commandes lorsque vous exécutez ce programme.  Si vous ne souhaitez pas invite de commandes toosee hello, consultez [créer une authentification non interactive les applications .NET HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

## <a name="create-clusters"></a>Créer des clusters
Consultez [basés sur Linux de créer des clusters HDInsight à l’aide hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)

## <a name="list-clusters"></a>Énumérer les clusters
Hello extrait de code suivant répertorie les clusters et certaines propriétés :

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a>Suppression des clusters
Hello suivant extrait de code toodelete un cluster de façon synchrone ou asynchrone, utilisez : 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a>Mise à l’échelle des clusters
cluster Hello fonctionnalité de mise à l’échelle permet un nombre de hello toochange de nœuds de travail utilisé par un cluster qui s’exécute dans Azure HDInsight sans avoir toore-créer le cluster de hello.

> [!NOTE]
> Seuls les clusters ayant la version 3.1.3 de HDInsight ou une version ultérieure sont pris en charge. Si vous ne savez pas de version hello de votre cluster, vous pouvez vérifier la page de propriétés hello.  Voir [Énumération et affichage des clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
> 
> 

impact Hello modifiant nombre hello de nœuds de données pour chaque type de cluster pris en charge par HDInsight :

* Hadoop
  
    Vous pouvez augmenter de façon transparente nombre hello de nœuds de travail dans un cluster Hadoop qui est en cours d’exécution sans impact sur toutes les tâches en attente ou en cours d’exécution. Nouvelles tâches peuvent également être soumises pendant que l’opération de hello est en cours. Échecs dans une opération de mise à l’échelle sont correctement gérés afin que hello cluster est toujours conservé dans un état fonctionnel.
  
    Lorsqu’un cluster Hadoop est réduite en réduisant le nombre de hello de nœuds de données, certains services hello dans un cluster de hello sont redémarrés. Ainsi, en cours d’exécution et en attente de toofail de travaux à l’achèvement de hello Hello opération de mise à l’échelle. Vous pouvez, toutefois, renvoyer des tâches de hello une fois l’opération hello est terminée.
* HBase
  
    Vous pouvez accéder en toute transparence ajouter ou supprimer le cluster de nœuds tooyour HBase pendant son exécution. Serveurs régionaux sont équilibrés automatiquement après quelques minutes d’achèvement hello opération de mise à l’échelle. Toutefois, vous pouvez équilibrer manuellement les serveurs régionaux hello en vous connectant à un nœud principal de hello du cluster et hello en cours d’exécution suivant des commandes dans une fenêtre d’invite de commandes :
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm
  
    Vous pouvez accéder en toute transparence ajouter ou supprimer le cluster de données nœuds tooyour Storm pendant son exécution. Mais après la réussite de l’opération de mise à l’échelle de hello, vous devrez topologie de hello toorebalance.
  
    Cela peut se faire de deux façons à l’aide de :
  
  * l'interface utilisateur Web de Storm
  * l’outil d’interface de ligne de commande (CLI)
    
    Reportez-vous toohello [documentation d’Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) pour plus d’informations.
    
    interface utilisateur web de Storm Hello est disponible sur le cluster HDInsight de hello :
    
    ![Rééquilibrage de mise à l’échelle HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    Voici un exemple comment toouse hello CLI commande topologie de Storm toorebalance hello :
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

Hello suivant extrait de code montre comment tooresize un cluster de façon synchrone ou asynchrone :

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a>Octroyer/Révoquer l’accès
Clusters HDInsight ont hello suivant (tous ces services ont des points de terminaison RESTful) des services web HTTP :

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Par défaut, l'accès à ces services est octroyé. Vous pouvez révoquer ou octroyer l’accès de hello. toorevoke :

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

toogrant :

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> Par attribution/révocation de l’accès hello, vous allez réinitialiser le mot de passe et le nom d’utilisateur de cluster de hello.
> 
> 

Peut également être cela via le portail de hello. Consultez [HDInsight de gérer à l’aide de hello portail Azure][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Mettre à jour les informations d’identification de l’utilisateur HTTP
Il est même hello procédure en tant que [Grant/revoke HTTP accès](#grant/revoke-access). Si le cluster de hello a été accordée hello accès HTTP, vous devez d’abord la révoquer.  Et accorder l’accès hello avec nouvelles informations d’identification utilisateur HTTP.

## <a name="find-hello-default-storage-account"></a>Recherchez le compte de stockage par défaut hello
Hello suivant extrait de code montre comment les tooget hello nom de compte de stockage par défaut et hello clé de compte de stockage par défaut pour un cluster.

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a>Soumettre les travaux
**tâches MapReduce toosubmit**

Consultez [Exécution des exemples Hadoop MapReduce dans HDInsight](hdinsight-hadoop-run-samples-linux.md).

**travaux de ruche toosubmit** 

Consultez [Exécution de requêtes Hive avec le Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).

**travaux de Pig toosubmit**

Consultez [Exécution de tâches Pig avec le Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-use-pig-dotnet-sdk.md).

**travaux de Sqoop toosubmit**

Consultez l'article [Utilisation de Sqoop avec HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).

**travaux de Oozie toosubmit**

Consultez [Oozie utilisation avec Hadoop toodefine et exécuter un flux de travail dans HDInsight](hdinsight-use-oozie-linux-mac.md).

## <a name="upload-data-tooazure-blob-storage"></a>Télécharger le stockage d’objets Blob de données tooAzure
Consultez [télécharger des données tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Voir aussi
* [Documentation de référence sur le Kit de développement logiciel (SDK) .NET HDInsight](https://msdn.microsoft.com/library/mt271028.aspx)
* [Administrer HDInsight à l’aide de hello portail Azure][hdinsight-admin-portal]
* [Administration de HDInsight à l’aide de l’interface de ligne de commande][hdinsight-admin-cli]
* [Création de clusters HDInsight][hdinsight-provision]
* [Télécharger des données tooHDInsight][hdinsight-upload-data]
* [Prise en main d’Azure HDInsight][hdinsight-get-started]

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


